# Intro to Parameterized Design, How to Dump the verilog code to a FPGA

📅 MAY 19, 2025  
📌 NIELIT,Calicut

## Parameterized register
`Code`
```verilog
`timescale 1ns / 1ps
module para_reg #(
    parameter WIDTH = 8,
    parameter DEPTH = 4
)(
    input clk,
    input rst,
    input wen,
    input [WIDTH-1:0]D,
    output [WIDTH-1:0] Q);
    
reg [WIDTH-1:0] shift_arr[0:DEPTH-1];
integer i;
always @(posedge clk or posedge rst)
begin
    if(rst) begin
        for (i=0;i<DEPTH;i=i+1) begin
            shift_arr[i]<=D;
        end
    end 
    if(wen) begin
        shift_arr[0]<=D;
        for(i=1;i<DEPTH;i=i+1) begin
            shift_arr[i]<=shift_arr[i-1];   
        end
    end
end
assign Q=shift_arr[DEPTH-1];
endmodule
```
`Testbench`
```verilog
`timescale 1ns / 1ps

module shift_reg_tb;

    // Parameters
    parameter WIDTH = 8;
    parameter DEPTH = 4;

    // Inputs
    reg clk;
    reg rst;
    reg wen;
    reg [WIDTH-1:0] D;

    // Output
    wire [WIDTH-1:0] Q;

    // Instantiate the shift register
    para_reg #(WIDTH, DEPTH) uut (
        .clk(clk),
        .rst(rst),
        .wen(wen),
        .D(D),
        .Q(Q)
    );

    // Clock generation
    always #5 clk = ~clk;  // 100MHz clock

    // Test sequence
    initial begin
        $display("Starting shift_reg testbench...");
        clk = 0;
        rst = 1;
        wen = 0;
        D = 0;

        // Hold reset
        #10;
        rst = 0;

        // Apply test data
        wen = 1;
        D = 8'hA1; #10;
        D = 8'hB2; #10;
        D = 8'hC3; #10;
        D = 8'hD4; #10;
        D = 8'hE5; #10;

        // Disable write enable
        wen = 0; D = 8'h00; #20;

        // End simulation
        $finish;
    end

    // Monitor output
    initial begin
        $monitor("Time=%0t | clk=%b rst=%b wen=%b D=0x%h Q=0x%h", 
                  $time, clk, rst, wen, D, Q);
    end

endmodule
```
![image](images/Day6/Screenshot%202025-05-19%20105527.png)

___

## FPGA Dumping
- Used board  : Digilent Arty 7 35T
- Part number : xc7a35tcsg324-1
- Software    : Xilinx Vivado 2024.2

**FLOW**

CODE &rarr; SYNTHESIS &rarr; I/O PLANNING &rarr; IMPLEMENTATION &rarr; GENERATE BITSTREAM &rarr; HARDWARE MANAGER &rarr; PROGRAM DEIVCE

**Steps**  
  
  1. Set the correct board in the Settings page.   
  2. Add the design source file.
  3. Create an empty `.xdc` file in Constraints page.
  4. Click on the `RUN SYNTHESIS` button.
  5. After Synthesis, Open `I/O Planning` in the `Layout` column.
  6. Map the ports to the physical buttons or LED's of the FPGA using the user manual of the FPGA board.
  7. Then click `RUN IMPLEMENTATION`.
  8. Once it is done, click `GENERATE BITSTREAM`.
  9. Then click `Open Hardware Manager` and click `Autoconnect`.
  10. Once the device name appeared, right click and click `Program device`.   

  ___