# Challenge Overview

We are greeted with a page that says we must log in with admin credentials. Click [here](https://github.com/Leonard514/CTF-Writeups/blob/main/OverTheWire/Natas/Natas18Source.html) for the source


# Challenge approach

The source shows that it is "impossible" to change the admin part of the PHP session to be 1 (true). I sent some POST requests (testing some credentials), and saw that there was a PHPSESSID cookie:

<img width="469" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/f7eb8652-adb2-4394-a14f-45467f4bed26">


Now, I must remind you (from the Natas16 writeup) that I've taken the liberty to read titles for video writeups to these challenges. The title to this challenge said something about brute-forcing the session IDs. I decided it would be best to watch a tutorial to see how these kinds of things worked, so I watched [this one](https://www.youtube.com/watch?v=xzKEXAdlxPU&list=PLHUKi1UlEgOJLPSFZaFKMoexpM6qhOb4Q&index=10) about weak session ids. It essentially said that if we modified the session id to be of another user, we could immediately log in as that user without knowing his credentials. As such, the course of action was pretty obvious. I would use burpsuite's intruder to brute-force the PHPSESSID cookie from 1 to 640 (its maximum value) and get requests until I yielded a response with the password. This I did.

<img width="470" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/19d83fd5-843c-43e8-b784-ad00a9a80bb2">
