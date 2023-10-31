# Challenge Description
What does asm3(0xd73346ed,0xd48672ae,0xd3c8b139) return? Submit the flag as a hexadecimal value (starting with '0x'). NOTE: Your submission for this question will NOT be in the normal flag format.

## Assembly Code
```
asm3:
	<+0>:	push   ebp
	<+1>:	mov    ebp,esp ; set up everything
	<+3>:	xor    eax,eax ; clear eax register, eax = 0
	<+5>:	mov    ah,BYTE PTR [ebp+0xa] ; eax = 3300
	<+8>:	shl    ax,0x10; shift ax left 16 bytes. eax = 0
	<+12>:	sub    al,BYTE PTR [ebp+0xc]; eax = 0051 (note: is like 00ff - 00ae)
	<+15>:	add    ah,BYTE PTR [ebp+0xd]; eax = 7251
	<+18>:	xor    ax,WORD PTR [ebp+0x10]; eax = 0xb139 ^ 0x7251
	<+22>:	nop; does nothing
	<+23>:	pop    ebp; clean up stack
	<+24>:	ret; return value of eax
```

## Helpful Guides

[Pico 2018 - Assembly 3](https://www.youtube.com/watch?v=3aleJWRZEFY&list=PLJ_vkrXdcgH8l7m6PDGxYQm3GHS_5zRmx&index=88)

[Assembly Registers](https://wiki.skullsecurity.org/index.php?title=Registers)

### Assembly Buffer of inputs

```
10, 11, 12, 13 - 39, b1, c8, d3
c, d, e, f - ae, 72, 86, d4
8, 9, a, b - ed, 46, 33, d7
4 - return address
0 - ebp
```

### Solution Methods

Work In Progress
