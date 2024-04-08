# Challenge Overview

We are greeted with a page where once again we are logged in as a normal user, but we need to be logged in as an admin. We have a text box to enter a string and a button to allow us to change a name

Source code available [here](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas20Source.html)

## Source code analysis: PHP Commands

We have debug functions, functions to print credentials... most of the functions other than myread and mywrite are completely useless


Let's start with the **myread** function

**strspn** returns an integer n, the first n characters of a string that are composed entirely of a given mask. strspn is used in myread to check if the PHPSESSID has only alphanumeric characters (and dashes - for if it didn't, strspn would return a different integer than a length function)

**explode** is basically Python's built-in split (I'd assume you have some familiarity with Python as I do - but if not, it essentially takes a string and splits it into an array of elements separated by a given separator). In this case, it is first used to read from a file (located in /var/lib/php/sessions/mysess_sid) each line to debug output. Then for each line, it takes the first two elements separated by spaces

The part of the $parts = explode... according to ChatGPT, this reads session data from a file into the $_SESSION array in a readable format (and this is called deserializing), while session_encode() reserializes it


etc etc etc

## Challenge Approach

I tried a sequencer on burpsuite, but the cookies were generated pretty randomly (with the alphanumeric characters). I floundered around on Cryptocat's DVWA tutorials for some time because I didn't know what to do. XSS tutorials looked pretty interesting, so I put in some JS in the name input box:

`<script>alert("hrar")</script>`

With the debugging option enabled (through appending **?debug** to the URL), I found the JS is executed three times, and twice before the admin check is enabled.


The first hacking session grows late, but the goal for the next session is to find a way to inject JS that changes the value of `$_SESSION["admin"]` to 1 (if it be possible)
