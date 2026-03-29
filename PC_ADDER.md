# PC_ADDER
![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/c68398da1a734b88b9d29a6e4ca643ba0032afb8/Screenshot%202026-03-29%20145028.png
)
```verilog 
`timescale 1ns / 1ps
module PC_Adder(a,b,c);
input [31:0]a,b;
output  [31:0]c;
assign c=a+b; 
endmodule
