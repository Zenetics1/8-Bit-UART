# 8-Bit UART

An 8-bit UART project built using **SystemVerilog**. Contains RTL, verification, and documentation.

---

## Goal

Create a UART controller that sends and receives data over 8-bit data buses.

- Start with a baud rate of **9600**, then improve to support changeable speeds
- UART packet format (**8N1**):
  - 1 Start bit
  - 8 Data bits (LSB first)
  - 1 Stop bit

---

## Architecture

The controller has an **8-bit data bus** that acts as both input and output.

Both RX and TX use a **counter** to determine how long before a bit is sent/received, allowing for an adjustable baud rate.

### TX (Transmitter)

| State | Behavior |
|---|---|
| **IDLE** | TX stays HIGH until data is available |
| **START** | TX goes LOW for 1 counter period |
| **DATA** | Send 8-bit data, shifting 1 bit out of the shift register when counter == 0 |
| **STOP** | TX goes HIGH for 1 counter period |

### RX (Receiver)

| State | Behavior |
|---|---|
| **IDLE** | RX line stays HIGH until a falling edge (start bit) is detected |
| **START** | Check that the start bit is LOW at its midpoint |
| **DATA** | Sample 8-bit data, shifting 1 bit into the shift register when counter == 0 |
| **STOP** | Check that the stop bit is HIGH |

---

## Additional

Add a **CRC-8** and **frame protocol** to handle bit errors instead of a parity bit. This will be built after the main UART, applied before and after sending data through.