# x64 Cheat Sheet


## x64 Registers

8-byte register | Byte 0-3 | Bytes 0-1 | Byte 0
----------------|----------|-----------|-------
%rax | %eax | %ax | %al
%rcx | %ecx | %cx | %cl
%rdx | %edx | %dx | %dl
%rbx | %ebx | %bx | %bl
%rsi | %esi | %si | %sil
%rdi | %edi | %di | %dil
%rsp | %esp | %sp | %spl
%rbp | %ebp | %bp | %bpl
%r8 | %r8d | %r8w | %r8b
%r9 | %r9d | %r9w | %r9b
%r10 | %r10d | %r10w | %r10b
%r11 | %r11d | %r11w | %r11b
%r12 | %r12d | %r12w | %r12b
%r13 | %r13d | %r13w | %r13b
%r14 | %r14d | %r14w | %r14b
%r15 | %r15d | %r15w | %r15b

## Operand Specifiers

Type | From | Operand Value | Name
-----|------|---------------|-----
Immediate | $Imm | Imm | Immediate
Register | E<sub>2</sub> | R[E<sub>a</sub>]| Register
Memory | Imm | M[Imm]| Absolute
Memory | (E<sub>2</sub>) | M[R[E<sub>b</sub>]] | Absolute
Memory | Imm[E<sub>b</sub>, E<sub>i</sub> s] | M[Imm + R[E<sub>b</sub>] + (R[E<sub>i</sub>] x s) | Scaled Index

## Data Movement

###### b = byte, w = word, l = doubleword (4 byte integer), q = quadword (8 byte integer)
###### s = source, d = destination

Instruction | Description
------------|------------
One suffix |    
mov  *s, d* | Move source to destination
push *s* | Move source to stack
pop *d* | Pop top of stack to destination
Two suffixes | 
mov *s, d* | Move byte to word (zero extended)
push *s* | Move byte to word (zero extended)
No suffix |
cwtl | Convert word in *%ax*to doubleword in *%eax* (sign-extended)
cltq | Convert doubleword in *%eax* to quadword in *%rax* (sign-extended)
cqto | Convert quadword in *%rax* to octoword in *%rdx:%rax*

