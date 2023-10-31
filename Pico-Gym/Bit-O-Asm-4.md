# Challenge Description
Can you figure out what is in the eax register? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Download the assembly dump here.
- Hint 1: Don't tell anyone I told you this, but you can solve this problem without understanding the compare/jump relationship.
- Hint 2: Of course, if you're really good, you'll only need one attempt to solve this problem.

## Assembly Dump

```
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
```

## Solution Process

Once again, the relevant code starts at <+15>.
- 0x9fe1a is moved into **[rbp-0x4]**
- **[rbp-0x4]** (0x9fe1a) compared to 0x2710. Since 0x9fe1a is not less than or equal to 0x2710, the jump is ignored.
- 0x65 subtracted from 0x9fe1a
- jump to <+41>, which sends **[rbp-0x4]** to **eax** to be returned

Here's some python code:

```python
print(0x9fe1a - 0x65)
```
