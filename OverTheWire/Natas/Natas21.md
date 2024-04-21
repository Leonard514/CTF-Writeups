# Challenge Overview

We are greeted with a page that says this site is colocated with another site

<img width="292" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/d1a767ed-899e-4b95-9eed-5dd27511dd44">


This is what the other site looks like:



<img width="298" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/cc463e6f-d2ff-41ad-991f-96036a530dfe">



[Natas 21 Source Code](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas21Source.html)

[Natas 21 Colocated Site Source Code](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas21Source.html)


# Challenge Approach

The source code for Natas 21 will check if the session cookie has a value 'admin' set to 1. If so, it gives the password, and if not, it doesn't

The source code for the Natas 21 colocated website will make key:value pairs for each submitted to the website. It makes a form that allows for the submission of an alignment, fontsize, and background color. However, this is where the trick comes in. If we feed the website the `admin = 1` directly, then we could give our session ID admin powers. With this in mind, the following was done:

- I clicked the **update** button on the website to feed it a POST request so that I could send it to the Burp Repeater. With that, I just added a new parameter `admin` and set it to 1 (see image - notice I also had debugging to confirm the changes). This gave the PHPSESSID cookie that I sent the website admin powers. 
- At that, I just grabbed the session ID I sent in the POST request and pasted it into my PHPSESSID cookie in the original website and reloaded the page. It then gave me the flag.

<img width="779" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/971c9454-9e92-44c7-91a0-10dc9e5be125">
