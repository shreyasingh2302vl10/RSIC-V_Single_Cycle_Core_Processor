# ALU DECODER
![Processor Screenshot](https://github.com/shreyasingh2302vl10/RSIC-V_Single_Cycle_Core_Processor/blob/cec7a6e704807285406621c8226769f7490d2d0a/Screenshot%202026-03-15%20003153.png
)
```verilog
`timescale 1ns / 1ps
module alu_decoder(ALUOp,op5,funct3,funct7,control);
input op5,funct7;
input [2:0]funct3;
output [1:0]ALUOp;
output [2:0]control;

wire [1:0]concatenation;
assign concatenation={op5,funct7};
assign control= (ALUOp==2'b00)? 3'b000:
                (ALUOp==2'b01)? 3'b001:
                ((ALUOp==2'b10)&(funct3==3'b010))?3'b101:
               ((ALUOp==2'b10)&(funct3==3'b110))?3'b011:
               ((ALUOp==2'b10)&(funct3==3'b111))?3'b010:
               ((ALUOp==2'b10)&(funct3==3'b000)&(concatenation==2'b11))?3'b001:
               ((ALUOp==2'b10)&(funct3==3'b000)&(concatenation!=2'b11))?3'b000:3'b000;

endmodule
```
