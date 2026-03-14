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

assign o=(~control[1]) & (a[31]^sum[31]) & (~(control[0]^a[31]^b[31]));// overflow flag 

//Zero extension
assign e={{31{1'b0}},sum[31]};
endmodule```
