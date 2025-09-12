# RISC-V Architecture: Detailed Analysis & Learnings

This repository is designed to share the learnings regarding the fundamentals and advanced concepts of computer architecture, processors and RISC-V. It covers the core components of processors, memory systems, instruction sets, practical applications and much more.
## Table of Contents
1. <a href="#intro">Introduction to digital world</a>
2. <a href="#pro">Processors</a>
3. <a href="#bin">Binary and Data Representation</a>
4. <a href="#reg">Registers: Processor's Workspace</a>
5. <a href="#mem">Memory System Architecture</a>
6. <a href="#exec">Processor Execution Models</a>
7. <a href="#isa">RISC-V ISA</a>
8. <a href="#cond">Control Flow and Program Structure</a>
9. <a href="#ext">Advanced RISC_V Features and Extensions</a>
8. <a href="#exp">Experimentation with Simulator</a>


# <h1 id="intro">Introduction to Digital World</h1>
Processors are an integral part of our lives. They are present in almost all of the electronic devices we use on a day to day basis from our smartphones all the way to our cars

<img width="942" height="364" alt="image" src="https://github.com/user-attachments/assets/c4b847d6-14dd-41a1-92f9-327d7e67a925" />

# <h1 id="pro">Processors</h1>
Termed as the "brain" of the computer, processor in simple words is an extremely fast calculator that can perform the following functions:
```Arithmetic```, ```Logic Operations```, ```Comparison```, ```Access memory```, ```Make decisions``` and ```Input/Output```
## Instruction Execution Cycle
Every processor follows a basic this basic cycle billions of times per second
1. ```Fetch```: Get the next instruction from memory
2. ```Decode```: Figure out the instruction
3. ```Execute```: Perform the operation
4. ```Writeback```: Store the result
5. ```Repeat```: Move to the next instruction

<img width="600" height="538" alt="image" src="https://github.com/user-attachments/assets/fb7f6737-964b-4bb4-a0d5-7254f8e92b15" />

## Processor Performance
### Clock Speed (Frequency)
Indicates how many instruction cycles processor can attempt in one second. It is measured in Hertz (Hz)

<img width="954" height="215" alt="image" src="https://github.com/user-attachments/assets/5f2125fc-b352-41f6-befa-3e7a3c625453" />

### Instruction per Cycle
1. Simple Processors = 1 instr. per cycle
2. Superscalar Processors = 2-4 instr. per cycle
3. High-performance Processors = 4-8 instr. per cycle

### Performance Calculation
CPU Performance is calculated using a formula

<img width="860" height="433" alt="image" src="https://github.com/user-attachments/assets/e512513c-8b7d-4d42-8d73-4f85730e181d" />

# <h1 id="bin">Binary and Data Representation</h1>

In computer chip, information is stored using voltage levels. High voltage is represented as ```1``` and low voltage as ```0```. It can be converted to other number systems

<img width="927" height="287" alt="image" src="https://github.com/user-attachments/assets/7c3535b4-9808-48e4-bec8-1e8eb0f4c32f" />
<br>

### Signed and Unsigned Numbers
1. Unsigned Numbers - Use all bits for magnitude
  - 8 bit: 0 to 255
  - 16 bit: 0 to 65535

2. Signed Numbers - Use to represent negative numbers. Uses two's complement representation
   - 8 bit: -127 to +127
   - 16 bit: -32768 to +32767

<img width="860" height="465" alt="image" src="https://github.com/user-attachments/assets/94e05900-8005-427f-9093-5297766e78a0" />


# <h1 id="reg">Registers</h1>
Registers are tiny storage elements built directly into the processor chip using transistors arranged as flipflops

