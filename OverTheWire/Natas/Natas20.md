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

### Approach 1: XSS?

I tried a sequencer on burpsuite, but the cookies were generated pretty randomly (with the alphanumeric characters). I floundered around on Cryptocat's DVWA tutorials for some time because I didn't know what to do. XSS tutorials looked pretty interesting, so I put in some JS in the name input box:

`<script>alert("hrar")</script>`

With the debugging option enabled (through appending **?debug** to the URL), I found the JS is executed three times, and twice before the admin check is enabled.


I then looked up a bunch of actual XSS challenge videos and found that this wasn't what I was looking for. In XSS, we want an "admin" script to execute our JS payload, and we didn't have such a thing here.


### Approach 2: PHP injection

I then saw that the name input option seemed pretty vulnerable. I first wanted to inject PHP code that set the variable `$_SESSION["admin"]` to 1 directly, inputting payloads like `$_SESSION["admin"] = 1`, but this did nothing.

I then noticed how in the source code, how the session data was read by taking pairs of strings in the file for each data piece (key and value), with the key-value pairs separated by newlines. The course of action then became obvious: make a dummy name and put in a newline, then put `admin 1` after it. It would then write that to a file, after which I could reload the page with the same cookie, where the file would be read and `$_SESSION['admin']` would be set to 1 (meaning I get the flag)

Now, URL encoding a newline consists of `%0D%0A` rather than \n (which I had gotten used to with my experience in Python). Once I put in the payload, I extracted my flag.
