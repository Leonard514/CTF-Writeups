# Challenge Overview

We are greeted with a page that says that for security reasons, they filter on even more characters, and a search box for finding words in a dictionary containing the string. This seems to be a continuation of the command injection scenario from Challenges 9-10. Let’s see the source code:

<img width="375" alt="Screenshot 2024-03-20 005558" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/1a00adf4-b8ba-4beb-970b-5fbda95f9d18">

Natas had command injection in challenges 9-10. This challenge restricts semicolons, pipes, and ampersands as in challenge 10. This time, they also added ` characters, backslashes, and quotes. In addition, our key variable is wrapped in double quotes.


## Challenge Approach

This does not go nearly as smoothly as I retell it. Since I am quite the beginner with these web challenges, I have taken the liberty to read only the titles of video writeups to these challenges, so that I am not completely lost and I may start by seeing how similar challenges are solved. It is already quite the challenge to learn how to execute these techniques, but the difficulty is squared if, for example, you were to approach a blind SQL challenge without knowing what blind SQL was.


After I watched a [video tutorial](https://www.youtube.com/watch?v=TrWw6vrOuLI), I learned I could use $() to run commands (and I learned afterwards that these are called subshells), and their output would be placed where the variables are. This means I essentially have piping functionality if I nest the subshells, only that the grep being executed is the final command. Taking the hint from seeing that this was a "blind command injection" challenge, the following strategy was formulated:

- Find a way to fetch one character at a time from the /etc/natas_webpass/natas17 file and output it
- The character seen in every entry is the character of a given index
- Reconstruct the password character by character

I eventually found that **cut** did the trick. Here was my payload:

**$(cut -c <index> /etc/natas_webpass/natas17)**

I then sent the first request and used burpsuite's intruder to automate the index. I then had a partial reconstruction of the flag, but there were two problems.
- The alphabetic characters in the search results are case-insensitive due to the -i argument in grep
- The numeric digits are unknown because there are no digits in the dictionary (and this can be verified by entering a ^ or $ in the search results, which will dump the whole dictionary since they stand for the beginning or end of lines in regex).

## New Task: Confirm cases and numeric digits.

- Approach 1: Shift ASCII values of numbers and letters (the numbers up, the letters down). This failed because the commands used illegal characters
- Approach 2: Make a boolean expression to test the values of each of the characters. I was hoping they would evaluate to True/False as they do in Python, but they evaluated to 1 and 0 instead.
- Approach 3: Use parameter expansion. This fails because this requires saving a value to a variable, but we can only execute one line of code.
- Approach 4: Upload a payload file with digits and capital/lowercase letters as the first character and unique consonants/vowels as the second character. It seemed like a genius plan until I realized Natas16 has no access to the files in Natas 12's directory.
- Approach 5: Use /etc/passwd. This approach may be possible since /etc/passwd contains both numbers and letters, but it seems difficult to manipulate the file (many variants of nested cut may be required)
- Approach 6: This one seems more reasonable. Use nested subshells. After obtaining a given character via cut, I would grep the file with case-sensivity in a subshell (and I would configure it to grep for that character being the first), use head to extract the first result, then pass that result into the search. For example, a lowercase a should yield search results of the first string in the dictionary that had a lowercase a, while an uppercase A would likely yield an A and therefore all results with an a (case-insensitive), and in this manner I should be able to tell the case. For the digits, I will use cat with the option to number the lines, then use head to extract only the first 9-10 lines, grep that (for the digits), then use cut to remove the index, and in this manner one of the first 9-10 of the dictionary entries will be passed into the final grep, and I will be able to tell by the results which number it is.

## Executing Approach 6a - Reconnaissance (on Natas9)

I started by doing some recon on Natas9 using burpsuite's repeater. I wanted to _start with the letters_, and my goal was to grep for a certain letter but only for the first character. That way, each letter and case would yield a different first word, which I would then output into the parent command **grep -i**.

[This source](https://askubuntu.com/questions/964465/how-to-use-grep-to-match-lines-where-the-first-character-falls-in-a-range) used for Approach 6a

Initial Payload: `grep -i "$(grep "^[A]" dictionary.txt | head -n 2 | tail -n 1)" dictionary.txt`

This searched for all entries in the dictionary that started with a given character (case-sensitive), then extracts the second entry using head and tail (because the first entry usually yielded that letter, uppercase or lowercase, so that it would be impossible to tell the difference). I then extracted that into the case-insensitive grep of the dictionary (to simulate Natas 16 - though in the real challenge, I would have to use nested subshells instead of pipes)

I then used Burpsuite's intruder to cycle through all the alphabetic characters, uppercase and lowercase, for the character in the regex. I found that there were no entries for Q, R, or Z, so that the entire dictionary was dumped instead. Fortunately I know which characters those are without their case.

Modified Payload: `$(tail -n 1 $(head -n 2 $(grep "^[$(cut -c <index> /etc/natas_webpass/natas17)]" dictionary.txt)))`

I then realized that the regex used double quotes, which are forbidden. I then realized the head and tail subshells were breaking since they demanded a file instead of standard input. After some toying around, I tried something new:

`1; grep -i "$(grep §A§e dictionary.txt)" dictionary.txt #`

- This essentially takes an alphabetic character and appends an `e` to it, then does a case-sensitive grep of the dictionary. The result is then used for a case-insensitive grep of the dictionary, where the §A§ can be replaced by any alphabetic character (yes, I did copy-paste this from burpsuite). Attacking all the alphanumeric characters on the dictionary yielded different results for each case - positive reuslts! Of course the plan would be to replace §A§ with the cut subshell from earlier and use the differentiated results to decipher the case of each letter in the password. As a side effect, searches with no results dumped the whole file due to the regex $ in the "" (and in this case I don't have to worry about the "" being prohibited - that's there to simulate how Natas16 would respond since I was testing on Natas 9 for greater flexibility)

#### Finishing Approach 6a (determining case)

Final payload: `$(grep $(cut -c §0§ /etc/natas_webpass/natas17)e dictionary.txt)`

Where §0§ is a number (index) from 1 to 32 used to extract each character of the password

I then automated the index with burpsuite's intruder and used the testing payload to differentiate the cases

I then made a partially constructed password **with** the cases, but not the numbers. That would require another approach.

# Task: Find digits

- I initially wanted to try and concatenate the dictionary file with line numbers (-n argument), using some grepping and cutting, to differentiate the files. In time I realized this would not work since subshells and piping aren't going to work the same (with subshells, you place the output as text to input into the next command, but grep, cut and cat all demand a file as input - an unworkable situation)

- I then developed a new approach: I would use the number from the cut command and I will execute **tail** with the -n to vary the number of lines, and I will have the password digit change the number of lines. In tests for the previous approach, I found that if I returned a multiline output for a grep, then it would only grep the first line. After some payload tests, the approach was surprisingly easy:


Payload for Natas9 (used for testing due to no restrictions): `grep -i "$(tail -n §0§ dictionary.txt)" dictionary.txt

Payload for Natas16 (the actual level): `$(tail -n $(cut -c §0§ /etc/natas_webpass/natas17) dictionary.txt)`

I then automated the index with burpsuite's intruder and used the Natas9 test results for comparison. I then obtained the password with the cases.
