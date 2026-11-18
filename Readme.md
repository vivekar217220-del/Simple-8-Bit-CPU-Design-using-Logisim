# Simple 8-Bit CPU in Logisim

A digital logic model of a basic CPU that illustrates the fetch–decode–execute cycle. The design connects program flow, instruction decoding, operands, arithmetic and logic, and result storage through clocked stages.

![Logisim CPU project screenshot](<Screenshot 2026-02-08 165254.png>)

## Datapath and control

```text
Program counter ── Address path ── Memory ── Instruction register ── Control logic
                                       ▲                                  │
                                       └── Memory address register        │
                                                                          ▼
                     A register ──┐                           Clocked step sequencing
                                  ├── ALU ── Output register
                     B register ──┘        └── Status flags
```

| Block | Role in instruction processing |
| --- | --- |
| Clock | Synchronizes transfers and register loads with the active clock edge. |
| Program counter (PC) | Holds the address of the next instruction and advances to the following address during sequential execution. |
| Memory address register (MAR) | Holds the address selected for a memory access. |
| Memory | Supplies instructions and operands and can store data described by the design. |
| Instruction register (IR) | Holds the instruction being decoded and executed while other values move through the datapath. |
| Step counter and control logic | Sequence micro-operations and direct which block loads, drives data, or performs an operation. |
| A and B registers | Hold operands for the arithmetic logic unit. |
| Arithmetic logic unit (ALU) | Produces arithmetic or bitwise results from the operands. The design notes describe addition, subtraction, AND, and OR. |
| Output register | Holds a stable result for display after the ALU operation. |
| Status flags | Record conditions about the result, such as whether it is zero. |

## Trace an instruction

1. **Fetch.** The PC supplies the instruction address. The address path selects the memory location, and the instruction word is latched into the IR.
2. **Decode.** The control logic interprets the instruction. The step counter sequences the internal actions over clock edges.
3. **Prepare operands.** The control sequence loads or selects the operands for the A and B registers.
4. **Execute and store.** The ALU combines both operands using the selected operation. The result is latched into the output register, and the status flags reflect the result.
5. **Continue.** Sequential execution moves to the next address. The original design notes also describe updating the PC from a target address for a jump or branch.

## Example checkpoints

These sample values illustrate what to look for when tracing a circuit that implements the described datapath.

| Example | Input or condition | Expected observation |
| --- | --- | --- |
| Arithmetic result | Add 3 and 5 | Result 8 is captured at the output and the zero flag is clear. |
| Zero result | Subtract 5 from 5 | Result 0 is captured and the zero flag is set. |
| Bitwise result | AND binary `0110` and `1010` | Output shows binary `0010` for the low four bits. |
| Instruction sequencing | Step the clock through fetch and decode | The instruction register holds a stable value while later stages run. |

These are illustrative checks for reconstructing the design. The repository does not provide an opcode map, a program image, or a runnable Logisim circuit.

## Explore the project material

The repository contains Logisim screenshots and architecture notes. Start with the [overview screenshot](<Screenshot 2026-02-08 165254.png>) and [browse the circuit images](https://github.com/vivekar217220-del/Simple-8-Bit-CPU-Design-using-Logisim/tree/main) to follow the signal paths. The [embedded build journal](https://github.com/vivekar217220-del/Embedded_Journey/blob/main/What_I_Done) records additional component-level notes.

**Design focus** · Digital logic, registers, clocked datapaths, and instruction sequencing.
