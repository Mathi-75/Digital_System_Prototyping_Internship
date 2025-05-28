# Designing of Counters

📅 MAY 12, 2025  
📌 NIELIT,Calicut

## Upcounter 
`Code`
```verilog
`timescale 1ns / 1ps
module UP_COUNTER_SYN(
input clk,reset,
output reg [3:0] count
);
reg [25:0] clk_divider = 0;
wire slow_clk;
always @(posedge clk)
begin
clk_divider <= clk_divider+1;
end

assign slow_clk = clk_divider[25];

always @(posedge slow_clk or posedge reset) begin
if (reset)
count<=4'b0000;
else
count<= count+1;
end
endmodule
```

___

## Downcounter
`Code`
```verilog
`timescale 1ns / 1ps
module downcounter_4(
    input clk,reset,
    output reg [3:0] count
    );
    reg [25:0] clk_div=0;
    wire slow_clk;
    always @(posedge clk)
    begin
    clk_div <= clk_div +1;
    end
    assign slow_clk=clk_div[25];
    always @(posedge slow_clk or posedge reset)
    begin
    if(reset)
    count<=4'b1111;
    else
    count<=count-1;
    end
endmodule
```

___

## Ring Counter
`Code`
```verilog
`timescale 1ns / 1ps
module ringcounter_4(
    input clk,reset,
    output reg [3:0] count
    );
    reg [25:0]clk_div=0;
    wire slow_clk;
    always @(posedge clk)
    begin
    clk_div <= clk_div + 1;
    end
    assign slow_clk = clk_div[25];
    always @(posedge slow_clk or posedge reset)
    begin
    if(reset)
        count <= 4'b1000;
    else
        count <= {count[0],count[3:1]};
    end
endmodule
```

___

## Johnson Counter
`Code`
```verilog
`timescale 1ns / 1ps
module johnsoncounter_4(
    input clk,reset,
    output reg [3:0] count
    );
    reg [25:0]clk_div=0;
    wire slow_clk;
    always @(posedge clk)
    begin
    clk_div <= clk_div + 1;
    end
    assign slow_clk = clk_div[25];
    always @(posedge slow_clk or posedge reset)
    begin
    if(reset)
        count <= 4'b0000;
    else
        count <= {count[2:0],~count[3]};
    end
endmodule
```

___
