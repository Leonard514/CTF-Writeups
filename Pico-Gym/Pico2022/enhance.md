# Challenge Description

Download this image file and find the flag

![drawing flag](https://github.com/Leonard514/CTF-Writeups/assets/92343899/d471e450-6c7b-432c-b775-410f761791b9)

# Challenge Approach

The commands **exiftool**, **binwalk**, and stego commands do nothing. However, running a hexedit tells us that the file was made with inkscape. As such, inkscape was downloaded and the file was opened in inkscape.

<img width="960" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/4d973f91-a2ec-4768-929f-e69683a97475">


Use of CTRL + A in inkscape tells us that there are text, ellipse, and circle objects. The text object probably contains the flag, so tab was used to select and find the text object, which was within three concentric ellipses - some zooming and size modification of ellipses and textboxes were required since the text object was tiny
