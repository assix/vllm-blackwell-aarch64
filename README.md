vLLM-Blackwell-ARM64

Optimized vLLM build for NVIDIA Grace Blackwell (GB10) and ARM64. This repository contains pre-compiled SM12.1 kernels, specifically tuned for CUDA 13.0 on DGX Spark systems.
Why this exists

Standard vLLM wheels are typically built for x86_64 and older CUDA versions (12.1/12.4). Compiling natively for the GB10 on aarch64 can take over 20 minutes. This repository provides a pre-compiled wheel to leverage Blackwell's coherent unified memory immediately.
Highlights

    Target Architecture: SM 12.1 (Blackwell GB10).

    OS: Ubuntu 24.04 (Noble Numbat).

    CUDA Support: 13.0+.

    Hardware: Optimized for Grace Neoverse cores and LPDDR5x unified memory.

Installation
1. Download the Wheel

Download the latest .whl from the Releases page.

2. Setup Environment & Install

```bash
export LD_LIBRARY_PATH=/usr/local/cuda-13.0/lib64:$LD_LIBRARY_PATH export PATH=/usr/local/cuda-13.0/bin:$PATH
Install the pre-compiled wheel

pip install vllm-0.16.0rc1.dev84+gcd86fff38-cp310-cp310-linux_aarch64.whl
```

Quick Start: Run GPT-OSS-120B

To launch an OpenAI-compatible API server on your DGX Spark:

```bash python3 -m vllm.entrypoints.openai.api_server

--model openai/gpt-oss-120b

--tensor-parallel-size 1

--gpu-memory-utilization 0.90

--trust-remote-code
```

Building from Source

If you prefer to build natively on your own Grace Blackwell node:

```bash
export CUDA_HOME=/usr/local/cuda-13.0 export MAX_JOBS=16 export TORCH_CUDA_ARCH_LIST="12.1" pip install -e .
```
License

This project is licensed under the Apache License 2.0. See the LICENSE file for details.
