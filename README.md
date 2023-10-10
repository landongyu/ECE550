# ECE550

## Checkpoint 3

**Author:** Dongyu Lan  
**Date:** 10/10/2023  
**Netid id:** dl393  
**Course:** ECE 550, Duke University, Durham, NC

### Design Description
I developed and simulated a register file using Verilog, which features 32 registers, each with a width of 32 bits. This register file supports two read ports and one write port.
For the read operation, the two read ports take in data from all the registers in the file. Control bits (ctrl_readRegA and ctrl_readRegB) are used to select the specific register from which data is retrieved, resulting in the outputs data_readRegA and data_readRegB.
On the write side, a similar mechanism is used with control bits (ctrl_writeReg) to specify the target register, into which data (data_writeReg) is written.
To enable these read and write operations, I've implemented three essential modules in my design: "registers," "decoder," and "tristate buffer." These modules collectively enable the register file to perform data storage and retrieval efficiently.

#### Module write_decoder
It takes a 5-bit selection signal select_bits and an enable signal enable. It generates a 32-bit output, out, by selectively appending zeros to temp0 based on the bits set in select_bits. The enable signal determines whether the output is enabled or not.

#### Module dffe
It defines a 32-bit D flip-flop with clear and enable controls. It stores data from the d input on the positive edge of the clock (clk) if the en signal is active, and it can be cleared to '0' when the clr signal is active. The initial state is set to '0'.

#### Module regfile
It allows data to be written into and read from specific registers, and it features the following key components:
Inputs: It accepts control signals for enabling writing, resetting, and selecting registers, as well as clock signals and data to be written.
Outputs: It provides two separate data outputs based on the selected registers.
Write Data Section: The module uses a "write_decoder" to determine the register to which data should be written based on control signals. It has 32 instances of "dffe_ref" to store data when enabled.
Read Data Section: It employs "write_decoder" modules to select registers from which data should be read. Tristate buffers are used to facilitate data reading based on control signals.

#### Module tristate_buffer
The "tristate_buffer" module acts as a switch for data. If the "tristate_select" signal is enabled (1), it lets the "tristate_data" pass through to the output, "tristate_buffer_out." If "tristate_select" is disabled (0), it isolates the output, effectively disconnecting the data flow. 


