# Simple 8-Bit CPU in Logisim

A digital logic project that follows an instruction through the fetch–decode–execute cycle. Use the circuit screenshots and component notes below to trace how the program counter, registers, and ALU work together.

![Logisim project screenshot](<Screenshot 2026-02-08 165254.png>)

## Instruction cycle

1. **Fetch** · The program counter provides an address and memory supplies the instruction to the instruction register.
2. **Decode** · Control logic interprets the instruction while the step counter sequences the micro-operations.
3. **Execute** · The A and B registers feed the ALU. The result updates the output register and the status flags.

## CPU components

### Clock

The clock generates periodic pulses that synchronize all CPU activities. 
Every operation inside the processor happens on clock edges. 
It controls register loading, instruction execution timing, and data transfer between components. 
Without the clock, the CPU cannot operate because no sequencing of steps is possible.

### Program Counter (PC)

The Program Counter stores the address of the next instruction to be executed. 
During every instruction cycle, the PC outputs its value to memory and then increments automatically to point to the following instruction. 
In jump or branch instructions, the PC is updated with a new address instead of incrementing. 
This unit controls program flow.

### Memory

Memory stores both instructions and data. 
The CPU accesses memory using addresses provided by the Program Counter or MAR. 
During fetch, instructions are read from memory. During execution, data can be read or written.
Memory acts as the storage backbone of the system.

### Memory Address Register (MAR)

MAR temporarily holds the address of the memory location that needs to be accessed.
Before any memory read or write operation, the address is first loaded into MAR. 
This ensures stable and controlled memory access.

### Instruction Register (IR)

The Instruction Register stores the currently fetched instruction from memory. 
This instruction is decoded by control logic to determine which operation must be performed. 
IR separates instruction fetching from execution and allows stable decoding.

### Step Counter

The Step Counter controls the internal execution stages of each instruction. 
It divides every instruction into smaller steps such as fetch, decode, operand load, execute, and store. 
It provides proper sequencing of micro-operations inside the CPU.

### A Register

The A Register holds the primary operand for ALU operations. 
It receives data from memory or previous computations and supplies one input directly to the ALU. 
It plays a central role in arithmetic and logic processing.

### B Register

The B Register stores the secondary operand for ALU operations. 
Together with the A Register, it provides two inputs required for computation. 
This separation allows structured data flow.

### ALU (Arithmetic Logic Unit)

The ALU is the computational core of the CPU. 
It performs arithmetic operations such as addition and subtraction, and logical operations such as AND and OR. 
It receives operands from A and B registers and produces the result, which is sent to the Output Register and Flags.

### Output Register

The Output Register stores the final processed result from the ALU. 
It provides a stable output for display or further use. 
This register represents the visible result of CPU execution.

### Flags / Zero Flag

Flags store status information about the ALU result. 
The Zero Flag becomes active when the output equals zero. 
Flags are used for conditional operations such as branching and decision making.

### Overall working

The Program Counter fetches an instruction from memory. 
The instruction is stored in the Instruction Register and decoded. 
Operands are loaded into A and B registers. The ALU executes the required operation. 
The result is stored in the Output Register, flags are updated, and the PC moves to the next instruction. 
The clock synchronizes every step. This loop repeats continuously.
