# 5-Stage Pipelined RISC-V CPU

![ISA](https://img.shields.io/badge/ISA-RISC--V_RV32I-b51800)
![EDA](https://img.shields.io/badge/EDA-Logisim--Evolution-005f9e)
![Verification](https://img.shields.io/badge/Verification-Python_%26_Bash-success)

## 📌 Overview
This repository contains a fully functional **32-bit 5-stage pipelined RISC-V processor** designed and simulated in Logisim Evolution. 

The project implements the core RISC-V 32I Instruction Set Architecture (ISA) and features a complete datapath and control unit capable of handling data and control hazards through hardware-based solutions. This project was developed based on the framework from UC Berkeley's CS61C architecture course.

## 🏗️ Architecture & Design
The CPU implements a classic 5-stage pipeline to maximize instruction throughput.

### Pipeline Stages
1.  **Instruction Fetch (IF):** Retrieves instructions from instruction memory; handles PC updates.
2.  **Instruction Decode (ID):** Decodes instructions, reads from the Register File, and generates immediates (ImmGen).
3.  **Execute (EX):** Performs arithmetic/logic operations via the ALU and resolves branch conditions.
4.  **Memory (MEM):** Handles read/write operations to data memory.
5.  **Write Back (WB):** Commits results back to the Register File.

### Key Features
* **Hazard Handling:**
    * **Structural Hazards:** Resolved via separate Instruction and Data memories (Harvard Architecture).
    * **Data Hazards:** Implemented a **Forwarding Unit** to bypass results from MEM and WB stages directly to the EX stage, minimizing stalls.
    * **Control Hazards:** Implemented a **Hazard Detection Unit** to insert "nop" bubbles or flush the pipeline during branch mispredictions or load-use dependencies.
* **Modular Design:**
    * `alu.circ`: Arithmetic Logic Unit supporting add, sub, and, or, xor, slt, sll, srl, sra, mul, etc.
    * `regfile.circ`: 32x32 Register File with dual-read/single-write ports.
    * `branch_comp.circ`: Branch comparator for conditional logic (BEQ, BNE, BLT, BGE, etc.).
    * `imm_gen.circ`: Immediate generator for I, S, B, U, and J type instructions.

## 🧪 Verification & Testing
The reliability of the CPU is verified through a rigorous testing suite located in the `tests/` directory.

* **Unit Testing:** Individual sub-circuits (ALU, RegFile) verified against truth tables.
* **Integration Testing:** Full pipeline tested against reference outputs using valid RISC-V assembly binaries.
* **Automated Test Suite:**
    * Uses `test.sh` (Bash) and Python harnesses to automate the simulation of assembly files.
    * Verifies register states and memory outputs at every clock cycle.

## 🚀 How to Run
**(Note: Requires Logisim Evolution)**

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/GrantAyala/RV32I-Pipelined-Core](https://github.com/GrantAyala/RV32I-Pipelined-Core)
    cd RV32I-Pipelined-Core
    ```
2.  **Run the test suite:**
    ```bash
    ./test.sh
    ```
3.  **Manual Simulation:**
    Open `cpu/cpu.circ` in Logisim Evolution to visualize the datapath and signal propagation in real-time.

## 🛠️ Skills & Technologies
* **Computer Architecture:** Deep understanding of Von Neumann vs. Harvard architectures, pipelining, and ISA design.
* **Digital Logic Design:** combinational and sequential logic, multiplexers, latches, and flip-flops.
* **Hardware Verification:** Writing automated test scripts in **Python** and **Bash** to validate hardware logic.
* **Assembly Language:** Writing and debugging RISC-V assembly.

## 📜 Acknowledgments
* Based on the project specifications from **CS61C (Great Ideas in Computer Architecture)** at UC Berkeley.

---
*Author: Grant Ayala*
