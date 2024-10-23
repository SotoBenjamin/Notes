The words in a computer's language are called instructions. The computer vocabulary is called *instruction set* . All programs running in a computer use the same instruction set.
# Computer functions and Components
### 1. Data Processing
### 2. Data Storage
### 3. Data Movement
	-Input
	 -Output
### 4. Control
	A control unit manages the computer's in response to instructions

# Computer Architecture Models
## .Von Neumann
	-Single Area of Memorie for program instructions and the data
## .Harvard
	-Complete separation of code and data memory regions.
## .Modified Harvard
	-Some degree of separation between program instructions and data
	-Modern Procesors

# Von Neumann Model
Has 5 parts: Memory,Processing Unit, Input, Output and Control Unit
## Memory
+ Memory stores:
	+  Data
	+  Programs(instructions)
+ The memory contains bits
	+ Bits are grouped into bytes(8 bits)
+ How the bits are accessed determines the **addressability** 
	+ word addressable
	+ byte addressable
 + The total number of addresses in the address space
	+ In ARM, the address space is $2^{32}$
	+ In x86-64, the address space is $2^{48}$
+ There are two ways of access memory 
	+ Reading or loading 
	+ Writing or storing
+ Two registers are necessary to access memory
	+ Memory Address Register (MAR)
	+ Memory Data Register (MDR)
+ Word Addressable Memory   [[06-ArchT-Instruction Set Architecture.pdf#page=19&selection=0,0,0,23&color=yellow|06-Arch-Instruction Set Architecture, p.19]]
+ Byte Addressable Memory [[06-ArchT-Instruction Set Architecture.pdf#search=Byte-Addressable Memory|06-Arch T-Instruction Set Architecture, p.20]]
	+ ARM is Byte Addressable
+ Little-endian: byte numbers start at the little (least significant) end 
	
+  Big-endian: byte numbers start at the big (most significant) end
+  [[06-ArchT-Instruction Set Architecture.pdf#page=22&annotation=201R|06-ArchT-Instruction Set Architecture, p.22]]
## Processing Unit
+ The processing unit can consists of many functional Units like [[ALU]]
+ ALU executes instructions like (in ARM) : add,sub,mul,nor,etc...
+ It has temporary storage named **registers** commonly used in intermediate results
+ **Registers** are faster than memory, In ARM exist 16 registers.
+ **Registers** have 32 bits
+ **Registers** named with R and a number, E.g.: "R0" is the register zero
+ Used specific purposes registers : 
	+ **Saved Registers:**  R4 - R11
	+ **Temporary Registers:** R0 - R3 and R12
	+ For more detail : [[06-ArchT-Instruction Set Architecture.pdf#page=25&annotation=204R|06-ArchT-Instruction Set Architecture, p.25]]
	+ [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=325&annotation=7530R|Digital Design and Computer Arc - Sarah L. Harris, p.300]] Table 6.1 ARM register
## Input and Output
[[06-ArchT-Instruction Set Architecture.pdf#page=26&annotation=212R|06-ArchT-Instruction Set Architecture, p.26]]I
## Control Unit
+ Conduces the processing of execution the instructions (step by step)
+ Keeps track of the instruction being executed with an instruction register (IR), which contains the instruction
+ The register Program Counter (PC) contain the address of the next instruction to execute
## Assembly Language
### Instructions
#### Addition
```assembly
;R0=a,R1=b,R2=c
ADD R0,R1,R2 ; a = b + c
```
### Subtraction

```assembly 
;R0=a,R1=b,R2=c
SUB R0,R1,R2 ; a = b - c
```

Obs : Instruction RSB is using for reverse subtract
```assembly 
;R0=a,R1=b
RSB R0,R1,#0 ; a = 0 - b;
```
### Logical Instructions
The logical instructions are AND, ORR,EOR,BIC,MVN

![[Pasted image 20241005215055.png]]
[[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=329&annotation=7533R|Digital Design and Computer Arc - Sarah L. Harris, p.304]]Figure 6.3 Logical operations
### Shift Instructions
The shift instructions shift the bits to left o right dropping the bits of the end
ARM shift operations are LSL , LSR , ASR and ROR
![[Pasted image 20241006110732.png]]
> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=330&annotation=7536R|Digital Design and Computer Arc - Sarah L. Harris, p.305]]
> > Shifting a value left by N is equivalent to multiplying it by $2^{n}$. Likewise, arithmetically shifting a value right by N is equivalent to dividing it by $2^{n}$ ,  as discussed in Section 5.2.5. Logical shifts are also used to extract or assemble bitfields.
> 

### Conditional Flags
Are used to change the flow execution of a program, these flags are set by the [[ALU]]  and are head in the top 4 bits of the Current Program Status Register
![[Pasted image 20241006112553.png]]
> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=331&annotation=7554R|Digital Design and Computer Arc - Sarah L. Harris, p.306]]
> > The ARM condition flags, also called status flags, are negative (N), zero (Z), carry (C), and overflow (V), as listed in Table 6.2. 
> 
> 

![[Pasted image 20241006112826.png]]
> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=331&annotation=7557R|Digital Design and Computer Arc - Sarah L. Harris, p.306]]
> > The most common way to set the status bits is with the compare (CMP) instruction, which subtracts the second source operand from the first and sets the condition flags based on the result. For example, if the numbers are equal, the result will be zero and the Z flag is set. If the first number is an unsigned value that is higher than or the same as the second, the subtraction will produce a carry out and the C flag is set.

> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=331&annotation=7565R|Digital Design and Computer Arc - Sarah L. Harris, p.306]]
> > For example, suppose a program performs CMP R4, R5, and then ADDEQ R1, R2, R3. The compare sets the Z flag if R4 and R5 are equal, and the ADDEQ executes only if the Z flag is set.
> 
> 


![[Pasted image 20241006114121.png]]
> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=332&annotation=7573R|Digital Design and Computer Arc - Sarah L. Harris, p.307]]
> > Other data-processing instructions will set the condition flags when the instruction mnemonic is followed by “S.” For example, SUBS R2, R3, R7 will subtract R7 from R3, put the result in R2, and set the condition flags. Table B.5 in Appendix B summarizes which condition flags are influenced by each instruction. All data-processing instructions will affect the N and Z flags based on whether the result is zero or has the most significant bit set. ADDS and SUBS also influence V and C, and shifts influence C.

> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=332&selection=42,0,42,18|Digital Design and Computer Arc - Sarah L. Harris, p.307]]
> > Code Example 6.10 

### Branching
> [!PDF|255, 208, 0] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=333&annotation=7586R|Digital Design and Computer Arc - Sarah L. Harris, p.308]]
> > A program usually executes in sequence, with the program counter (PC) incrementing by 4 after each instruction to point to the next instruction. (Recall that instructions are 4 bytes long and ARM is a byteaddressed architecture.) Branch instructions change the program counter. ARM includes two types of branches: a simple branch (B) and branch and link (BL). BL is used for function calls.
> > 

Branches can be conditional or unconditional and uses to implement loops and conditionals
```assembly
;Unconditional Branch
	ADD R1,R2,#17 
	B TARGET
	ORR R1,R1,R3 ;not execute
	AND R3,R1,#0XFF;not execute
TARGET
SUB R1,R1,#78
```

```assembly
;Conditional Branch
	MOV R0,#4    ;R0=4
	ADD R1,R0,R0 ;R1=8;
	CMP R0,R1       
	BEQ THERE  
	ORR R1,R1,#1 R1 = 9  
THERE
	ADD R1,R1,#78  R1 = 87
```
#### if-else statements and switch case
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=336&selection=65,0,65,17|Digital Design and Computer Arc - Sarah L. Harris, p.311]]
> > IF/ELSE STATEMENT

