# Instruction Memory
![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/7722623bffc791ca515b7f24b8badd64903e65ee/Screenshot%202026-03-29%20143234.png
)
```verilog
`timescale 1ns / 1ps
module Instr_Mem(A,rst,RD);
input [31:0]A;
input rst;
output [31:0]RD;
/*we talk instruction memory with the help of register 
memory is a stack of register ...in that register we save machine code register 
instruction memory input is address and it get updated .. by every clock ... 

*/
reg [31:0]Mem[1023:0];// it has ..1024 register and each register has ... 32 size 

assign RD= (rst==1'b0)?32'd0:Mem[A[31:2]];

initial begin 
Mem[0]=32'hFFC4A303;
end 
endmodule
