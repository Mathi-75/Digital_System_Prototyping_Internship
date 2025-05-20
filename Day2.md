# DAY 2: Implementation of Logic Gates and MUX in Vivado 

📅 MAY 12, 2025  
📌 NIELIT,Calicut

## AND GATE
```verilog
module OR_Gate(
input A,B,
output Y
);
assign Y = A | B ;
endmodule
```

![image](images/Screenshot%202025-05-13%20142517.png)

___

## OR GATE
```verilog
module OR_Gate(
input A,B,
output Y
);
assign Y = A | B ;
endmodule
```
![image](images/Screenshot%202025-05-13%20141853.png)

___

## NOT GATE
```verilog
module NOT_Gate(
input A,
output Y
);
assign Y = ~A;
endmodule
```

![image](images/Screenshot%202025-05-13%20144333.png)

___

## NAND GATE
```verilog
module NAND_Gate(
input A,B,
output Y
);
assign Y = !(A & B) ;
endmodule
```

![image](images/Screenshot%202025-05-13%20143007.png)

___

## NOR GATE
```verilog
module NOR_Gate(
input A,B,
output Y
);
assign Y = !(A | B);
endmodule
```

![image](images/Screenshot%202025-05-13%20144654.png)

___


## XOR GATE
```verilog
module XOR_Gate(
input A,B,
output Y
);
assign Y = A ^ B ;
endmodule
```

![image](images/Screenshot%202025-05-13%20144013.png)

___

## 2:1 MUX
```verilog
module Mux_2_1(
input A,B,sel,
output Y
);
assign Y = sel ? B : A;
endmodule
```

![image](images/Screenshot%202025-05-13%20145516.png)

___

## 4:1 MUX
```verilog
module Mux_4_1(
input A,B,C,D,
input [1:0]S,
output Y
);
assign Y = ((~S[1])&(~S[0])&A) || ((~S[1]) & S[0]& B) || (S[1] & ~(S[0]) & C) || (S[1] & S[1] & D);  
endmodule
```

![image](images/Screenshot%202025-05-13%20151114.png)

___