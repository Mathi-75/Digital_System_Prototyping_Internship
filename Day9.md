# Mini Projects

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

## Mini-Project: Car Parking Occupied Slot Counting system
Our last real-life problem is as follows. There is a car park with three slots and we would like to know how many of its slots are occupied at a given time. Within the design, occupied slot locations are not important. We can design a combinational circuit for this purpose. Assume that we placed a sensor over each slot which gives output logic level 1 when the slot is occupied. If the slot is empty, sensor gives output logic level 0. Let’s label output of sensors as binary variables s0, s1, and s2. The designed combinational circuit will provide the output as a two-bit binary number c1 (MSB) and c0 (LSB). Therefore, we should cover all input combinations in terms of a truth table.
![alt text](image.png)

`Code`
```verilog
`timescale 1ns / 1ps
module car_park(
    input [2:0] s,
    output [1:0] c
    );
    assign c[1]=(s[0]&s[1])||(s[0]&s[2])||(s[1]&s[2]);
    assign c[0]=s[0]^s[1]^s[2];
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module car_park_tb();
reg [2:0]s;
wire [1:0]c;
car_park uut(s,c);
initial
begin
s=3'd0;
#10 s=3'd1;
#10 s=3'd2;
#10 s=3'd3;
#10 s=3'd4;
#10 s=3'd5;
#10 s=3'd6;
#10 s=3'd7;
#10 $finish;
end
endmodule
```
![image](images/Day5/Screenshot%202025-05-16%20114516.png)

___

