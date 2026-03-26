# Cross-ISA GEMM Benchmark

This project performs a system-level performance analysis of GEMM (matrix multiplication)
across heterogeneous compute platforms, focusing on the performance gap between emerging
RISC-V systems and mature ARM/GPU architectures.

## Platforms

- ARM NEON (Qualcomm RB3/RB5)
- ARM Cortex-A72 (Raspberry Pi 4)
- RISC-V Scalar (VisionFive 2)
- RISC-V Vector (RVV via QEMU emulation)
- GPU (Jetson CUDA)

## Objectives

- Quantify performance differences across ISAs and accelerators
- Analyze vectorization efficiency (NEON vs projected RVV)
- Understand memory hierarchy impact (cache + bandwidth limits)
- Study compiler behavior (LLVM auto-vectorization vs intrinsics)
- Decompose performance into compute vs data-movement components

## Key Insight Areas

This project is not just benchmarking—it aims to answer:

- Where is performance lost across architectures?
- Is the bottleneck compute, memory, or vectorization?
- How much of the gap is due to ISA vs compiler vs microarchitecture?
- What optimizations close the gap?

## Methodology

- Implement GEMM kernels:
  - Naive (baseline)
  - Cache-blocked
  - Vectorized (NEON / RVV)

- Profile using:
  - `perf` (ARM + RISC-V)
  - CUDA profiling tools (Jetson)

- Measure:
  - GFLOPS
  - IPC
  - Cache misses
  - Memory bandwidth

- Compare across matrix sizes and data types

## Important Notes

- VisionFive 2 does not support RVV; it is used as a scalar RISC-V baseline
- RVV results are obtained via QEMU and are used for:
  - functional validation
  - instruction-level analysis
  - trend estimation (not cycle-accurate performance)

## Repository Structure
src/ Core GEMM implementations
include/ Headers (GEMM, timing utilities)
scripts/ Benchmark + profiling scripts
results/ Raw data and plots
analysis/ Notebooks and performance breakdown


## Goal

Build a deep, cross-layer understanding of performance across:
ISA → Compiler → Kernel → Hardware → Workload

This project is intended for systems engineers working on:
- AI acceleration
- compiler optimization
- heterogeneous compute systems

## Roadmap

### Core Compute
- [ ] Baseline GEMM (naive)
- [ ] Cache-blocked GEMM
- [ ] NEON vectorization
- [ ] RVV implementation (QEMU)
- [ ] Cross-platform benchmarking (ARM, RISC-V, GPU)

### Profiling & Analysis
- [ ] perf-based profiling (IPC, cache, memory)
- [ ] Roofline-style analysis (compute vs memory bound)
- [ ] LLVM codegen analysis (auto-vectorization vs intrinsics)

### Data Movement & System-Level Analysis
- [ ] Measure memory bandwidth vs compute throughput
- [ ] Analyze data movement cost (memcpy vs compute time)
- [ ] Simulate pipeline: data transfer + compute overlap

### RDMA / SmartNIC Exploration (Advanced)
- [ ] Model RDMA-style data transfer vs CPU memcpy
- [ ] Simulate zero-copy data pipelines
- [ ] Analyze impact of offloading data movement from CPU
- [ ] Explore eBPF / SmartNIC-style compute + data path integration

### Synthesis
- [ ] Cross-ISA performance gap decomposition
- [ ] Compute vs data-movement bottleneck breakdown
- [ ] Optimization opportunities across ISA, compiler, and system