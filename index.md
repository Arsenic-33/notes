#CS1S Notes (Sigma 16)
##Lecture 7 (First)
###Structure of Registers
The RTM circuit has 4 (R0, …, R3), each holding 4 bits 
There are 16 registers in Sigma16, each holding 16 bits (a
16-bit word) [^1]

###RTM Instructions
The RTM circuit can execute only two instructions
```
R2 := R1 + R0 ; add two registers and load result
R1 := 8 ; load a constant
```




[^1]: Each 16-bit register is 16 copies of the reg1 circuit
