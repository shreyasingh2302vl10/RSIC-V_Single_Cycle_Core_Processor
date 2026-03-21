![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/8b0adca9bbece5af2cdf849c8f17d99a7194ecb9/Screenshot%202026-03-14%20141601.png)

# ALU
```verilog
`timescale 1ns / 1ps
module alu(y,a,b,control,n,z,o,c,e);
// inputs 
input [31:0]a,b;
input [2:0]control;
// outputs 
output [31:0]y;
output n,z,o,c;
output [31:0]e;
// wires 
wire [31:0] a_and_b;
wire [31:0] a_or_b;
wire[31:0] not_b;
wire [31:0] mux_l;
wire [31:0]sum;
wire carry;
// not 
assign not_b=~b;
// or 
assign a_or_b=a|b;
// and 
assign a_and_b=a&b;
// for subtraction
assign mux_l=(control[0]==1'b0)?b:not_b;
assign {carry,sum}=a+mux_l+control[0];
//result 
assign y=(control[2:0]==3'b000)?sum:
(control[2:0]==3'b001)?sum:
 (control[2:0]==3'b010)?a_and_b:
(control[2:0]==3'b011)?a_or_b:
(control[2:0]==3'b101)?e:32'd0;


assign z=&(~y);

assign n=y[31];

assign c=carry&(~control[1]);

//Result ka “reference” operand = a  hai ... 
// CASE 1: ADD → (+ + → -) 
//Inputs:
//control[0] = 0 (ADD)
//a[31] = 0
//b[31] = 0
//sum[31] = 1   (wrong)
//Check:
//~control[1] = 1 
//(a[31]^sum[31]) = 0^1 = 1  (sign flipped)
//~(0 ^ 0 ^ 0) = ~(0) = 1  (same sign inputs)
// Final:
//o = 1 → overflow 
//CASE 2: ADD → (- - → +) 
//Inputs:
//control[0] = 0
//a[31] = 1
//b[31] = 1
//sum[31] = 0   (wrong)
//Check:
//~control[1] = 1 
//(1^0) = 1 
//~(0 ^ 1 ^ 1) = ~(0) = 1 
//Final:
//o = 1 → overflow 
//CASE 3: SUB → (+ - → -) 
//Inputs:
//control[0] = 1 (SUB)
//a[31] = 0
//b[31] = 1
//sum[31] = 1   (wrong)
//Check:
//~control[1] = 1 
//(0^1) = 1 
//~(1 ^ 0 ^ 1) = ~(0) = 1  (different signs)
// Final:
//o = 1 → overflow 
//CASE 4: SUB → (- + → +) 
//Inputs:
/*control[0] = 1
a[31] = 1
b[31] = 0
sum[31] = 0   (wrong)
Check:
~control[1] = 1 
(1^0) = 1 
~(1 ^ 1 ^ 0) = ~(0) = 1 
 Final:
o = 1 → overflow 
 Why this works (simple English)
Yeh code 3 cheezein ensure karta hai:

1. Operation correct hai
~control[1]
2. Result ka sign galat hai
(a[31]^sum[31])
3. Yeh woh case hai jahan overflow ho sakta hai
~(control[0]^a[31]^b[31])
ADD → same sign inputs
SUB → different sign inputs*/


assign o=(~control[1]) & (a[31]^sum[31]) & (~(control[0]^a[31]^b[31]));// overflow flag 

//Zero extension
assign e={{31{1'b0}},sum[31]};
endmodule
