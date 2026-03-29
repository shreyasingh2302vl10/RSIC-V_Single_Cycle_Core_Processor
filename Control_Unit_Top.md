# ALU_CONTROL_UNIT
```verilog
`timescale 1ns / 1ps
module Control_Unit_Top(Op,RegWrite,Immsrc,ALUSrc,MemWrite,ResultSrc,
Branch,funct3,funct7,ALUcontrol);
input [6:0]Op,funct7;
input [2:0]funct3;
output RegWrite,ALUSrc,ResultSrc,Branch,MemWrite;
output [1:0]Immsrc;
output [2:0]ALUcontrol;

wire [1:0]ALUOp;

alu_decoder alupart(.ALUOp(ALUOp),.funct3(funct3),.funct7(funct7),.op(Op)
,.ALUControl(ALUControl));

main_decoder mainpart(.op(Op),.RegWrite(RegWrite),
.Memwrite(MemWrite),.ResultSrc(ResultSrc),
.ALUSrc(ALUSrc),.ImmSrc(Immsrc),.ALUOp(ALUOp),
.Branch(Branch));


endmodule
