# Sub-Program in Verilog

📅 MAY 21, 2025  
📌 NIELIT,Calicut

## Tasks
`Code`
```verilog
`timescale 1ns / 1ps
module Task(  
    input [7:0] x,y,
    output reg [7:0] r_and,r_or,r_xor
);
    task bitwise_op(
    input [7:0] a,b,
    output [7:0] r_and, r_or, r_xor
    );
    begin
        assign r_and = a&b;
        assign r_or = a|b;
        assign r_xor = a^b;
    end
    endtask
    always @(x or y)
    begin
        bitwise_op(x,y,r_and,r_or,r_xor);
    end
endmodule
```
`TestBench`
```verilog
`timescale 1ns / 1ps
module Task_TB();
    reg [7:0] a,b;
    wire [7:0] r_and,r_or,r_xor;
    Task uut(a,b,r_and,r_or,r_xor);
    initial
    begin
        a = 8'b11001100; b = 8'b10101010; #10;
        a = 8'b11110000; b = 8'b00001111; #10;
        a = 8'b00000000; b = 8'b11111111; #10;
        a = 8'b10101010; b = 8'b01010101; #10;
        a = 8'b11111111; b = 8'b11111111; #10;
        $finish;
    end
endmodule
```
![image](images/Day8/Screenshot%202025-05-20%20110450.png)

___

## Shift Register
`Code`
```verilog
`timescale 1ns / 1ps
module shift_reg(
    input clk,serial_in,reset,
    output reg [3:0] q
    );
    reg [25:0]clk_div=0;
    wire slow_clk;
    always @(posedge clk)
    begin
        clk_div <= clk_div +1;
    end
    assign slow_clk= clk_div[25];
    always @(posedge slow_clk or posedge reset)
    begin
        if(reset)
            q<=4'b0000;
        else
            q<={q[2:0],serial_in}; //leftshift
    end
endmodule
```

___

