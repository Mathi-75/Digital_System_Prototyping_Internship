# Implementation of Combinational Circuits and Mini Project

📅 MAY 15, 2025  
📌 NIELIT,Calicut

## 8x3 Encoder
`Code`
```verilog
module Encoder_8x1(
input [0:7]I,
output [0:2]Y);
assign Y[0]=I[4]+I[5]+I[6]+I[7];
assign Y[1]=I[2]+I[3]+I[6]+I[7];
assign Y[2]=I[1]+I[3]+I[5]+I[7];
endmodule
```
`Testbench`
```verilog
module Encoder_8x1_TB();
reg [0:7]i;
wire [0:2]y;
Encoder_8x1 uut(.I(i),.Y(y));
initial
begin
i=8'd128;
#5 i=8'd64;
#5 i=8'd32;
#5 i=8'd16;
#5 i=8'd8;
#5 i=8'd4;
#5 i=8'd2;
#5 i=8'd1;
#5 $finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20104106.png)

___

## 8x3 Priority Encoder
`Code`
```verilog
`timescale 1ns / 1ps
module Priority_encoder_8x3(
input [0:7]I,
output [0:2]Y);
assign Y[0]=I[4]+I[5]+I[6]+I[7];
assign Y[1]=I[6]+I[7]+((~I[5])&(~I[4])&(I[3]+I[2]));
assign Y[2]=I[7]+(~I[6]&I[5])+(~I[6]&~I[5]&~I[4]&~I[3]&I[1]);
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps
module Priority_encoder_8x3_TB();
reg [0:7]I;
wire [0:2]Y;
Priority_encoder_8x3 uut(I,Y);
initial
begin
I=8'd2;
#10 I=8'd0;
#10 I=8'd3;
#10 $finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20110803.png)

___

## 2x4 Decoder
`Code`
```verilog
`timescale 1ns / 1ps
module Decoder_2x4(
input [0:1]I,
output [0:3]Y);
assign Y[0]=~I[0]&~I[1];
assign Y[1]=~I[0]&I[1];
assign Y[2]=I[0]&~I[1];
assign Y[3]=I[0]&I[1];
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps
module Decoder_2x4_TB();
reg [0:1]I;
wire [0:3]Y;
Decoder_2x4 uut(I,Y);
initial
begin
I=0; #10;
I=1; #10;
I=2; #10;
I=3; #10;
$finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20112851.png)

___

## 7-Segment Display
`Code`
```verilog
`timescale 1ns / 1ps
module seven_segment(
    input [3:0] I,
    output reg [6:0]Y);
always @(I,Y)
begin
case(I)
4'd0 : Y=7'b1111110;
4'd1 : Y=7'b0110000;
4'd2 : Y=7'b1101101;
4'd3 : Y=7'b1111001;
4'd4 : Y=7'b0100111;
4'd5 : Y=7'b1011011;
4'd6 : Y=7'b1011111;
4'd7 : Y=7'b1110000;
4'd8 : Y=7'b1111111;
4'd9 : Y=7'b1111011;
default : Y=7'bx;
endcase
end
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps
module seven_segment_TB();
reg [3:0]I;
wire [6:0]Y;
seven_segment uut(I,Y);
initial 
begin
I=4'd0;
#5 I=4'd1;
#5 I=4'd2;
#5 I=4'd3;
#5 I=4'd4;
#5 I=4'd5;
#5 I=4'd6;
#5 I=4'd7;
#5 I=4'd8;
#5 I=4'd9;
#5 $finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20120133.png)

___

## 16x1 Mux using 4x1 Mux
`Code`
```verilog
`timescale 1ns / 1ps
module Mux_16x1(
input [0:15] I,
input [0:3] S,
output Y);
wire w1,w2,w3,w4;
Mux_4_1 M1(I[0],I[1],I[2],I[3],S[0:1],w1);
Mux_4_1 M2(I[4],I[5],I[6],I[7],S[0:1],w2);
Mux_4_1 M3(I[8],I[9],I[10],I[11],S[0:1],w3);
Mux_4_1 M4(I[12],I[13],I[14],I[15],S[0:1],w4);
Mux_4_1 M5(w1,w2,w3,w4,S[2:3],Y);
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps
module Mux_16x1_TB();
reg [0:15]I;
reg [0:3]S;
wire Y;
Mux_16x1 uut(I,S,Y);
initial
begin
I=16'd32768; S=4'd0;
#5 I=16'd16384; S=4'd1;
#5 I=16'd8192; S=4'd2;
#5 I=16'd4096; S=4'd3;
#5 I=16'd2048; S=4'd4;
#5 I=16'd1024; S=4'd5;
#5 I=16'd512; S=4'd6;
#5 I=16'd256; S=4'd7;
#5 I=16'd128; S=4'd8;
#5 I=16'd64; S=4'd9;
#5 I=16'd32; S=4'd10;
#5 I=16'd16; S=4'd11;
#5 I=16'd8; S=4'd12;
#5 I=16'd4; S=4'd13;
#5 I=16'd2; S=4'd14;
#5 I=16'd1; S=4'd15;
#5 $finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20145020.png)

___

## Digital Safe System
`Code`
```verilog
`timescale 1ns / 1ps
module Digital_Safe_System(
input [0:3]p,
output I);
wire [0:3]s;
assign s= 4'b1011;      //predefined password
xnor G1(w1,s[0],p[0]);
xnor G2(w2,s[1],p[1]);
xnor G3(w3,s[2],p[2]);
xnor G4(w4,s[3],p[3]);
and G5(I,w1,w2,w3,w4);
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps
module Digital_Safe_System_TB();
reg [0:3]p;
wire I;
Digital_Safe_System uut(p,I);
initial
begin
p=4'b1011;
#10 p=4'b0000;
#10 p=4'b1111;
#10 $finish;
end
endmodule
```
![image](images/Day4/Screenshot%202025-05-15%20151856.png)

___