#### loops (for and while)
##### while:
```assembly
;R0 = pow, R1 = x
MOV R0,#1 ; pow = 1
MOV R1,#0 ; x = 0
WHILE:
 cmp R0,#128
 BEQ DONE
 LSL R0,R0,#1
 ADD R1,R1,#1
 B WHILE
DONE:
	

```
##### for:
```assembly
;R0 = i , R1 = s

MOV,R0,#0
MOV R1,#0

FOR:
	CMP R0,#10
	BGE DONE
	ADD R1,R1,R0
	ADD R0,R0,#1
	B FOR
DONE: 	

```

### Memory
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=339&selection=53,0,54,1|Digital Design and Computer Arc - Sarah L. Harris, p.314]]
> > Code Example 6.18 

![[Captura de pantalla 2024-10-19 a la(s) 7.55.33 p. m..png]]
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=338&selection=51,0,66,24|Digital Design and Computer Arc - Sarah L. Harris, p.313]]
> > ARM can scale (multiply) the index, add it to the base address, and load from memory in a single instruction. Instead of the LSL and LDR instruction sequence in Code Example 6.18, we can use a single instruction: LDR R3, [R0, R1, LSL #2]

> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=339&selection=0,0,75,2|Digital Design and Computer Arc - Sarah L. Harris, p.314]]
> > In addition to scaling the index register, ARM provides offset, preindexed, and post-indexed addressing to enable dense and efficient code for array accesses and function calls. Table 6.4 gives examples of each indexing mode. In each case, the base register is R1 and the offset is R2. The offset can be subtracted by writing –R2. The offset may also be an immediate in the range of 0–4095 that can be added (e.g., #20) or subtracted (e.g., #−20). Offset addressing calculates the address as the base register ± the offset; the base register is unchanged. Pre-indexed addressing calculates the address as the base register ± the offset and updates the base register to this new address. Post-indexed addressing calculates the address as the base register only and then, after accessing memory, the base register is updated to the base register ± the offset. We have seen many examples of offset indexing mode. Code Example 6.19 shows the for loop from Code Example 6.18 rewritten to use post-indexing, eliminating the ADD to increment i.
> 


![[Captura de pantalla 2024-10-19 a la(s) 8.05.41 p. m..png]]
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=340&selection=108,0,109,1|Digital Design and Computer Arc - Sarah L. Harris, p.315]]
> > Code Example 6.19 

### Bytes And Memory

> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=340&selection=85,0,106,74|Digital Design and Computer Arc - Sarah L. Harris, p.315]]
> > ARM provides load byte (LDRB), load signed byte (LDRSB), and store byte (STRB) to access individual bytes in memory. LDRB zero-extends the byte, whereas LDRSB sign-extends the byte to fill the entire 32-bit register. STRB stores the least significant byte of the 32-bit register into the specified byte address in memory. All three are illustrated in Figure 6.9, with the base address R4 being 0. LDRB loads the byte at memory address 2 into the least significant byte of R1 and fills the remaining register bits with 0. LDRSB loads this byte into R2 and sign-extends the byte into the upper 24 bits of the register. STRB stores the least significant byte of R3 (0x9B) into memory byte 3; it replaces 0xF7 with 0x9B. The more significant bytes of R3 are ignored.

![[Captura de pantalla 2024-10-20 a la(s) 7.29.49 a. m..png]]
![[Captura de pantalla 2024-10-20 a la(s) 7.32.30 a. m..png]]

> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=341&selection=18,0,31,67|Digital Design and Computer Arc - Sarah L. Harris, p.316]]
> > A series of characters is called a string. Strings have a variable length, so programming languages must provide a way to determine the length or end of the string. In C, the null character (0x00) signifies the end of a string. For example, Figure 6.10 shows the string “Hello!” (0x48 65 6C 6C 6F 21 00) stored in memory. The string is seven bytes long and extends from address 0x1522FFF0 to 0x1522FFF6. The first character of the string (H = 0x48) is stored at the lowest byte address (0x1522FFF0).

