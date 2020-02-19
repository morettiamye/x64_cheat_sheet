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
Memory | (E<sub>2</sub> | M[R[E<sub>B</sub>]] | Absolute
