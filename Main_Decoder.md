# Main Decoder
```verilog
`timescale 1ns / 1ps
module main_decoder(op,zero,RegWrite,Memwrite,ResultSrc,ALUSrc,ImmSrc,ALUOp,PCSrc);
input [6:0]op;
input zero;
output RegWrite,Memwrite,ResultSrc,ALUSrc,PCSrc;
output [1:0]ALUOp,ImmSrc;
//  inside wires
wire branch;
assign RegWrite= ((op ==7'b00000110)| (op== 7'b0110011))?1'b1:1'b0;
assign ALUSrc= ((op== 7'b0000011)|(op== 7'b0100011))?1'b1:1'b0;
assign branch= (op==7'b1100011)?1'b1:1'b0;
assign PCSrc= (branch&zero);
assign Memwrite=(op==7'b0100011)?1'b1:1'b0;
assign ResultSrc= (op==7'b0000011)?1'b1:1'b0;
assign ImmSrc[1]= (op==7'b1100011)?1'b1:1'b0;
assign ImmSrc[0]= (op==7'b0100011)?1'b1:1'b0;
assign ALUOp[0]= (op==7'b1100011)?1'b1:1'b0;
assign ALUOp[1]= (op==7'b0110011)?1'b1:1'b0;

endmodule```
