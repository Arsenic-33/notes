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
```
add dest,op1,op2 *where dest, op1, op2 are registers*
**The two operands are added, the result is placed in the destination**
*Meaning:* dest := op1 + op2
```



[^1]: Each 16-bit register is 16 copies of the reg1 circuit
