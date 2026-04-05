# Asynchronous FIFO with SystemVerilog Testbench
## Project Overview
This repository contains the RTL design and a complete SystemVerilog verification environment for an Asynchronous First-In-First-Out (FIFO) memory. The design safely transfers data between two asynchronous clock domains using Gray code pointer synchronization to prevent metastability and data corruption.
## Design Features
 * **Dual Clock Domains:** Independent write (wr_clk) and read (rd_clk) clocks.
 * **Gray Code Synchronization:** Write and read pointers are converted to Gray code before crossing clock domains using 2-stage synchronizers.
 * **Status Flags:** Accurate generation of full and empty flags to prevent memory overflow and underflow.
 * **Parameterized Design:** Configurable FIFO depth and data width.
## SystemVerilog Testbench Architecture
The verification environment is built using a layered SystemVerilog testbench approach to ensure modularity and reusability. The architecture consists of the following key components:
 * **Transaction (Sequence Item):** Defines the data variables (like data_in, data_out, wr_en, rd_en) and randomization constraints for driving the DUT (Design Under Test).
 * **Generator:** Creates randomized transaction objects and passes them to the driver through a mailbox.
 * **Write & Read Drivers:** Receives transactions from the generator and drives the pin-level signals of the Write and Read interfaces according to their respective clock domains.
 * **Write & Read Monitors:** Passively observes the interfaces, captures the pin-level activity, converts it back into transaction objects, and sends them to the scoreboard.
 * **Scoreboard:** Acts as the golden reference. It receives the driven data from the Write Monitor and compares it against the received data from the Read Monitor to verify data integrity and correct order.
 * **Environment:** The container class that instantiates, connects, and builds the generator, drivers, monitors, and scoreboard.
 * **Test:** The top-level class that configures the environment and starts the stimulus generation.
 * **Top Module & Interfaces:** Instantiates the DUT, defines the physical interfaces, generates the asynchronous wr_clk and rd_clk, and initiates the test.
## Tools Used
 * **Simulation & Synthesis:** EDA Playground
 * **Language:** SystemVerilog (IEEE 1800-2012)
## How to Run the Simulation
 1. Open the project in EDA Playground.
 2. Ensure the top-level testbench file is selected.
 3. Choose your preferred simulator [ codence 25.03 ]
 4. Check the "Open EPWave after run" box to view the simulation waveforms.
 5. Click **Run**.
## Simulation Output
 * Included simulation_output.txt detailing the console log of successful transactions and scoreboard matches.
 * Included waveform screenshots demonstrating the full and empty flag assertions and clock domain crossing logic.
