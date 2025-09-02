
# RISC-V Architecture: Detailed Analysis & Guide


This study guide is designed to help you review the fundamental and advanced concepts of the RISC-V architecture. It covers the core components of processors, memory systems, instruction sets, and practical applications.
## Table of Contents
1. [Introduction_to_processore](#introduction-to-processors-and-digital-systems)<br>
    1.1 [Role_of_processors](#1-role-of-processors)<br>
    1.2 [Processor_functions](#2-processors-functions)<br>
    1.3 [Techology_Hierarchy](#3-techology-hierarchy)<br>


# Introduction to processors and digital systems
## <u>1. Role of processors<br></u>
<div align="center">
<img src="Resources/what-does-a-processor-do.png">
</div>
Processors are integral to daily technology as they are the core components that execute instructions, process data, and enable computing devices to perform tasks. General-purpose processors like CPUs (Central Processing Units) handle a broad range of tasks including running operating systems, applications, and managing basic input/output functions. Specialized processors such as ISPs (Image Signal Processors), GPUs (Graphics Processing Units), and ML (Machine Learning) accelerators are designed for distinct, intensive tasks like image processing, rendering graphics, and accelerating AI computations, respectively.
<div align="center">
<img  src="Resources/Processor_1.webp">
</div>
<b>A. Role of General-Purpose CPUs</b><br>
CPUs are often called the "brain" of computers because they execute instructions sequentially for a variety of general computing needs such as browsing the internet, handling files, or running software applications. They manage data flow and system operations by fetching, decoding, executing instructions, and storing results. Their design focuses on single-threaded and latency-sensitive operations, with multiple cores enabling some <a href = 'https://search.brave.com/search?q=parallelism+meaning+in+computer+architecture&source=web&summary=1&conversation=8ff5c2596b78c07cdc87a0' target ='_blank' >parallelism</a> for multitasking and enhancedefficiency.

<b>B. Specialized Processors and Their Functions</b><br>
<ul><li>ISPs (Image Signal Processors):</li> Specialized for real-time image and video processing, such as enhancing photo quality and managing camera inputs in smartphones and other devices.

<li>GPUs (Graphics Processing Units):</li> Originally designed to accelerate 3D graphics rendering by processing many operations in parallel with their numerous smaller cores. GPUs are also widely used for parallelizable tasks beyond graphics, like AI model training and data analysis, due to their ability to perform many calculations simultaneously.

<li>ML Accelerators:</li> These are dedicated processors designed to accelerate machine learning workloads efficiently by offloading specific AI computations from CPUs or GPUs, delivering faster training and inference speeds in AI applications.</ul>

<b>C. Integration and Importance</b><br>
Modern computing systems often combine CPUs with specialized processors (such as integrated GPUs in system-on-chip designs) to balance general-purpose and specialized workloads, improving performance and energy efficiency. These processors collectively enable the smooth operation of technologies used daily—from smartphones to home automation to advanced AI-driven systems.

In summary, processors provide the computational foundation for all digital technology, with CPUs serving as versatile controllers and specialized processors like ISPs, GPUs, and ML accelerators enhancing performance for targeted tasks in modern computing environments. This differentiation allows devices to handle a vast array of user and system demands effectively.

## <u>2. Processors Functions</u><br>
Processor's basic capabilities include performing arithmetic operations (addition, subtraction, multiplication, division), logic operations (AND, OR, NOT, XOR), and comparison operations (equal to, less than, greater than). It accesses memory to read and write data, manages decision-making based on instructions (e.g., branching or conditional execution), and handles input/output (I/O) operations to communicate with peripherals.
<div align="center">
<img src ="Resources/ABasicComputer.svg.png"></div>
<b>A. Basic Functions of a Processor</b>
<ul><li>
Arithmetic Operations:</li> The Arithmetic Logic Unit (ALU) performs calculations like addition and subtraction.

<li>Logic Operations:</li> The ALU also performs logical operations such as AND, OR, NOT.

<li>Comparison:</li> The processor compares values to determine conditions for branching decisions.

<li>Memory Access:</li> It reads data from and writes data to system memory or registers.

<li>Decision Making:</li> Using conditional instructions, the processor controls the flow of programs by making decisions based on comparisons.

<li>Input/Output (I/O):</li> The processor communicates with external devices, coordinating data exchange through I/O operations.

<li>Instruction Cycle:</li> It fetches instructions from memory, decodes them to understand the operation, executes the operation, and stores the result as needed.
</ul>
<b>B. Limitations of a Processor</b><br>
A processor cannot directly understand high-level abstract concepts such as human language or semantics. It operates on binary instructions and numerical data, so complex tasks like natural language understanding require specialized software or hardware accelerators for machine learning, which interpret and process high-level data on behalf of the CPU.
<br><br>
In summary, processors execute fundamental computational and control tasks essential for running software, but they do not inherently understand human languages or complex abstract data. These require additional layers of interpretation and computation beyond the processor's direct capabilities.


## <u>3. Techology Hierarchy  </u><br>

🏗️Computing systems are built in layers. Each layer communicates with the one below it. Here's a simplified structure from bottom to top:

| **Layer**                    | **Description**                                                                 |
|------------------------------|---------------------------------------------------------------------------------|
| 1. **Hardware**              | Physical circuits: transistors, logic gates, silicon chips (CPUs, RAM, etc.)   |
| 2. **Processor Architecture (ISA)** | Defines the instructions and behavior of the CPU (e.g., RISC-V, x86, ARM)        |
| 3. **Assembly Language**     | Human-readable version of machine instructions specific to an architecture     |
| 4. **Low-Level Programming Languages** | Languages like C or Rust, which compile down to assembly/machine code           |
| 5. **Operating System**      | Manages hardware and software resources (Linux, Windows, macOS, etc.)          |
| 6. **High-Level Programming Languages** | User-friendly languages like Python, Java, JavaScript, etc.                     |
| 7. **Applications**          | Programs users interact with: browsers, games, productivity tools, etc.        |

---

### 🔧 What is RISC-V?

**RISC-V** is an **Instruction Set Architecture (ISA)** — a specification for how a processor should operate. Unlike x86 and ARM, RISC-V is:

- **Open-source** (no licensing fees)
- **Modular** (you can choose only the features you need)
- **Designed for scalability** (from small embedded chips to full desktops)

> RISC-V does not define how the chip is built physically — it defines how software talks to the hardware.

---

### 📐 Processor Architecture (ISA) Explained

A **Processor Architecture** or **Instruction Set Architecture (ISA)** is the **blueprint** that defines:

- ✅ What instructions the CPU supports (e.g., `add`, `load`, `jump`)
- ✅ How data is stored and accessed (registers, memory layout)
- ✅ The binary format of instructions
- ✅ Rules for interacting with the CPU

### Popular ISAs:
- **x86** — Used in most PCs and servers (Intel/AMD)
- **ARM** — Dominates mobile and embedded markets
- **RISC-V** — New, open-source competitor, growing rapidly

---

### 💬 Assembly Language

**Assembly Language** is a low-level, human-readable way to write programs that map directly to the ISA’s instructions.

Each **assembly instruction** corresponds to **one machine code instruction**.

### 🧾 Example: RISC-V Assembly

```assembly
add x1, x2, x3      # x1 = x2 + x3
lw x5, 0(x6)        # Load word from memory at address in x6 into x5
sw x5, 4(x6)        # Store word from x5 into memory at x6 + 4
```
## 4. <u>Instruction Execution Cycyle</u><br>

### RISC-V Instruction Execution Cycle

This README explains the **5-stage instruction execution cycle** used in **RISC‑V processors**, focusing on how instructions are fetched, decoded, executed, and written back in a pipeline architecture.

---

### What Is the Instruction Execution Cycle?

In RISC‑V, every instruction passes through five key stages:

1. **FETCH**
2. **DECODE**
3. **EXECUTE**
4. **WRITEBACK**
5. **REPEAT**

This is also known as the **RISC‑V 5-Stage Pipeline**. Each instruction flows through these stages like an item in an assembly line.

---

### 🔧 The Five Stages (RISC-V Context)

### 1. 🧾 FETCH  
**Goal:** Get the next instruction from memory.

- The **Program Counter (PC)** points to the instruction.
- Memory returns the instruction as binary.

✅ Example:
```asm
add x5, x6, x7
```
### 2. 🧠 DECODE

Goal: Understand what the instruction is and which operands it uses.<br>
   - Control unit decodes:
     - Operation type (e.g., ADD)
     - Instruction format (e.g., R-type)
     - Registers involved

✅ Decoded:

```asm
Add contents of x6 and x7, result into x5.
```

### 3. ⚙️ EXECUTE

Goal: Perform the actual operation in the ALU.<br>
   - Arithmetic: ALU performs computation
   - Branch: calculate target address
   - Memory: compute effective address
   
✅ Here:

```asm
x5 = x6 + x7
```

### 4. 🧮 WRITEBACK

Goal: Save the result into the destination register. <br>
   - Result from ALU is written back into x5.

✅ Write:

```asm 
Store the sum into x5.
```

### 5. 🔁 REPEAT

Goal: Move on to the next instruction.
   - Increment the Program Counter (PC)
   - Repeat the cycle for the next instruction.

## 5. Performance Metrices

Here’s a clear breakdown of Clock Speed (Frequency), Instructions Per Cycle (IPC), and how they contribute to overall CPU performance:

### 1. Clock Speed (Frequency)

   - <b>Definition:</b>
Clock speed is the rate at which a processor’s clock generates pulses. These pulses synchronize the CPU's operations.

   - <b>Units:</b> Usually measured in Hertz (Hz), commonly Gigahertz (GHz) for modern CPUs.

   - <b>What it means:</b>
If a CPU has a clock speed of 3 GHz, it means the clock ticks 3 billion times per second. Each tick corresponds to a potential opportunity for the CPU to perform part of an instruction.

### 2. Instructions Per Cycle (IPC)

   - <b>Definition:</b>
IPC is the average number of instructions a CPU can execute in one clock cycle.

   - <b>What it means:</b>
A higher IPC means the CPU can do more work in each clock tick. For example, if a CPU has an IPC of 2, it can process 2 instructions per clock cycle.

### 3. How They Contribute to Performance

  - <b>CPU Performance Formula:</b>

    `Performance ∝ Clock Speed × IPC` 


   - <b>Explanation:</b>
The overall performance depends on both how fast the clock ticks (clock speed) and how many instructions the CPU completes per tick (IPC).

   - <b>For example:</b>

       - CPU A: 3 GHz clock speed, IPC = 1 → 3 billion instructions/sec

       - CPU B: 2.5 GHz clock speed, IPC = 1.5 → 3.75 billion instructions/sec<br>
Even though CPU B has a slower clock, it performs better because of higher IPC.

### Summary
| Term                             | What It Measures                | Impact on Performance                                  |
| -------------------------------- | ------------------------------- | ------------------------------------------------------ |
| **Clock Speed**                  | How many cycles per second      | More cycles = potentially more work done               |
| **Instructions per Cycle (IPC)** | How many instructions per cycle | More instructions per cycle = more work done per cycle |