![OIP-987733606](https://github.com/user-attachments/assets/b3aa8f65-f864-4945-84e0-e3ea02148371)
(Shows MSB and LSB in 8-bit)

### RISC-V Register Set
RISC-V has 32 general purpose registers (x0-x31) plus special registers

<img width="860" height="458" alt="image" src="https://github.com/user-attachments/assets/1788eda0-1460-456b-9b3e-4262c113cb50" />

1. ```Register x0``` : Hardwired to contain zero only. It is used for copying, clearing, loading and discarding calculations
2. ```Register x1``` : Return address. Cpu returns here after executing a function
3. ```Register x2``` : Stack pointer. Points to the top of stack
4. ```Register x3``` : Global Pointer
5. ```Register x4``` : Thread Pointer
6. ```Register x5 - x7``` : Temporaries. To store temporary values
7. ```Register x8``` : Saved Register/Frame Pointer.
8. ```Register x9``` : Saved Register. Used to preserve original values
9. ```Register x10 - x11``` : Function Arguments/Return Values. Stores first two arguements and return values
10. ```Register x12 - x17``` : Arguments. Stores 3-8 function arguements
11. ```Register x18 - x27``` : Saved Register
12. ```Register x28 - x31``` : Temporaries

**Caller Saved Registers**:
Registers: t0-t6, a0-a7
Used to store temporary values. Can be easily overwritten by Callee Function. The caller must save the value if it needs the value later on.

**Callee Saved Register**:
Registers: s0-s11
Callee must save these registers if it modifies them and restore them before returning. Because caller expects these registers to remain unchanged

                ┌───────────────────────────┐
                │         MAIN()            │
                ├───────────────────────────┤
                │   Uses t0, a0, a1         │  ← Caller-saved
                │   Saves t0 before calling │
                │   Calls FUNC()            │
                ├───────────────────────────┤
                         ↓  JAL
                ┌───────────────────────────┐
                │         FUNC()            │
                ├───────────────────────────┤
                │   Uses s0, s1             │  ← Callee-saved
                │   Saves s0, s1 on stack   │
                │   Restores before return  │
                └───────────────────────────┘


# <h1 id="mem">Memory System Architecture</h1>

### Memory Hierarchy
Computer memory is organized in a hierarchy based on speed, size and cost:

<img width="912" height="270" alt="image" src="https://github.com/user-attachments/assets/688943ea-fd8a-4dc2-bf81-dd99a50695a4" />

## Virtual Memory
Virtual Memory creates an illusion that each program has access to a large, private memory space even though the physical memory is limited and shared.

**Virtual View (Programs' Perspective)**

<img width="284" height="289" alt="image" src="https://github.com/user-attachments/assets/011b1596-9a84-49d2-ab89-84d5c3966389" />


Physical View (Reality)

<img width="248" height="189" alt="image" src="https://github.com/user-attachments/assets/a7a951c2-08e3-4a25-8508-97af7391e542" />


### How does Virtual Memory Works
Step 1 — Virtual Addresses
Every program thinks it has access to a huge memory space. Program A sees addresses from 0x00000000 → 0xFFFFFFFF (4 GB). Program B also sees the same range. But physically, they share the same RAM.

Step 2 — MMU Translates Virtual → Physical
The MMU (Memory Management Unit) converts virtual addresses into physical addresses using:
- Page tables (mapping virtual pages → physical pages). 
- TLB (Translation Lookaside Buffer) for speed

MMU Translation Process
1. Checks TLB for cached translation. If address found the translation of address is quick.
2. If not found, it consults Page tables to find the pages:
  ```Virtual Page: 0x10000``` and ```Physical Page: 0x01200```
3. Combines page address with offset:
   ```Virtual Address: 0x10000000 = Page 0x10000 + Offset 0x000```
   ```Physical Address: 0x01200000 = Page 0x01200 + Offset 0x000```
4. Access memory at ```0x01200000```

# <h1 id="exec">Processor Execution Models</h1>

## In-Order Execution
In-order processors execute instructions exactly in the sequence they appear in the program one by one.

<img width="886" height="589" alt="Screenshot 2025-09-06 131530" src="https://github.com/user-attachments/assets/91202a49-e664-4de2-98bf-9f60a657f262" />

**Advantages**
- suitable for simple hardware designs
- lower power consumption
- easier to debug
- lower cost to manufacture

**Disadvantages**
- limited performance
- cannot perform instruction level parallelism
- stalls on memory access

## Out-of-Order Execution
Out-of-order processors can rearrange instruction execution to improve performance as long as dependencies are respected

<img width="925" height="474" alt="image" src="https://github.com/user-attachments/assets/1d04d982-6ef3-4dbe-84bf-e56335a1849f" />

### Key components:
1. ```Instruction Queue```: Buffer(temp storage) holding multiple instructions so that CPU knows what instructions are upcoming
2. ```Reservation Stations```: Hold instructions waiting for operands(data). Allows CPU  to prepare instructions in advance and execute them when data is ready
3. ```Reorder Buffer```: Ensure instructions complete in program order even if instructions finish out of order
4. ```Register Renaming```: Eliminate false dependencies. Hardware renames registers to avoid false dependencies

**Advantages**
- higher performance on typical programs
- better utilization of execution units
- hides memory latency
- exploits instruction-level parallelism

**Disadvantages**
- complex hardware design
- higher power consumption
- expensive to manufacture

## Superscalar Execution
Superscalar processors have multiple execution units and can execute multiple instructions simultaneously.

<img width="860" height="502" alt="image" src="https://github.com/user-attachments/assets/aa93f4c4-78b2-4dd2-a577-82cc761ce2b6" />
<br><br>

**Resources** <br>
- 2-4 Integer ALU's <br>
- 1-2 Multiply/Divide units <br>
- 2-3 Load/Store units (memory access) <br>
- 1-2 Branch units <br>
- 2-4 Floating-point units <br>
 <br><br>
<img width="609" height="193" alt="image" src="https://github.com/user-attachments/assets/f67fe9c7-896b-4368-9c40-d0b2e8ed5c13" />

## Issue Width vs Execution Width
1. Issue Width: How many instructions can be sent to execution units per cycle
2. Execution Width: How many instructions can actually be completed per cycle

Example:
```A "4-issue" processor can send 4 instructions to execution units per cycle, but due to dependencies and resource conflicts. might only complete 2.3 instructions per cycle on average```
## VLIW (Very Long Instruction Word)
VLIW processors move the complexity of ```instruction scheduling``` from hardware to software (the compiler). Each instruction word contains multiple operations that are guaranteed to be independent

<img width="860" height="625" alt="image" src="https://github.com/user-attachments/assets/edbdf432-5010-40b9-8293-f8e2c4552394" />
<br><br>
Example in RISC Asm:
<br><br>

<img width="809" height="223" alt="image" src="https://github.com/user-attachments/assets/e8b1ad28-80a8-44a8-8f06-07be7a30c289" />
<br><br>

Note:
```Instruction Scheduling: ```deciding order in which instructions are executed

## Specialized Execution Models
### Dataflow Processors
Execute instructions as soon as their operands(data) are available, regardless of program order. Execution is driven by data availability and not by instruction sequence
<br>
<img width="805" height="173" alt="image" src="https://github.com/user-attachments/assets/859062ac-565a-4bd8-abcb-3ac1a7264feb" />

### Vector Processors
Execute same instructions on multiple data elements simultaneously
<br>
<img width="773" height="216" alt="image" src="https://github.com/user-attachments/assets/940829d0-308e-450a-9c2a-d01b175ca226" />



# <h1 id="isa">RISC-V ISA</h1>
## Instruction Formats (Binary Encoding)
```Instruction Width``` - no. of bits used to represent single instruction in an ISA.

RISC-V uses 32-bit fixed ```instruction-width``` for various reasons:
1. simplicity: easier to decode and fetch
2. performance: predictable instruction fetch
3. alignment: instructions naturally align to 4-byte boundaries
4. pipelining: uniform instruction size simplifies pipeline stages

## R-Type Format (Register-Register Operations)
Used when both operands come from register and the result is stored in another register
<br>
<img width="860" height="151" alt="image" src="https://github.com/user-attachments/assets/9e7bfd8d-6518-46ed-ad50-114e60ea515e" />

**Detailed Field Analysis**
1. ```opcode``` : 0-6 bits. Instruction family (0110011 for R-type arithmetic)
2. ```rd```     : 7-11 bits. Destination register (00000-11111 for x0-x31)
3. ```funct3``` : 12-14 bits. Operation type (000=ADD/SUB, 001=SLL, etc)
4. ```rs1```    : 15-19 bits. First source register (00000-11111 for x0-x31)
5. ```rs2```    : 20-24 bits. Second source register (00000-11111 for x0-x31)
6. ```funct7``` : 25-31 bits. Additional operation info (0000000=ADD, 0100000=SUB)

Example
<br>
<img width="501" height="311" alt="image" src="https://github.com/user-attachments/assets/c9c3917f-c300-4771-a23c-b59c7292b046" />

## I-Type Format (Immediate Operations)
Used when one operand is constant (immediate)
<br>
<img width="860" height="154" alt="image" src="https://github.com/user-attachments/assets/5f74020d-6fc7-487e-8be7-e171a9b71437" />

Example
<br>
<img width="827" height="298" alt="image" src="https://github.com/user-attachments/assets/0bb68a9c-d98a-4455-bc8d-b897fd7064b7" />

## Load/Store Architecture
In RISC-V only dedicated load/store instructions can access memory. This has several advantages:
1. simpler instruction formats
2. easier pipeline
3. more predictable timing
4. better compiler optimization

Example 
<br>
<img width="197" height="88" alt="image" src="https://github.com/user-attachments/assets/9171e67c-0c1f-4879-9f04-c2f2cbc8659f" />

### Memory Access Instructions
Supposing at ```Adress 0x1000 : 0x87654321 (32-bit word)```. It is of ```4 Bytes``` where: <br>
```Byte 0x1000 : 0x21``` <br>
```Byte 0x1001 : 0x34``` <br>
```Byte 0x1002 : 0x56``` <br>
```Byte 0x1003 : 0x78``` <br>

Assuming ```x1 contains 0x1000```

- Load Word (32-bit) <br>
  ```lw x2, 0(x1)  ->  x2 = 0x87654321```
  
- Load Halfword (16-bit) with sign extension <br>
  ```lh x2, 0(x1)  ->  x2 = 0x4321``` <br>
  loads bytes from 0x1000 to 0x1001 = 0x4321 <br>
  since bit 15 = 0 i.e. 0x4321 is positive <br>
  ```x2 = 0x00004321``` 
  
  ```lh x2, 2(x1)  ->  x2 = 0x8765``` <br>
  loads bytes from 0x1002 to 0x1003 = 0x8765 <br>
  since bit 15 = 1 i.e. 0x8765 is negative <br>
  ```x2 = 0xFFFF8765```
  
- Load Halfword Unsigned (16-bit) <br>
  ```lhu x2, 2(x1)  ->  x2 = 0x8765``` <br>
  loads bytes from 0x1002 to 0x1003 = 0x8765 <br>
  always zero-extended regardless of sign bit <br>
  ```x2 = 0x00008765```
  
- Load Byte (8-bit) with sign extension <br>
  ```lw x2, 0(x1)  ->  x2 = 0x21``` <br>
  loads byte from 0x1000 = 0x21 <br>
  since bit 7 = 0 i.e. 0x21 is positive <br>
  ```x2 = 0x00000021```

  ```lw x2, 3(x1)  ->  x2 = 0x87``` <br>
  loads byte from 0x1003 = 0x87 <br>
  since bit 7 = 1 i.e. 0x87 is negative <br>
  ```x2 = 0xFFFFFF87```
  
- Load Word (8-bit) Unsigned <br>
  ```lw x2, 3(x1)  ->  x2 = 0x87``` <br>
  loads byte 0x1003 = 0x87 <br>
  always zero-extended regardless of sign bit <br>
  ```x2 = 0x00000087```

### Address Calculation Modes
The only mode in RISC-V to calculate address is: <br>
```Base + Offset addressing```

```Address  =  register_value + sign_extended_immediate```

1. **Array Access** <br>

   Suppose an example
   <br>
   <img width="570" height="79" alt="image" src="https://github.com/user-attachments/assets/ea67d131-985c-423e-9818-4313554b8bd9" />
   <br>
   CASE 1: When index cannot be fit inside 12-bit offset <br>
   ```slli x12, x11, 2``` - x12 = index * 4 (shift left 2 means multiply by 4) <br>
   ```add x12, x10, x12``` - x12 = base + (index * 4) <br>
   ```lw x13, 0(x12)``` <br>
  
   CASE 2: When index can be fit inside 12-bit offset <br>
   ```lw x13, 20(x10)``` - loads array[5] directly (20 = 5 * 4) <br>

2. **Structure Member Access** <br>
  
   Suppose an example
   <br>
   <img width="544" height="46" alt="image" src="https://github.com/user-attachments/assets/1cc87019-abed-42cc-92fa-18f4122401a5" />
   <br>
   ```Note : int x, int y, int z are all of 4 bytes hence offset is 4``` <br>

   ```lw x14, 4(x10)``` <br>
   
3. **Stack Access**
   <br>
   Local variables at negative offsets from frame pointer <br>
   ```lw x15, -8(s0)``` - loads local variable at fp-8 <br>
   ```sw x16, -12(s0)``` - store to local variable at fp-12
   
4. **Global Variable Access** using global pointer
   <br>
   ```lw x17, 100(gp)``` - load global variable at gp+100 <br>
   ```sw x17, 200(gp)``` - store global variable at gp+200

# <h1 id="cond">Control Flow and Program Structure</h1>

## Conditional Branches
### Branch Instruction Format (B-type)
Branch Instruction is used when we have to jump to another location if a condition is true
<br>
<img width="860" height="155" alt="image" src="https://github.com/user-attachments/assets/6862be16-0cae-401d-8284-62a11c81b19e" />


**Note**
1. ```imm[11]``` : jump offset bit
2. ```imm[4:1]``` : next 4-bit of jump offset
3. ```imm[10:5]``` : next 6-bit of jump offset
4. ```imm[12:11]``` : part of jump offset (sign bit)

### Branch Condition and Implementation
<img width="965" height="235" alt="image" src="https://github.com/user-attachments/assets/f18ecdda-170c-4ef7-8a78-017ab74f0941" />

**Instructions** <br>
1. ```BEQ``` - branch if equal. checks equality of two registers by subtracting them and equating them to 0 <br>
2. ```BNE``` - branch if not equal. checks non equality of two registers by subtracting them and ensuring result is not 0 <br>
3. ```BLT``` - branch if less than (signed). checks if one register is less than other by subtracting them and branches if sign bit is set or 1 <br>
4. ```BGE``` - branch if greater or equal (signed). checks if one register is greater than other by subtracting them if sign bit is clear or 0 <br>
5. ```BLTU``` - branch if less than unsigned. checks if one register is less than other by subtracting them and if carry over takes place <br>
6. ```BGEU``` - branch if greater or equal unsigned. checks if one register is greater than other by subtracting them and no carry over is generated <br>
<br>

**Other Instructions**
1. ```BLE``` - branch if less than or equal
2. ```BEQZ``` - branch if equal to zero
3. ```BNEZ``` - branch if not equal to zero

<a href="#if_example">See Example</a>

## Loop Implementation
### For Loop

for (i = 0; i < n; i++) <br>
x1 = i <br>
x2 = n <br>

    li   x1, 0         # initialize i = 0
    # assume x2 contains n already (loop limit)

loop_start:             # <--- loop label <br>
      
    bge  x1, x2, loop_end # if i >= n, exit loop
    
    # ---- Loop body ----
    # process array[i] or do work here
    # -------------------

    addi x1, x1, 1     # i++
    j    loop_start    # go back to start of loop

loop_end: <br>
    # loop finished

**Notes**
```loop_start``` - this is a label. CPU doesn't execute it. It just marks the memory the address in memory so instructions inside it know where to go
```j``` - unconditional jump. Always goes back to the instruction at ```loop_start```. This creates the repetition

### Countdown Loop
Instead of counting up (usual looping), countdown loop starts from i = n and ends at i = 0. It is more efficient compared to countup loop as equating to zero is more easier than any other number
<br>
<img width="680" height="317" alt="image" src="https://github.com/user-attachments/assets/e3bdbe82-563b-45d7-a087-7ed179e1247c" />
<br>

### While Loop

<img width="723" height="323" alt="image" src="https://github.com/user-attachments/assets/dab50c94-b7f1-4854-9ef9-d373b88c13d9" />

### Do-While Loop

<img width="707" height="292" alt="image" src="https://github.com/user-attachments/assets/44aa73ca-b98d-4456-82ac-aae9afe8f970" />

# <h1 id="ext">Advanced RISC_V Features and Extensions</h1>
RISC-V uses a modular approach where the base instruction set (RV32I or RV64I) is extended with additional instruction sets for specific needs

### Standard Extensions
RISC-V has many instructions for meeting various purposes
| Extension | Description                         | Purpose and Insructions                                        |
|-----------|-------------------------------------|----------------------------------------------------------------|
| A         | Atomic instructions                 | Atomic memory operations for multithreading
| C         | Compressed instructions             | Shorter 16-bit instructions to save memory
| D         | Double-precision floating-point     | 64-bit floating math
| F         | Single-precision floating-point     | 32-bit floating math
| *G*       | *Shorthand for IMAFD extensions*    | Short for the combo of IMAFD
| H         | Hypervisor extension                | For visual support
| I         | Integer                             | Basic integer instruction set (required)
| M         | Integer multiplication and division | Hardware multiplication and division
| P         | Packed-SIMD instructions            | Multimedia and DSP tasks
| Q         | Quad-precision floating-point       | 128-bit floating math
| V         | Vector operations                   | SIMD operations for AI & HFC

Notes:
```SIMD``` - Single instructions, multiple data
```HFC``` - High Performance Computing

**Examples**

| Name      | Description                                                              |
|-----------|--------------------------------------------------------------------------|
| RV32I     | Supports only basic operations natively on 32 bits                       |
| RV32GC    | General purpose uses on 32 bits with support for compressed instructions |
| RV64IMACV | For intensive and parallel integer-only computing                        |
| RV64GCV   | Theoretically suitable for future personal computers                     |

# <h1 id="exp">Experimentation/Tinkering with Simulator</h1>
I'm using the <a href="https://venus.cs61c.org/">Venus Simulator</a> for trying out simple programs to grasp more about RISC-V Assembly

## 1. Printing something on console

Steps:
1. Creating a ```.data``` section where variables are stored
2. ```message:``` is a label which stores a string

<img width="1592" height="630" alt="image" src="https://github.com/user-attachments/assets/d2934f5a-e14c-4a3e-8551-cfe9f307e7f6" />
<br>
<img width="1895" height="998" alt="image" src="https://github.com/user-attachments/assets/8283af95-7857-489c-9e03-c2899a7404d4" />

## 2. Adding two numbers in RISC-V assembly

Steps:
1. Creating a ```.data``` section where variables are stored
2. ```a:``` and ```b:``` are labels
3. ```.word 8``` allocates 4 bytes and stores value ```8```
4. ```.word 7``` allocates 4 bytes and stores value ```7```
5. ```.text``` declares the code section
6. ```.main``` label marking the starting point of code

<img width="1276" height="773" alt="image" src="https://github.com/user-attachments/assets/f3340205-5ac5-4bec-a1fc-a10f2d207fda" />
<br><br>

Output:
Answer is ```15 or F``` stored in ```t3```
<img width="1894" height="977" alt="image" src="https://github.com/user-attachments/assets/737ebcc8-bbf1-42e8-9021-69ceeeea80ad" />

## 3. Creating a simple function that multiples 4 numbers together

Steps:
1. Defines 4 arguments inside main
2. allocate stack space first
3. saves the return address
4. saves the s0 and moves the stack pointer
5. multiplies the arguements
6. stores the result in a0
7. restores s0, return address and deallocate stack space
<br>
<img width="959" height="861" alt="image" src="https://github.com/user-attachments/assets/70464f18-fef9-41bd-a0f5-27f44d770c49" />
<br><br>

Output:
Answer is 360 written as ```168``` in hexadecimal saved at ```a0```
<img width="1699" height="989" alt="image" src="https://github.com/user-attachments/assets/90baecdb-c4bd-47f2-9ea0-2a25e1c09635" />
