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

###### Imm = constant value, E<sub>x</sub> = register, 
###### R[E<sub>x</sub>] = value stored in E<sub>x</sub>, M[x] = value stored at memory address

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
cwtl | Convert word in *%ax* to doubleword in *%eax* (sign-extended)
cltq | Convert doubleword in *%eax* to quadword in *%rax* (sign-extended)
cqto | Convert quadword in *%rax* to octoword in *%rdx:%rax*


## Arithmetic Operations

### Unary Operations

Instruction | Description
------------|------------
inc *d* | Increment by 1
dec *d* | Decrement by 1
neg *d* | Arithmetic negation
not *d* | Bitwise complement

### Binary Operations

Instruction | Description
------------|------------
leaq *s, d* | Load effective address of source into destination
add *s, d* | Add source to destination
sub *s, d* | Subtract source from destination
imul *s, d* | Multiply source by destination
xor *s, d* | Bitwise XOR (exclusive or) destination by source
or *s, d* | Bitwise OR destination by source
and *s, d* | Bitwise AND destination by source

### Shift Operations

Instruction | Description
------------|------------
sal/sdl *k, d* | Left shift destination by *k* bits
sar *k, d* | Arithmetic right shift by *k* bits
shr *k, d* | Logical right shift by *k* bits

### Special Arithmetic Operations

Instruction | Description
------------|------------
imulq *s* | Signed full multiply of *%rax* by *s*, result stored in  *%rdx*:*%rax*
mulq *s* | Unsigned full multiply of *%rax* by *s*, result stored in  *%rdx*:*%rax*
idivq *s* | Signed divide *%rdx*:*%rax* by *s*, quotient stored in *%rax*, remainder stored in *rdx*
divq *s* | Unsigned divide *%rdx*:*%rax* by *s*, quotient stored in *%rax*, remainder stored in *rdx*


## Comparisons and Tests

Instruction | Description
------------|------------
cmp *s<sub>2</sub>*, *s<sub>1</sub>* | Set condition codes according to *s<sub>1</sub>* - *s<sub>2</sub>*
test *s<sub>2</sub>*, *s<sub>1</sub>* | Set condition codes according to *s<sub>1</sub>* - *s<sub>2</sub>*

## Condition Codes

### Conditional Set Instructions

Instruction | Description | Condition Code
------------|-------------|---------------
sete/setz *D* | Set if equal/zero | **ZF**
setne/setnz *D* | Set if not equal/nonzero | **~ZF**
sets *D* | Set if negative | **SF**
setns *D* | Set if nonnegative | **~SF**
setg/setnle *D* | Set if greater (signed) | **~(SF^0F)&~ZF**
setge/setnl *D* | Set if greater or equal (signed) | **~(SF^0F)**
setl/setnge *D* | Set if less (signed) | **SF^0F**
setle/setng *D* | Set if less or equal | **(SF^0F)|ZF**
seta/setnbe *D* | Set if above (unsigned) | **~CF&~ZF**
setae/setnb *D* | Set if above or equal (unsigned) | **~CF**
setb/setnae *D* | Set if below (unsigned) | **CF**
setbe/setna *D* | Set if below or equal (unsigned) | **CF** or **ZF**


### Jump Instructions

Instruction | Description | Condition Code
------------|-------------|---------------
jmp | Jump to label | 
jmp *operand* | Jump to specified location
je/jz | Jump if equal/zero | **ZF**
jne/jnz | Jump if not equal/zero | **~ZF**
js | Jump if negative | **SF**
jns | Jump if nonnegative | **~SF**
jg/jnle | Jump if greater (signed) | **~(SF^0F)&~ZF**
jge/jnl | Jump if greater or equal (signed) | **~(SF^0F)**
jl/jnge | Jump if less (signed) | **SF^0F**
jle/jng | Jump if less or equal | **(SF^0F)|ZF**
ja/jnbe | Jump if above (unsigned) | **~CF&~ZF**
jae/jnb | Jump if above or equal (unsigned) | **~CF**
jb/jnae | Jump if below (unsigned) | **CF**
jbe/jna | Jump if below or equal (unsigned) | **CF** or **ZF**


### Conditional Move Instructions

Instruction | Description | Condition Code
------------|-------------|---------------
cmove/cmovz *S, D* | Move if equal/zero | **ZF**
cmovne/cmovnz *S, D* | Move if not equal/nonzero | **~ZF**
cmovs *S, D* | Move if negative | **SF**
cmovns *S, D* | Move if nonnegative | **~SF**
cmovg/cmovnle *S, D* | Move if greater (signed) | **~(SF^0F)&~ZF**
cmovge/cmovnl *S, D* | Move if greater or equal (signed) | **~(SF^0F)**
cmovl/cmovnge *S, D* | Move if less (signed) | **SF^0F**
cmovle/cmovng *S, D* | Move if less or equal | **(SF^0F)|ZF**
cmova/cmovnbe *S, D* | Move if above (unsigned) | **~CF&~ZF**
cmovae/cmovnb *S, D* | Move if above or equal (unsigned) | **~CF**
cmovb/cmovnae *S, D* | Move if below (unsigned) | **CF**
cmovbe/cmovna  *S, D* | Move if below or equal (unsigned) | **CF** or **ZF**  


### Procedure Call Instructions

Instruction | Description 
------------|-------------
call *label* | Push return address and jump to label
call *operand* | Push return address and jump to specified location
leave | Set **%rsp** to **%rbp**, then pop top of stack to **%rbp**
ret | Pop return address from stack and jump there