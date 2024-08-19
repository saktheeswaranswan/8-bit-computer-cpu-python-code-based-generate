# 8-Bit Computer in Logisim

This is my 8-bit SAP that i build watching ben eather youtube playlist.

While studying the 8085 microprocessor, I was looking for resources to deepen my understanding of its internal workings. I came across the r/emudev subreddit, where I saw people building interesting projects in Logisim. This led me to discover Ben Eater's 8-bit SAP-1 YouTube playlist. After completing my studies on the 8085, I went through the entire playlist and implemented the SAP-1 in Logisim.

![image](https://github.com/user-attachments/assets/377b9600-227c-43f2-aedd-b149b6d86a7e)


You can check out a recorded demonstration of the Division program on my Twitter post [here](https://x.com/0xJatinChopra/status/1818348699078250912).


## Project Overview

This project simulates a simple 8-bit computer with the following key components and specifications:

- **Registers:**
  - **Accumulator**: An 8-bit register for arithmetic and logic operations.
  - **B Register**: Another 8-bit register used in conjunction with the Accumulator.
  - **Temporary Register**: An 8-bit register used during instruction execution.

- **Program Counter (PC):** A 4-bit parallel load register that keeps track of the next instruction to execute.

- **Memory Address Register (MAR):** A 4-bit register that holds the address of the memory location to be accessed.

- **RAM:** 16 bytes of memory used for storing both data and instructions.

- **Instruction Register (IR):** An 8-bit register that holds the current instruction being executed.

- **Arithmetic Logic Unit (ALU):**
  - Performs 8-bit addition and subtraction.
  - Affects the Carry and Zero flags based on the operation results.

- **Control Logic (Instruction Decoder):** Implemented using a 1K x 20 ROM that decodes instructions and generates control signals.

## Instruction Set

The instruction set includes the following commands:

- `LDA`: Load the Accumulator with the contents of a memory location.
- `ADD`: Add the contents of a memory location to the Accumulator.
- `JMP`: Jump to a specific memory location.
- `JC`: Jump to a specific memory location if the Carry flag is set.
- `STA`: Store the contents of the Accumulator in a memory location.
- `ADI`: Add an immediate value to the Accumulator.
- `SUB`: Subtract the contents of a memory location from the Accumulator.
- `OUT`: Output the contents of the Accumulator.
- `JZ`: Jump to a specific memory location if the Zero flag is set.
- `SUI`: Subtract an immediate value from the Accumulator.
- `HLT`: Halt the execution of the program.

### Capabilities

With the above instructions, this computer can:

- Move data in and out of RAM.
- Perform arithmetic operations on data stored in registers.
- Execute unconditional and conditional jumps.

These functionalities make the computer Turing Complete. There is still space left for 4 more instructions to be added.

Below are the resources that I've used: 
I started by stuyding about microprocessor 8085 and microcontroller 8051 while studying about them i came across ben eater youtube channler and emudev subreddit, I was amazed by looking at the cool projects people were building 
so thats how i decided of building a simple implementation.


### Programming 
![image](https://github.com/user-attachments/assets/29e98424-d7c2-4128-9f84-51a10487147c)

In order to program it you need to set `toggle_address_mode` & `prog_bus_toggle` pin to 1 and then you can feed the memory address through the `prog_addr` and can input the instructions through `prog_data`.

## Resources and Acknowledgments

- **EEEGUIDE Blogs:** Blogs for studying the 8085 microprocessor and 8051 microcontroller.
- **Digital Fundamentals (11th Edition) by Thomas L. Floyd:** Book for digital fundamentals.
- **Ben Eater's YouTube Playlist on 8-Bit SAP:** YouTube playlist for building an 8-bit CPU.
- **Emudev Subreddit:** Community for support and discussions related to emulation and low-level programming.

## Below are a few programs 

===> A MULTIPLICATION PROGRAM USING REPETITIVE ADDITION

| RAM | Mem Loc | Instruction | Opcode | Address/Data | Binary Instruction |
|-----|---------|-------------|--------|--------------|---------------------|
| 00  | 0000    | LDA 1100    | 0001   | 1100         | 0001 1100           |
| 01  | 0001    | ADD 1111    | 0010   | 1111         | 0010 1111           |
| 02  | 0010    | STA 1100    | 0101   | 1100         | 0101 1100           |
| 03  | 0011    | LDA 1110    | 0001   | 1110         | 0001 1110           |
| 04  | 0100    | SUI 01      | 1000   | 0001         | 1000 0001           |
| 05  | 0101    | STA 1110    | 0101   | 1110         | 0101 1110           |
| 06  | 0110    | JZ 1000     | 0110   | 1000         | 0110 1000           |
| 07  | 0111    | JMP 0000    | 0011   | 0000         | 0011 0000           |
| 08  | 1000    | LDA 1100    | 0001   | 1100         | 0001 1100           |
| 09  | 1001    | OUT         | 1000   | 0000         | 1000 0000           |
| 10  | 1010    | HLT         | 1011   | 0000         | 1011 0000           |
| 11  | 1011    | -           | -      | -            | -                   |
| 12  | 1100    | -           | -      | -            | -                   |
| 13  | 1101    | -           | -      | -            | -                   |

| RAM | Mem Loc | Data         | Description        |
|-----|---------|--------------|---------------------|
| 14  | 1110    | 00000000     | Multiplier/Counter |
| 15  | 1111    | 00000000     | Multiplicand       |


===> A DIVISION PROGRAM USING REPETITIVE SUBTRACTION

| RAM | Mem Loc | Instruction | Opcode | Address/Data | Binary Instruction |
|-----|---------|-------------|--------|--------------|---------------------|
| 00  | 0000    | LDA 1110    | 0001   | 1110         | 0001 1110           |
| 01  | 0001    | SUB 1111    | 0111   | 1111         | 0111 1111           |
| 02  | 0010    | JC  1000    | 0100   | 1000         | 0100 1000           |
| 03  | 0011    | STA 1110    | 0101   | 1110         | 0101 1110           |
| 04  | 0100    | LDA 1101    | 0001   | 1101         | 0001 1101           |
| 05  | 0101    | ADI 01      | 0110   | 0001         | 0110 0001           |
| 06  | 0110    | STA 1101    | 0101   | 1101         | 0101 1101           |
| 07  | 0111    | JMP 0000    | 0011   | 0000         | 0011 0000           |
| 08  | 1000    | LDA 1101    | 0001   | 1101         | 0001 1101           |
| 09  | 1001    | OUT         | 1000   | 0000         | 1000 0000           |
| 10  | 1010    | LDA 1110    | 0001   | 1110         | 0001 1110           |
| 11  | 1011    | HLT         | 1011   | 0000         | 1011 0000           |
| 12  | 1100    | -           | -      | -            | -                   |
| 13  | 1101    | -           | -      | -            | -                   |

| RAM | Mem Loc | Data         | Description |
|-----|---------|--------------|-------------|
| 14  | 1110    | 00101101(45) | Dividend    |
| 15  | 1111    | 00000110(6)  | Divisor     |


===> A FIBONACCI SEQUENCE GENERATOR PROGRAM

| RAM | Mem Loc | Instruction | Opcode | Address/Data | Binary Instruction |
|-----|---------|-------------|--------|--------------|---------------------|
| 00  | 0000    | LDA 1110    | 0001   | 1110         | 0001 1110           |
| 01  | 0001    | STA 1100    | 0101   | 1100         | 0101 1100           |
| 02  | 0010    | OUT         | 1000   | 0000         | 1000 0000           |
| 03  | 0011    | LDA 1111    | 0001   | 1111         | 0001 1111           |
| 04  | 0100    | STA 1101    | 0101   | 1101         | 0101 1101           |
| 05  | 0101    | OUT         | 1000   | 0000         | 1000 0000           |
| 06  | 0110    | ADD 1100    | 0010   | 1100         | 0010 1100           |
| 07  | 0111    | STA 1110    | 0101   | 1110         | 0101 1110           |
| 08  | 1000    | OUT         | 1000   | 0000         | 1000 0000           |
| 09  | 1001    | LDA 1101    | 0001   | 1101         | 0001 1101           |
| 10  | 1010    | STA 1100    | 0101   | 1100         | 0101 1100           |
| 11  | 1011    | LDA 1110    | 0001   | 1110         | 0001 1110           |
| 12  | 1100    | STA 1101    | 0101   | 1101         | 0101 1101           |
| 13  | 1101    | JMP 0110    | 0011   | 0110         | 0011 0110           |

| RAM | Mem Loc | Data         | Description           |
|-----|---------|--------------|------------------------|
| 14  | 1110    | 00000001     | Current Fibonacci num |
| 15  | 1111    | 00000001     | Next Fibonacci num    |




