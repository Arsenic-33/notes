# Sigma 16 Notes
## Lecture 7 (First)
### Structure of Registers
The RTM circuit has 4 (R0, …, R3), each holding 4 bits 
There are 16 registers in Sigma16, each holding 16 bits (a
16-bit word) [^1]  

### RTM Instructions
The RTM circuit can execute only two instructions  
```
R2 := R1 + R0 ; add two registers and load result
R1 := 8 ; load a constant
```
### Add instructions
The add instruction  
• Examples  
```
add R5,R2,R3 ; means R5 := R2 + R3
add R12,R1,R7 ; means R12 := R1 + R7
```
• General form
`add dest,op1,op2 ` *where dest, op1, op2 are registers*  
**The two operands are added, the result is placed in the destination**  
Meaning: `dest := op1 + op2`  
---------------------
### Register R0 and R15 are special!
• **You should not use R0 or R15 to hold ordinary variables!**  
• **R0 always contains 0**  
– Any time you need the number 0, it's available in R0  
– You cannot change the value of R0  
– It is legal to use R0 as the destination, but it will still be 0 after you do it!  
– `add R0,R2,R3` ; does nothing (R0 will not change)  
• ** R15 holds status information**  
– Some instructions place additional information in R15 (is the result
negative? was there an overflow?)  
– Therefore, R15 is for temporary information (not a safe place to keep
long-term data)  

### Registers and memory
• Register file  
– 16 registers (too small to hold all your variables)  
– Each register holds a 16-bit word  
– Names are R0, R1, R2, ..., R15  
– You can do arithmetic on data in the registers  
– Use registers to hold data temporarily that you're doing arithmetic on  
• Memory  
– 65,536 memory locations  
– Each memory location holds a 16-bit word  
– Each memory location has an address 0, 1, 2, …, 65,535  
– The machine cannot do arithmetic on a memory location  
– Use memory locations to store program variables and the program itself  

### Copying a word between memory and register
• There are two instructions for accessing the memory  
– load copies a variable from memory to a register  
• `load R2,x[R0]` copies the variable x from memory to register R2  
• `R2 := x`  
• R2 is changed; x is unchanged  
– store copies a variable from a register to memory  
• `store R3,y[R0]` copies the word in register R3 to variable y in memory  
• `y := R3`  
• y is changed; R3 is unchanged  

### An assignment statement in assembly language
• High-level language statement  
`x := a+b+c`  
• Assembly language  
```
load R1,a[R0] ; R1 := a
load R2,b[R0] ; R2 := b
add R3,R1,R2 ; R3 := a+b
load R4,c[R0] ; R4 := c
add R5,R3,R4 ; R5 := (a+b) + c
store R5,x[R0] ; x := a+b+c
```
• Use load to copy variables from memory to registers  
• Do arithmetic with add, sub, mul, div  
• Use store to copy result back to memory  

### A complete example program (Sigma16 assembly)  
; A minimal program that adds two integer variables  
; Execution starts at location 0, where the first instruction will be placed when the program is executed  
```
load R1,x[R0] ; R1 := x
load R2,y[R0] ; R2 := y
add R3,R1,R2 ; R3 := x + y
store R3,z[R0] ; z := x + y
trap R0,R0,R0 ; terminate

x data 23
y data 14
z data 99
```
Static variables are placed in memory after the program

[^1]: Each 16-bit register is 16 copies of the reg1 circuit


## Lecture 8 (Control Structures)
### Conditional jumps: Boolean decision
• The result of a cmp instruction can be used to control a conditional jump  
jumplt < less than  
jumple <= less than or equal  
jumpne != not equal  
jumpeq = equal  
jumpge >= greater than or equal  
jumpgt > greater than  
• Example:  
```
cmp R2,R3 ; compare R2 with R3
jumplt loop[R0] ; if R2 < R3 then goto loop
```

### if bexp then S1 else S2
```
if x<y
then { S1 }
else { S2 }
S3
```

Compiled into
```
load R1,x[R0]
load R2,y[R0]
cmp R1,R2
jumpge else[R0]
 **then part of the statement**
instructions for S1
jump done[R0]
 **else part of the statement**
else
instructions for S2
done
instructions for statement S3 
```

### while B do S
```
while i<n do
{ S1 }
S2
```
Compiled into
```
lea R1,1[R0]
load R2,i[R0]
load R3,n[R0]
loop
cmp R2,R3
jumpge done[R0]
… instructions for the loop body S1
add R2,R2,R1
jump loop[R0]
done
instructions for S2
```

### Nested statements  
• In larger programs, there will be nested statements  

```
if b1
	then { S1;
		if b2 then {S2} else {S3};
		S4;
	}
	else { S5;
		while b3 do {S6};
	}
S7
```
### How to compile nested statements  
• A block is a sequence of instructions  
– To execute it, always start with the first statement  
– When it finishes, it always reaches the last statement  
• Every high-level statement should be compiled into a block of code  
• This block may contain internal structure (several smaller blocks)  
– To execute it you should always begin at the beginning and it should
always finish at the end  
• The previous patterns work for nested statements  
• But you need to use new labels (can't have the same label in several places)  