# Challenge Description
Can you get the flag? Download this binary. Here's the test drive instructions:

- $ chmod +x gdbme
- $ gdb gdbme
- (gdb) layout asm
- (gdb) break *(main+99)
- (gdb) run
- (gdb) jump *(main+104)

# Useful Notes

Yes, the challenge is really as easy as following the instructions you are given. However, I think this teaches a few useful lessons to someone with absolutely no experience with assembly. Namely, you can run an assembly file, make it stop running at any point, make it continue running at a point, etc. Here is the layout of the file:


<img width="467" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/1bbf9793-27fe-4b55-a2d6-000f387f290a">
