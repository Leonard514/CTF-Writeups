# Challenge Description

I wrote you a song. Put it in the picoCTF{} flag format.
- Hint 1: Do you think you can master rockstar?

## Relevant File

```
Pico's a CTFFFFFFF
my mind is waitin
It's waitin

Put my mind of Pico into This
my flag is not found
put This into my flag
put my flag into Pico


shout Pico
shout Pico
shout Pico

My song's something
put Pico into This

Knock This down, down, down
put This into CTF

shout CTF
my lyric is nothing
Put This without my song into my lyric
Knock my lyric down, down, down

shout my lyric

Put my lyric into This
Put my song with This into my lyric
Knock my lyric down

shout my lyric

Build my lyric up, up ,up

shout my lyric
shout Pico
shout It

Pico CTF is fun
security is important
Fun is fun
Put security with fun into Pico CTF
Build Fun up
shout fun times Pico CTF
put fun times Pico CTF into my song

build it up

shout it
shout it

build it up, up
shout it
shout Pico
```

## Challenge Approach

I felt since over 20000 people had solved this challenge that it would be simple. So I went and looked up `CTF Rockstar` on Google, and other than writeups that I didn't want to look at for obvious reasons, I found a [Rockstar programming language executor](https://codewithrockstar.com/online). I went and pasted the lyrics into the form and ran it, and it outputted a bunch of ASCII/Unicode values, after which I wrote a simple Python program to convert those values to text

<img width="519" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/61fc74a9-1b1c-4efd-8f54-7d3ea7a09932">

```python
list = input().split()

for i in list:
    print(chr(int(i)), end='')
```

Putting the ASCII into this program yields the flag (without the suffix). We're done!
