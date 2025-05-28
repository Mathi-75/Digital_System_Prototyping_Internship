# Implementation of Parity Generator, Checker and Sequential Circuits

📅 MAY 16, 2025  
📌 NIELIT,Calicut

## Even Parity Generator
`Code`
```verilog
`timescale 1ns / 1ps
module parity_generator(
    input [0:2]I,
    output Par
    );
    assign Par = I[0] ^ I[1] ^ I[2];
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module Parity_generator_TB();
reg [0:2]I;
wire Par;
parity_generator uut(I,Par);
initial 
begin
I=3'd0;
#5 I=3'd1;
#5 I=3'd2;
#5 I=3'd3;
#5 I=3'd4;
#5 I=3'd5;
#5 I=3'd6;
#5 I=3'd7;
#5 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20102029.png)

___

## Odd Parity Generator
`Code`
```verilog
`timescale 1ns / 1ps
module odd_parity(
    input [0:2] I,
    output par
    );
    assign par = ~(I[0] ^ I[1] ^ I[2]);
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module odd_parity_tb();
reg [0:2]I;
wire Par;
odd_parity uut(I,Par);
initial
begin
I=3'd0;
#5 I=3'd1;
#5 I=3'd2;
#5 I=3'd3;
#5 I=3'd4;
#5 I=3'd5;
#5 I=3'd6;
#5 I=3'd7;
#5 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20102956.png)

___

## Even Parity Checker
`Code`
```verilog
`timescale 1ns / 1ps
module even_parity_checker(
    input [0:2] I,
    input P,
    output Err
    );
    assign Err =  I[0]^I[1]^I[2]^P;
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module parity_checker_tb();
reg [0:2]I;
reg P;
wire Err;
even_parity_checker uut(I,P,Err);
initial
begin
I=3'd0; P=0;
#5 I=3'd0; P=1;
#5 I=3'd1; P=0;
#5 I=3'd1; P=1;
#5 I=3'd2; P=0;
#5 I=3'd2; P=1;
#5 I=3'd3; P=0;
#5 I=3'd3; P=1;
#5 I=3'd4; P=0;
#5 I=3'd4; P=1;
#5 I=3'd5; P=0;
#5 I=3'd5; P=1;
#5 I=3'd6; P=0;
#5 I=3'd6; P=1;
#5 I=3'd7; P=0;
#5 I=3'd7; P=1;
#5 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20103814.png)

___

## D LATCH
`code`
```verilog
`timescale 1ns / 1ps
module D_Latch(
    input clk,
    input D,
    output reg Y
    );
    always @(clk)
    begin
    if(clk)
    Y<=D;
    else
    Y<=Y;
    end
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module D_Latch_TB();
reg clk,D;
wire Y;
D_Latch uut(clk,D,Y);
initial
begin
clk=0; D=1;
#5 clk=1; D=0;
#5 clk=0; D=1;
#5 clk=1; D=1;
#5 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20142054.png)

___

## D - Flip Flop
`Code`
```verilog
`timescale 1ns / 1ps
module D_FF(
    input clk,
    input D,
    output reg Y
    );
    always @(posedge clk)
    begin
    Y<=D;
    end
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module D_FF_TB();
reg clk,D;
wire Y;
D_FF uut(clk,D,Y);
initial
begin
clk=1; D=1;
#5 clk=0; D=0;
#5 clk=1; D=0;
#5 clk=0; D=1;
#5 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20142658.png)

___

## SR Flip Flop
`Code`
```verilog
`timescale 1ns / 1ps
module S_FF(
    input clk,
    input S,
    input R,
    output reg Q,
    output Qbar
    );
    assign Qbar=~Q;
    always @(posedge clk)
    begin
    case ({S,R})
    2'b00: Q<=Q;
    2'b01: Q<=0;
    2'b10: Q<=1;
    2'b11: Q<=1'bx;    
    endcase
    end
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module S_FF_TB();
reg clk,S,R;
wire Q;
S_FF uut(clk,S,R,Q,Qbar);
initial
begin
clk=0;S=0; R=0; clk=0;
#5 S=1; R=0;
#5 S=0; R=1;
#5 S=0; R=0;
#5 S=1; R=1;
#5 S=1; R=1;
#5 $finish;
end
always #5 clk=~clk;

endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20144155.png)

___

## JK Flip Flop
`Code`
```verilog
`timescale 1ns / 1ps
module JK_FF(
    input clk,
    input J,
    input K,
    output reg Q,
    output Qbar
    );
    assign Qbar =~Q;
    always @(posedge clk)
    begin
    case ({J,K})
    2'b00: Q<=Q;
    2'b01: Q<=0;
    2'b10: Q<=1;
    2'b11: Q<=~Q;
    endcase
    end
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module JK_FF_TB();
reg clk,J,K;
wire Q,Qbar;
JK_FF uut(clk,J,K,Q,Qbar);
initial
begin
clk=0; J=0; K=0;
#5 J=0; K =1;
#10 J=0; K =0;
#10 J= 1; K=1;
#10 J=1; K=0;
#5 $finish;
end
always #5 clk=~clk;
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20150330.png)

___
