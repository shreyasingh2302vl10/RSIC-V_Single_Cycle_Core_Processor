# PROGRAM COUNTER
![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/3c19efa4548228e96d27c01e198f2ddd4bdb390e/Screenshot%202026-03-29%20142859.png
)
```verilog
`timescale 1ns / 1ps
module P_C(PC,PC_NEXT,rst,clk); 
input [31:0]PC_NEXT;
output reg [31:0]PC;
input rst,clk;
/* this is counter ..the count  value which actually executes the program 
every clock cycle .. 
it  updates the address which is given to instruction memory ...
in every clock cycle program counter values gets updated so ... its ..instruction memory 
actually get updated 
input is actually the next instruction ...output is the current instruction
*/
always@(posedge clk or negedge rst)
begin 
if(rst==1'b0) PC<=32'd0;
else PC<=PC_NEXT;
end 
endmodule
