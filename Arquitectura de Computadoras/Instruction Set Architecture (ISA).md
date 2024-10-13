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
