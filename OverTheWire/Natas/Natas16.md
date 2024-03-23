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
