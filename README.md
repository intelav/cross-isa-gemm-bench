# Cross-ISA GEMM Benchmark

This project benchmarks and analyzes GEMM performance across:
- ARM NEON (Qualcomm RB3/RB5)
- RISC-V RVV (VisionFive)
- GPU (Jetson CUDA)

Focus areas:
- Vectorization efficiency (NEON vs RVV)
- Memory hierarchy impact (cache/memory bandwidth)
- Compiler behavior (LLVM auto-vectorization vs intrinsics)
- Cross-architecture performance scaling

The goal is to build a system-level understanding of compute vs data-movement bottlenecks across heterogeneous accelerators.
