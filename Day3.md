# Implementation of Combinational Circuits in Vivado and Simulating using TestBench

📅 MAY 14, 2025  
📌 NIELIT,Calicut

## HALF ADDER
`Code`
```verilog
module Half_Adder(
input a,b,
output sum,cout);
assign sum = a^b;
assign cout = a&b;
endmodule
```
`Testbench`
```verilog
module Half_Adder_tb();
reg A,B;
wire Sum,Cout;
Half_Adder dut(.a(A),.b(B),.sum(Sum),.cout(Cout));
initial 
begin
$monitor("Time=%g,A=%d,B=%d,Sum=%d,Cout=%d",$time, A,B,Sum,Cout);
end
initial
begin
#5 A=0;B=0;
#5 A=0;B=1;
#5 A=1;B=0;
#5 A=1;B=1;
end
endmodule
```
![image](images/Day3/Screenshot%202025-05-14%20140549.png)

___

## FULL ADDER
`Code`
```verilog
module Full_Adder(
input a,b,c,
output sum,cout);
wire sum1,c1,c2;
Half_Adder ha1(a,b,sum1,c1);
Half_Adder ha2(sum1,c,sum,c2);
assign cout = c1 | c2;
endmodule
```
`Testbench`
```verilog
module FULL_ADDER_TB();
reg A,B,C;
wire sum,cout;
Full_Adder uut(A,B,C,sum,cout);
initial
begin
A=0;B=0;C=0;
#5 A=0;B=0;C=1;
#5 A=0;B=1;C=0;
#5 A=0;B=1;C=1;
#5 A=1;B=0;C=0;
#5 A=1;B=0;C=1;
#5 A=1;B=1;C=0;
#5 A=1;B=1;C=1;
end
endmodule
```
![image](images/Day3/Screenshot%202025-05-14%20144144.png)

___

## Ripple Carry Adder
`Code`
```verilog
module Ripple_Carry_Adder(
input [3:0]a,b,
input cin,
output [3:0]sum,
output cout);
wire c1,c2,c3;
Full_Adder fa0(a[0],b[0],cin,sum[0],c1);
Full_Adder fa1(a[1],b[1],c1,sum[1],c2);
Full_Adder fa2(a[2],b[2],c2,sum[2],c3);
Full_Adder fa3(a[3],b[3],c3,sum[3],cout);
endmodule
```
`Testbench`
```verilog
module Ripple_Carry_Adder_tb();
reg [3:0]a,b;
reg cin;
wire [3:0]sum;
wire cout;

Ripple_Carry_Adder uut(a,b,cin,sum,cout);

initial
begin
a= 4'd0;b=4'd0;cin=0;
# 10 a= 4'd1;b=4'd8;cin=0;
# 10 a= 4'd2;b=4'd7;cin=0;
# 10 a= 4'd3;b=4'd6;cin=0;
# 10 a= 4'd4;b=4'd5;cin=0;
# 10 a= 4'd5;b=4'd4;cin=0;
# 10 a= 4'd6;b=4'd3;cin=0;
# 10 a= 4'd7;b=4'd2;cin=0;
# 10 a= 4'd8;b=4'd1;cin=0;
end
endmodule
```
![image](images/Day3/Screenshot%202025-05-14%20145350.png)
___

## HALF SUBTRACTOR
`Code`
```verilog
module Half_Subtracter(
input a,b,
output diff,bor);
assign diff = a^b;
assign bor = (~a)&b;
endmodule
```
`TestBench`
```verilog
module Half_Subtracter_TB();
reg a,b;
wire diff,bor;
Half_Subtracter uut(a,b,diff,bor);
initial 
begin
a=0;b=0;
#10 a=0;b=1;
#10 a=1;b=0;
#10 a=1;b=1;
end
endmodule
```

![image](images/Day3/Screenshot%202025-05-14%20150311.png)

___

## FULL SUBTRACTOR
`Code`
```verilog
module Full_Subtractor(
input a,b,bin,
output diff,bor);

wire diff1,b1,b2;
Half_Subtracter ha1(a,b,diff1,b1);
Half_Subtracter ha2(diff1,bin,diff,b2);
assign borr = b1 | b2 ;
endmodule
```
`TestBench`
```verilog
module Full_Subtractor_TB();
reg a,b,c;
wire diff,bor;

Full_Subtractor uut(a,b,c,diff,bor);
initial
begin
a=0;b=0;c=0;
#100 a=0;b=0;c=1;
#100 a=0;b=1;c=0;
#100 a=0;b=1;c=1;
#100 a=1;b=0;c=0;
#100 a=1;b=0;c=1;
#100 a=1;b=1;c=0;
#100 a=1;b=1;c=1;
#100 $finish;
end
endmodule
```
![image](images/Day3/Screenshot%202025-05-14%20151454.png)

___
