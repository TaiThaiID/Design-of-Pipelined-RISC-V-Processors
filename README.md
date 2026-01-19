# RISC-V Pipelined Processor (RV32I)

A 5-stage pipelined RISC-V processor implementation supporting the RV32I instruction set architecture, featuring hazard detection and data forwarding mechanisms.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Implementation Models](#implementation-models)
- [Performance Results](#performance-results)
- [Verification](#verification)
- [Demo](#demo)
- [References](#references)

---

## 🎯 Overview

This project implements a **5-stage pipelined RISC-V processor** based on the **RV32I** instruction set architecture. The design focuses on understanding pipeline hazards and implementing solutions through hazard detection and data forwarding techniques. Two distinct models were developed to compare performance trade-offs between different hazard handling strategies.

**Key Highlights:**
- ✅ Complete RV32I ISA support (40+ instructions)
- ✅ 5-stage pipeline architecture
- ✅ Comprehensive hazard detection unit
- ✅ Data forwarding mechanism
- ✅ Memory-mapped I/O system
- ✅ Verified with automated ISA test suite

---

## ✨ Features

### Instruction Set Support
The processor supports the complete RV32I base integer instruction set:

- **Arithmetic**: `ADD`, `ADDI`, `SUB`
- **Logical**: `AND`, `ANDI`, `OR`, `ORI`, `XOR`, `XORI`
- **Shift**: `SLL`, `SLLI`, `SRL`, `SRLI`, `SRA`, `SRAI`
- **Compare**: `SLT`, `SLTI`, `SLTU`, `SLTIU`
- **Load**: `LW`, `LH`, `LHU`, `LB`, `LBU`
- **Store**: `SW`, `SH`, `SB`
- **Branch**: `BEQ`, `BNE`, `BLT`, `BLTU`, `BGE`, `BGEU`
- **Jump**: `JAL`, `JALR`
- **Upper Immediate**: `LUI`, `AUIPC`

### I/O Peripherals
- 17 Red LEDs (mapped at `0x1000_0000`)
- 8 Green LEDs (mapped at `0x1000_1000`)
- 8 Seven-segment displays (mapped at `0x1000_2000` and `0x1000_3000`)
- LCD display support (mapped at `0x1000_4000`)
- 18 Switches for input (mapped at `0x1001_0000`)

---

## 🏗️ Architecture

### Pipeline Stages

The processor implements a classic 5-stage pipeline:

1. **Instruction Fetch (IF)**: Fetches instruction from instruction memory
2. **Instruction Decode (ID)**: Decodes instruction and reads register file
3. **Execute (EX)**: Performs ALU operations or address calculation
4. **Memory Access (MEM)**: Accesses data memory for load/store operations
5. **Write Back (WB)**: Writes results back to register file

### Block Diagram

### Model 1: Non-Forwarding Pipeline
![datapath_model1](https://github.com/user-attachments/assets/8ce29320-c51e-469e-a430-843e7363e086)

### Model 2: Forwarding Pipeline
![datapath_model2](https://github.com/user-attachments/assets/bfd76c91-b6bc-474e-93a3-0ddbebad37f8)

---

## 🔧 Implementation Models

Two pipeline models were implemented to demonstrate different approaches to handling data hazards:

### Model 1: Non-Forwarding Pipeline

**Strategy**: Insert pipeline stalls (bubbles) to resolve data hazards.

**Characteristics:**
- Simple control logic
- No forwarding paths required
- Easier to verify and debug

**Hazard Handling:**
- Load-use hazard: 1 cycle stall
- Data hazard: 2 cycle stall
- Control hazard: Flush on branch/jump

### Model 2: Forwarding Pipeline

**Strategy**: Forward data from later pipeline stages to resolve hazards.

**Characteristics:**
- Reduced pipeline stalls
- Forwarding paths from EX/MEM and MEM/WB to EX stage
- More complex control logic

**Hazard Handling:**
- Load-use hazard: 1 cycle stall (unavoidable)
- Data hazard: Resolved by forwarding
- Control hazard: Flush on branch/jump

---

## 📊 Performance Results

Performance comparison between the two implemented models:

### Performance Metrics

| Model           | IPC   | Mispred Rate (%) |
|-----------------|-------|------------------|
| Non-forwarding  | 0.43  |  90.52%          |
| Forwarding      | 0.62  |  90.52%          |

### Analysis

**IPC Comparison:**
- Forwarding model achieves **0.62 higher IPC** compared to non-forwarding
- Performance gain primarily from reduced data hazard stalls
---

## ✅ Verification

The processor has been verified using a comprehensive ISA test suite covering all RV32I instructions.

![model1](https://github.com/user-attachments/assets/5e0ba8af-79ae-4da9-82c9-696ec2ba8c58)
![model2](https://github.com/user-attachments/assets/93eee50d-2b4b-4b7f-b10a-f98f9ef36727)

---

## 🎬 Demo

**Demo Features:**
- LED output display
- Seven-segment display control
- Switch input handling
- Real-time instruction execution

### Hardware Demo


---

## 📚 References

- D. A. Patterson and J. L. Hennessy, Computer Organization and Design: The Hardware/Software Interface, RISC-V Edition, Morgan Kaufmann, 2020.
- S. L. Harris and D. Harris, Digital Design  and Computer Architecture: RISC-V Edition,  Morgan Kaufmann, 2021.
- Dan Garcia, "Pipeline I", Great Ideas in Computer Architecture (Machine Structures), University of California, Berkeley, 2020.
- Dan Garcia, " Pipeline II: Control Hazards, Data Hazards I", Great Ideas in Computer Architecture (Machine Structures), University of California, Berkeley, 2020.
- Dan Garcia, " Pipeline III: More Hazards, Superscalar Processors", Great Ideas in Computer Architecture (Machine Structures), University of California, Berkeley, 2020.

---

