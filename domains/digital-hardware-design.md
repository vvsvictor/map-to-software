# Digital Hardware Design (Chips and FPGAs)

**Problem:** go from a specification (*"a UART receiver at 115200 baud"*, *"a 4-stage RISC-V pipeline"*) to working digital logic that can run on an FPGA or be manufactured as a chip.

← Back to the [main README](../README.md)

Digital hardware is one of the most natural domains for this approach: chip designers already describe circuits as code, in **Hardware Description Languages (HDLs)**, and have done so for decades.

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**SystemVerilog / Verilog**](https://en.wikipedia.org/wiki/SystemVerilog) (RTL) |
| **Engine** | Simulation: [Verilator](https://www.veripool.org/verilator/) or [Icarus Verilog](https://steveicarus.github.io/iverilog/) · Synthesis: [Yosys](https://yosyshq.net/yosys/) · Layout: [OpenROAD](https://theopenroadproject.org/) (chips) or [nextpnr](https://github.com/YosysHQ/nextpnr) (FPGAs) |
| **Output** | Netlist → FPGA bitstream or chip layout (GDSII) |
| **Leaderboard** | [HWE Bench](https://hwebench.com/v2.html) (complete CPU) · [TuRTLe](https://huggingface.co/spaces/HPAI-BSC/TuRTLe-Leaderboard) (RTL generation) |

**Why:**

- It is the **industry standard**: every FPGA and chip toolchain accepts it, so there is far more training data than for any alternative.
- The verification loop is excellent: **testbenches** and simulation give exact pass/fail results, and synthesis reports area, timing and power.
- A complete **open-source flow** exists (Verilator/Icarus → Yosys → OpenROAD/nextpnr), so an agent can go from code to a real layout locally.

---

## Alternatives

| DSL | Language | When to use it |
|---|---|---|
| [VHDL](https://en.wikipedia.org/wiki/VHDL) | VHDL | Projects or companies that already use it (common in Europe, aerospace and defense). |
| [Chisel](https://www.chisel-lang.org/) | Scala | Highly parametric generators (used for many RISC-V cores). Generates Verilog. |
| [Amaranth](https://amaranth-lang.org/) | Python | Python-based HDL, convenient for LLMs and smaller FPGA projects. Generates Verilog. |
| [SpinalHDL](https://spinalhdl.github.io/SpinalDoc-RTD/) | Scala | Similar to Chisel, popular for FPGA soft cores. |
| High-Level Synthesis (Vitis HLS, Bambu) | C / C++ | Accelerators described as algorithms rather than circuits. |

---

## Benchmarks

**Best model right now:** [HWE Bench leaderboard](https://hwebench.com/v2.html) for designing a complete CPU, and [TuRTLe leaderboard](https://huggingface.co/spaces/HPAI-BSC/TuRTLe-Leaderboard) for RTL generation across VerilogEval, RTLLM and other benchmarks.

| Benchmark | What it measures | Results |
|---|---|---|
| **HWE Bench** | Models design a **RISC-V CPU**; the score is the performance of the resulting CPU on held-out programs. Open-ended: there is no maximum score, so it does not saturate. | [**Leaderboard**](https://hwebench.com/v2.html) |
| **TuRTLe** | Unified evaluation of RTL generation that groups VerilogEval, RTLLM and other benchmarks (module completion, specification-to-RTL, line completion), checked with Icarus Verilog and Verilator. | [**Leaderboard**](https://huggingface.co/spaces/HPAI-BSC/TuRTLe-Leaderboard) · [Paper](https://arxiv.org/abs/2504.01986) |
| CVDP | NVIDIA problems written by hardware engineers: RTL generation, debugging, verification and specification tasks, including agentic ones. | No public leaderboard · [Paper](https://arxiv.org/abs/2506.14074) |
| VerilogEval | 156 problems from HDLBits, graded by simulation. | Included in TuRTLe · [Paper](https://arxiv.org/abs/2309.07544) |
| RTLLM | Design-level RTL generation from natural-language specifications. | Included in TuRTLe · [Paper](https://arxiv.org/abs/2308.05345) |
