# Challenge Overview

We are greeted with a webpage that's completely blank. The source code is available [here](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas22Source.html)

# Challenge Approach

The source code states that if there is a **revelio** parameter in the GET request, then the admin password is revealed. This challenge is trivially easy since all that is required is to supply the new parameter in the GET request. I sent the GET request to the site to the Burp Repeater and appended the parameter as follows:

<img width="398" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/0e7ed41a-b6fc-404f-b732-bdae1ea13bff">


Upon sending the request, I gain the admin password for the next challenge
