### Comparison instruction: Boolean form  
• cmp Ra,Rb: compares the values in registers Ra and Rb, and then sets bits
(or flags) in R15 to indicate the result  
– The instruction performs both binary and two's complement comparison  
• The notation R15.i means bit i in R15 thus R15.0 is the leftmost bit of R15  
– Note that sigma16 uses “big endian” representation (when we saw
binary arithmetic it was “little endian”)  
• The resulting bits (or flags) are  
– binary less than (L) in R15.0  
– two's complement less than (<) in R15.1  
– equal in R15.2  
– binary greater than (G) in R15.3  
– two's complement greater than (>) in R15.4  