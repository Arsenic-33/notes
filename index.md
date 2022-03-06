# CS1S Notes (Sigma 16)
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
*Meaning:* `dest := op1 + op2`  
---
### Register R0 and R15 are special!
• **You should not use R0 or R15 to hold ordinary variables!**  
• **R0 always contains 0**  
– Any time you need the number 0, it's available in R0  
– You cannot change the value of R0  
– It is legal to use R0 as the destination, but it will still be 0 after you do it!  
– `add R0,R2,R3` ; does nothing (R0 will not change)  
•** R15 holds status information**  
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


[^1]: Each 16-bit register is 16 copies of the reg1 circuit
