# 8-Bit-UART
8-Bit UART Project built using System Verilog. Contain RTL, Verification, and Documentation


Goal: 
Create a UART controller that takes and sends inputs/outputs from 8 bit data buses. 
Start with a baud rate of 9600 to start and improve up to changeable speeds.
The UART packet will have: 1 Start bit, 8 Data Bits(Little Endian), 1 Stop Bit (8N1)

Architecture:

The controller will have a 8 bit data buses that acts as both input and output

Both RX and TX utilize a counter to determine how long before bit sent/received, allowing for adjustable baud rate.

TX(Transmitter): 
State machine has: 
IDLE - TX stays HIGH until data available
START - TX goes LOW for 1 counter period
DATA(Sampling) - Send 8 bit data, move out 1 bit out of shift register if counter == 0
STOP - TX Goes HIGH for 1 counter period

RX(RX): 
State machine has: 
IDLE - RX stays LOW until data available
START - Checks if start bit is LOW at midpoint
DATA(Sampling) - Samples 8 bit data, move out 1 bit into shift register if counter == 0
STOP - Check if stop bit is HIGH


Additional: 
Add on CRC-8 and Frame protocol to handle bit errors instead of Parity bit. This will be built after the main UART (Before and After sending data through).
