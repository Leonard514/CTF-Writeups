# Challenge Description

What does asm2(0x4,0x2d) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format.

- Hint 1: [List of Assembly Conditions](https://www.tutorialspoint.com/assembly_programming/assembly_conditions.htm)

## Assembly Code

```
asm2:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp
	<+3>:	sub    esp,0x10
	<+6>:	mov    eax,DWORD PTR [ebp+0xc]
	<+9>:	mov    DWORD PTR [ebp-0x4],eax
	<+12>:	mov    eax,DWORD PTR [ebp+0x8]
	<+15>:	mov    DWORD PTR [ebp-0x8],eax
	<+18>:	jmp    0x50c <asm2+31>
	<+20>:	add    DWORD PTR [ebp-0x4],0x1
	<+24>:	add    DWORD PTR [ebp-0x8],0xd1
	<+31>:	cmp    DWORD PTR [ebp-0x8],0x5fa1
	<+38>:	jle    0x501 <asm2+20>
	<+40>:	mov    eax,DWORD PTR [ebp-0x4]
	<+43>:	leave  
	<+44>:	ret    
```

This challenge took a while mostly since I didn't know what was going on. The good news is that picoCTF pushed out video solutions of their CTFs from _2018_, and they had [a challenge](https://www.youtube.com/watch?v=o9aVQdnhtmQ&list=PLJ_vkrXdcgH8l7m6PDGxYQm3GHS_5zRmx&index=58) that was nearly identical to this one (just with different numbers). The 2018 challenges are not on the picogym, so viewing their solutions is fair game. From this point, I will be consulting that guide to help me with the 2019 challenges

Regardless, we need to know how the assembly works. Let's do an explanation. ChatGPT happens to explain the first three bits better than I can, so I'll paste that in real quick...

```
`push ebp`: This instruction pushes the current value of the `ebp` (base pointer) register onto the stack. It is typically done at the beginning of a function to save the previous base pointer value.

`mov ebp, esp`: This instruction sets up a new stack frame by moving the value of the stack pointer (`esp`) into the base pointer (`ebp`). This is a common step in function prologues to create a stack frame for the current function.

`sub esp, 0x10`: This instruction subtracts 16 bytes from the stack pointer (`esp`). This is typically done to allocate space for local variables on the stack. In this case, 16 bytes (0x10 in hexadecimal) are reserved for local variables.
```

The next bits can be explained by watching the video I linked. Remember that asm2() has two parameters according to the description. Here, it seems we are storing our function input parameters into the buffer we just made for our local variables. According to the video, the first parameter will be stored in **[ebp+0x8]** since it is not as far up the stack. As such, this means the second parameter of the function **[ebp+0xc]** is actually stored _first_. This means the first parameter is stored in **[ebp-0x8]**, and the second parameter in **[ebp-0x4]**. After storing our local variables, we jump to a compare statement.

In the compare statement, we check if our first parameter is less than or equal to **0x5fa1**. If so, we jump to commands where we add 1 to the second parameter and 0xd1 to the first parameter, then do the comparison again. Once the comparison is over, the second parameter **[ebp-0x4]** is moved to register **eax** to be returned. Let's compile some Python that is comparable...

```python
def asm2(arg1, arg2):
    var1 = arg2 # remember the second parameter is stored first... var1 is [ebp-0x4]
    var2 = arg1 # var2 is [ebp-0x8]
    while var2 <= 0x5fa1:
        var1 += 1
        var2 += 0xd1
    return var1

flag = asm2(0x4,0x2d)

print(flag)
```

Running this Python code should be enough. From now on, I'll probably try to reconstruct assembly in another programming language if tracing is too difficult (as it is here). Don't forget to convert your decimal flag to hexadecimal at the end.
