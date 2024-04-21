# Challenge Overview

<img width="323" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/5f019cf4-94cf-4a46-9b64-467e43c2641b">


We are greeted with a page that allows us to put in a password.

The [source code](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas23Source.html) has PHP check if the password contains the substring `iloveyou` (see strstr docs [here](https://www.php.net/manual/en/function.strstr.php)) and if something about the password is greater than 10.


# Challenge Approach

Remember that I took the liberty to see video titles so that I am not completely lost with these new challenges. Now, in this case, I had to learn about PHP type juggling. I found that [this resource](https://web.archive.org/web/20201112021256/https://owasp.org/www-pdf-archive/PHPMagicTricks-TypeJuggling.pdf) is pretty helpful - it even gives real-world examples!

I think this portion should be the most telling:

<img width="352" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/06395b97-72cc-415b-b7bd-10b5a13d98aa">


It basically shows us that if we spit out a bunch of numbers at the beginning of the string, PHP could compare those numeric characters to a given number and perform an operation.

I then put a password `999999iloveyou` into the box. The first is fulfilled by the appropriate substring, while in the second, 999999 is found to be greater than 10 and passes. The flag was then yielded
