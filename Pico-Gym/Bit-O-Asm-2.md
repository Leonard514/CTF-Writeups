# Challenge Description


Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Download the assembly dump here.
- Hint 1: PTR's or 'pointers', reference a location in memory where values can be stored.

## Assembly dump

```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret
```

## Solution Process

This is a quick solve. We see in <+15> that **0x9fe1a** is placed into **[rbp-0x4]**, which is then placed in **eax**. As such, we only need to translate 0x9fe1a to decimal to get the flag.
