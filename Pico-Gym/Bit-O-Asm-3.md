# Challenge Description

Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Download the assembly dump here.

- Hint 1: Not everything in this disassembly listing is optimal.


## Assembly Dump
```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret
```

## Solution Process

The assembly code first becomes relevant at <+15>.

- 0x9fe1a moved into **[rbp-0xc]**
- 0x4 moved into **[rbp-0x8]**
- **[rbp-0xc]** (0x9fe1a) moved into **eax**
- According to [this source](https://www.cs.virginia.edu/~evans/cs216/guides/x86.html), imul multiplies operands and stores the results in the first operand. In **eax**, the value of 0x9fe1a * 0x4 is stored.
- Add 0x1f5 to whatever is in eax
- Move this value into **[rbp-0x4]** and then back into **eax**
- Return the value

I then made code in Python to calculate the final value as the flag. The convenient thing is Python automatically converts to decimal.

  ```python
  print(0x9fe1a * 0x4 + 0x1f5)
  ```
