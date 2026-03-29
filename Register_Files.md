# Register_Files
![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/ce21d3064c074564aa7dc1a9fcd1e4074620c8a7/Screenshot%202026-03-29%20144810.png
)
```verilog
`timescale 1ns / 1ps
module Reg_files(A1,A2,A3,WD3,WE3,clk,rst,RD1,RD2);
input [4:0] A1,A2,A3;
input [31:0]WD3;
input clk,rst,WE3;
output [31:0]RD1,RD2;
// creation of the temporary memory 
reg [31:0] Registers[31:0];
assign RD1=(rst==1'b0)?32'd0:Registers[A1];

assign RD2=(rst==1'b0)?32'd0:Registers[A2];

always@(posedge clk)
begin
    if(WE3==1'b1) begin 
    Registers[A3]<=WD3;
    end
 end 
 initial begin 
 Registers[5]=32'h00000005;
 Registers[6]=32'h00000004;
 end 
endmodule
