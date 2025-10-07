UART Transmitter & Receiver in Verilog

This repository contains a Verilog implementation of a UART (Universal Asynchronous Receiver/Transmitter) with both transmit (TX) and receive (RX) functionality, along with a testbench for simulation.
Features

Configurable baud rate and system clock.

TX Logic: Converts 8-bit parallel input into serial output with start/stop framing.

RX Logic: Detects start bit, samples incoming serial data, and reconstructs parallel 8-bit output.

Loopback Testbench: TX is connected to RX for self-verification.

Status signals:

txdone → TX complete.

rxdone → RX complete.
How It Works
1. Baud Rate Generator

Divides system clock to match baud rate.

Generates bitDone signal to synchronize TX/RX FSMs.

2. Transmitter (TX)

Frames data as: [Start Bit | Data Bits (8) | Stop Bit].

Shifts out bits at each bitDone.

txdone asserted at end of transmission.

3. Receiver (RX)

Waits for start bit (logic 0).

Samples each bit at center timing (wait_count/2).

Reconstructs 8-bit word into rxout.

rxdone asserted at end of reception.

🔹 Testbench (tb.v)

Generates 100 MHz clock.

Sends 5 random bytes through TX.

TX output (tx) is looped back to RX input (rx).

Waits for both txdone and rxdone.

Simulation stops after test sequence.

🔹 Example Simulation Output

TX sends txin = 0xAB.

RX receives rxout = 0xAB.

Console/logs show PASS if data matches.

🔹 How to Run

Clone repository.

Open in ModelSim / Vivado / any Verilog simulator.

Compile and run tb.v.

Inspect waveform or console output.

🔹 Future Improvements

Add parity bit support.

Add FIFO buffer for TX/RX.

Add error detection (framing error, parity error).

🔹 Author

👤 Anish Chattaraj

Electronics & Communication Engineering

Focus areas: Digital Design, Signal Processing, Embedded Systems


