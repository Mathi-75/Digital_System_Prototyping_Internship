# How to Dump the verilog code to a FPGA

📅 MAY 12, 2025  
📌 NIELIT,Calicut

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