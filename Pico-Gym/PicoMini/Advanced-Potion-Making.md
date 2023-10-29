# Challenge Description
Ron just found his own copy of advanced potion making, but its been corrupted by some kind of spell. Help him recover it!

## Solution approach
You may want to see my writeup from c0rrupt (pico2019), since I approached this challenge immediately after completing that challenge. The same background from there applies here...
- The magic bytes for PNG files are right [here](https://en.wikipedia.org/wiki/List_of_file_signatures)
- This [site](http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html) explains how PNG files work
- [hexed.it](hexed.it) allows you to change files on the web (or you can use **hexedit** if you prefer)
- [This site](https://www.nayuki.io/page/png-file-chunk-inspector) allows you to check out what's wrong with your png file (or you can use **pngcheck** if you prefer - though the website is much more informative about what's wrong with your file)

I used the provided websites more. Anyways, let's open up the file

<img width="518" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/f2cd7b7e-0e13-46e4-b0ec-59dd0ed0473b">

Alright, we got sRGB and gAMA running all over the place. Looks like another corrupted PNG file. I fixed the magic bytes and used the PNG checker site (linked above) to fix the length of the IHDR chunk. The fixed code looks like this:

<img width="516" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/f607a9a5-1bf3-49ba-98df-bb3a044cac81">


Overall, much easier to fix this PNG file than in c0rrupted, probably because I had a better idea of what I was doing. At this point, it was possible to open up the PNG image, and I was greeted with a red square.

![image](https://github.com/Leonard514/CTF-Writeups/assets/92343899/e20912b5-4853-4f3c-a996-28505e699adf)


My first instinct was that this was a least significant bit stego challenge, and I used this [site](https://stylesuxx.github.io/steganography/), but it turned up nothing.
