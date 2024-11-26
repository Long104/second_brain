---
date: 2024-11-18T00:00:00.000Z
tags:
  - stamford
hubs:
  - '[[]]'
urls:
  - null
---
# Contents

# BASIC STRUCTURE OF COMPUTERS

## COMPUTER TYPES

A **computer** is a fast electronic machine that accepts digitized input, processes it according to stored instructions (programs), and produces output.  
Internal storage is called computer memory. Types of computers include:

1. **Personal computers**: Common desktop computers used in homes, schools, and offices.
2. **Notebook computers**: Portable versions of PCs.
3. **Workstations**: High-resolution graphics computers for engineering and design.
4. **Enterprise systems**: Powerful systems for large-scale business data processing.
5. **Supercomputers**: Used for large-scale numerical calculations (e.g., weather forecasting).

![[Screenshot 2567-11-18 at 10.59.04.png]]

## Functional Unit

1. A computer consists of five functionally independent main parts

- **Input**: Receives data and instructions from the user or other devices.
- **Memory**: Stores data and instructions.
- **Arithmetic Logic Unit (ALU)**: Performs arithmetic and logical operations.
- **Output**: Presents processed data to the user or other devices.
- **Control Unit**: Controls the flow of data and instructions within the computer.

2. **Input unit**: -
   Input devices, such as keyboards, joysticks, trackballs, mice, and scanners, feed data into the computer.
   Key presses translate into binary code sent to memory or the processor.

### FDE cycle

The Fetch-Decode-Execute (FDE) cycle is the fundamental process by which a computer executes instructions. It's a continuous loop that repeats for each instruction in a program.

1. **Fetch:** The Control Unit retrieves the next instruction from memory, using the address stored in the Program Counter (PC).  
   The instruction is then loaded into the Instruction Register (IR).
   The PC is incremented to point to the next instruction.

2. **Decode:** The Control Unit decodes the instruction in the IR,
   determining the operation to be performed and the operands involved (data or memory locations).

3. **Execute:** The Control Unit directs the Arithmetic Logic Unit (ALU) or other components
   to perform the operation specified by the instruction.
   This might involve fetching data from memory (using the Memory Address Register, MAR,
   and Memory Data Register, MDR), performing calculations in the ALU, storing results back into memory,
   or modifying the PC to control the flow of execution (e.g., branching or jumping to a different instruction).

This cycle repeats continuously until the program terminates. The speed of the FDE cycle significantly impacts the overall performance of the computer. Modern processors employ various techniques to optimize this cycle, such as pipelining and caching, to execute instructions more efficiently.

## Memory Unit

1. Its function into store programs and data. It is basically to two types

- Primary memory (RAM, ROM)
- Secondary memory (Hard disk, SSD, USB)

| Feature           | Primary Memory (RAM, ROM(non volatile))                          | Secondary Memory (Hard Disk, SSD, USB)                         |
| ----------------- | -------------------------------------------------- | -------------------------------------------------------------- |
| **Speed**         | Very fast                                          | Relatively slow                                                |
| **Volatility**    | Volatile (data lost when power is off)             | Non-volatile (data persists even when power is off)            |
| **Cost**          | More expensive per unit of storage                 | Less expensive per unit of storage                             |
| **Capacity**      | Smaller capacity                                   | Larger capacity                                                |
| **Access Method** | Random access (any location accessed directly)     | Sequential or random access (depending on the type)            |
| **Examples**      | RAM (Random Access Memory), ROM (Read-Only Memory) | Hard Disk Drives (HDDs), Solid State Drives (SSDs), USB drives |
| **Use Cases**     | Running programs, storing currently used data      | Long-term storage of data and programs                         |

2. **Memory** stores programs and data. It's categorized as primary (RAM, ROM) and secondary (hard disk, SSD, USB).  
   Primary memory is fast, volatile, and expensive, while secondary memory is slower, non-volatile, and cheaper.
   Memory is addressable, with each location holding a word (a group of bits). Word length is the number of bits per word.
   Programs run from memory. RAM allows random access, while ROM is read-only. Caches are small, fast RAM integrated with the processor.

### program

- set of instructions

## Arithmetic Logic unit (ALU)

1. Most of the computer operators are executed in **ALU** of the processor like addition, subtraction, division, multiplication, etc.

- The operands are brought into the ALU from memory and stored in high speed storage elements called register.
- Then according to the instructions the operation is performed in the required sequence.
- The control and the ALU are many times faster than other devices connected to a computer system.
- This enables a single processor to control a number of external devices such as key boards, displays, magnetic and optical disks, sensors and other mechanical controllers.

1. in the old day we use 16 GPR (general purpose register)

![[Screenshot 2567-11-21 at 09.34.01.png]]

## Register

- Instruction Register: Holds the instruction currently being executed.
- Data Register: Holds data being processed by the ALU.
- Address Register: Holds the memory address of data or instructions.

## the program counter PC

- program counter is keep track of the instruction what is it doing right now
  by using pointer point to the address of the instruction in the stack

- This is another specialized register that keeps track of execution of a program.
  It contains the memory address of the next instruction to be fetched and executed.
  Besides IR and PC, there are n-general purpose registers R0 through Rn-1.
  The other two registers which facilitate communication with memory are: -

1. MAR – (Memory Address Register):- It holds the address of the location to be accessed.
2. MDR – (Memory Data Register):- It contains the data to be written into or read out of the address location.

## bus structure

- The simplest and most common way of interconnecting various parts of the computer.
  To achieve a reasonable speed of operation, a computer must be organized so that all its units can handle one full word of data at a given time.
  A group of lines that serve as a connecting port for several devices is called a bus.

- In addition to the lines that carry the data, the bus must have lines for address and control purpose.
  Simplest way to interconnect is to use the single bus as shown

![[Screenshot 2567-11-21 at 11.32.30.png]]

## performance

- processor time
- elapsed time
-