![[Captura de pantalla 2024-10-20 a la(s) 7.39.18 a. m..png]]
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=342&selection=69,0,79,27|Digital Design and Computer Arc - Sarah L. Harris, p.317]]
> > Example 6.2 USING LDRB AND STRB TO ACCESS A CHARACTER ARRAY

### Function Calls
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=342&selection=56,0,67,35|Digital Design and Computer Arc - Sarah L. Harris, p.317]]
> > When one function calls another, the calling function, the caller, and the called function, the callee, must agree on where to put the arguments and the return value. In ARM, the caller conventionally places up to four arguments in registers R0–R3 before making the function call, and the callee places the return value in register R0 before finishing. By following this convention, both functions know where to find the arguments and return value, even if the caller and callee were written by different people. The callee must not interfere with the behavior of the caller. This means that the callee must know where to return to after it completes and it must not trample on any registers or memory needed by the caller. The caller stores the return address in the link register LR at the same time it jumps to the callee using the branch and link instruction (BL). The callee must not overwrite any architectural state or memory that the caller is depending on. Specifically, the callee must leave the saved registers (R4–R11, and LR) and the stack, a portion of memory used for temporary variables, unmodified. This section shows how to call and return from a function. It shows how functions access input arguments and the return value and how they use the stack to store temporary variables.
> > 

> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=350&selection=108,0,110,21|Digital Design and Computer Arc - Sarah L. Harris, p.325]]
> > Code Example 6.26 NONLEAF FUNCTION CALL

#### Recursive Function Call
```
.global _start
_start:
	MOV R0,#3
	BL FACTORIAL
	B _end

FACTORIAL:
	PUSH {R0,LR}
	CMP R0,#1
	BGT ELSE
	MOV R0,#1
	ADD SP,SP,#8
	MOV PC,LR
ELSE:
	SUB R0,R0,#1
	BL FACTORIAL
	POP {R1,LR}
	MUL R0,R0,R1
	MOV PC,LR
```
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=352&selection=65,0,65,17|Digital Design and Computer Arc - Sarah L. Harris, p.327]]
> > Code Example 6.27

![[Captura de pantalla 2024-10-20 a la(s) 1.22.42 p. m..png]]
### Machine Code
Main Instructions format:
- Data Processing
- Memory
- Branch
#### Data Processing
The 32-bit instruction has six fields cond, op, funct, Rn, Rd, Scr2
![[Captura de pantalla 2024-10-20 a la(s) 10.09.41 p. m..png]]
op: operation code (00) for data processing , funct: function code , cond : conditional execution 
(1110) for unconditional. The operands are Rn (first source) , Rd (destiny) , Src2 (second source)
Scr2 can be an immediate or a register
> [!PDF|] [[Digital Design and Computer Arc - Sarah L. Harris.pdf#page=355&selection=56,1,147,27|Digital Design and Computer Arc - Sarah L. Harris, p.330]]
> > Figure 6.17 shows the format of the funct field and the three variations of Src2 for data-processing instructions. funct has three subfields: I, cmd, and S. The I-bit is 1 when Src2 is an immediate. The S-bit is 1 when the instruction sets the condition flags. For example, SUBS R1, R9, #11 has S = 1. cmd indicates the specific data-processing instruction, as given in Table B.1 in Appendix B. For example, cmd is 4 (0100 2) for ADD and 2 (0010 2 ) for SUB. Three variations of Src2 encoding allow the second source operand to be (1) an immediate, (2) a register (Rm) optionally shifted by a constant (shamt5), or (3) a register (Rm) shifted by another register (Rs). For the latter two encodings of Src2, sh encodes the type of shift to perform, as will be shown in Table 6.8.

![[Captura de pantalla 2024-10-20 a la(s) 10.23.11 p. m..png]]
![[Captura de pantalla 2024-10-20 a la(s) 10.46.29 p. m..png]]
![[Captura de pantalla 2024-10-20 a la(s) 10.50.36 p. m..png]]
