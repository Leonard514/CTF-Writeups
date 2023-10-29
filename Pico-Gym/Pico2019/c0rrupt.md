# Challenge Description
We found this file. Recover the flag
- Hint 1: Try fixing the file header

Initially, I was a bit lost with this challenge. **file** yielded that it was a data file, and then I found this output from **xxd:**

<img width="284" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/3e4e7a91-678a-4a38-a6e6-8426e8083864">

I knew that sRGB was a color scheme used by image files, and this gave a clue. I then performed **xxd** on a PNG file and found it had a similar output. At that point, I knew I had to fix the PNG file... and the process was incredibly messy. The writeup presents a more streamlined solution that was found after the flag was captured (and many hours of work were put in).

First and foremost come some important resources.
- The magic bytes for PNG files are right [here](https://en.wikipedia.org/wiki/List_of_file_signatures)
- This [site](http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html) explains how PNG files work
- [hexed.it](hexed.it) allows you to change files on the web (or you can use **hexedit** if you prefer)
- [This site](https://www.nayuki.io/page/png-file-chunk-inspector) allows you to check out what's wrong with your png file (or you can use **pngcheck** if you prefer - though the website is much more informative about what's wrong with your file)

So when we start with the file, the magic bytes aren't even configured correctly. Use the PNG magicbytes from Wikipedia and hexed.it to change them to what they're supposed to be (89 50 4E 47 0D 0A 1A 0A)
<img width="692" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/50276f33-e239-4a32-9943-7f7df95958c8">

After the magic bytes are fixed, an issue pops up with an IHDR chunk. According to the PNG documentation, an IHDR chunk is required first. It simply doesn't exist in this file. In order to find out the correct bytes, I would upload a normal PNG file to hexed.it. Then, we see we need to replace `43 22` with `49 48`.

<img width="652" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/c35948cc-cb2e-4aee-b0f2-a0bbd509b3af">


At this point, your file should look like this:

<img width="515" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/72d20890-b9d5-4775-b7fb-5efd5e60ed9a">


After that, we can upload our file to the PNG checker site again, where it shows that the pHYS header has an unusually high horizontal resolution. Let's take a look at the PNG documentation...

```
The pHYs chunk specifies the intended pixel size or aspect ratio for display of the image. It contains:

   Pixels per unit, X axis: 4 bytes (unsigned integer)
   Pixels per unit, Y axis: 4 bytes (unsigned integer)
   Unit specifier:          1 byte
```
from [PNG documentation](http://www.libpng.org/pub/png/spec/1.2/PNG-Chunks.html)

Indeed, the AA byte immediately after the pHYS is causing this unusually high horizontal resolution. Let's change it to `00`

<img width="511" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/9a6cb8b2-b001-4caf-9a29-42a7ac819f40">


After this, we get an error from the PNG checker that we have a massive chunk that overflows over the rest of the file: 

<img width="650" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/a7b1787b-05e0-44e5-ba17-356f6e7bac3c">


This only makes sense when we look at a normal PNG file

<img width="506" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/151834ff-beda-4e4f-9033-f19a8db3f47c">

Here in this normal PNG file, an IDAT chunk is started very soon after some of the other chunks, but this is not the case in the corrupted PNG file. However, there is an uncanny similarity of characters around the circled region. In addition, a DET chunk is not found in the documentation, so this is likely another modification. Let's fix that!

<img width="511" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/83c8b545-0ce2-4503-a261-c2152d0790d4">


After the fix, we still have to contend with the unusual data length of the chunk. Those two aa bytes are highly responsible, so let's set them to `00 00` to make the data length more reasonable.

<img width="650" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/69d4c0ad-1b66-4ff1-a15b-1a6be70f422a">

At that point, if you put the PNG file into the checker, things should be normal. And indeed, you can open the file and extract your well-earned flag.
