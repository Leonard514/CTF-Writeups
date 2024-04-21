# Challenge Overview

<img width="323" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/5f019cf4-94cf-4a46-9b64-467e43c2641b">


Once again, we are greeted with a page that allows us to put in a password.

The [source code](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas24Source.html) has PHP do a strcmp (see docs [here](https://www.php.net/manual/en/function.strcmp.php)), makes a NOT of the result, and if a truthy value is returned, the password is printed.


# Challenge Approach

strcmp, according to the documentation, returns -1 if the first string is less than the second string; 0 if the first string is equal to the second string; and 1 if the first string is greater than the second string.

Once again, the helpful [OWASP document about PHP type juggling](https://web.archive.org/web/20201112021256/https://owasp.org/www-pdf-archive/PHPMagicTricks-TypeJuggling.pdf) came up. In fact, if you scrolled to the bottom of the document, the way it messes with strcmp() basically spoiled the whole challenge. 

<img width="614" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/aa923014-7d4f-4c0b-a41d-d4251c6c5542">


Essentially, if I made an array of a password instead of a string, it returns NULL. Now, the PHP code should NOT the NULL to return what is probably a truthy value... and it works! Here's how I made an array of the password using burpsuite:

<img width="402" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/f7032cf6-2726-415c-acf9-cc3e2abb82a5">
