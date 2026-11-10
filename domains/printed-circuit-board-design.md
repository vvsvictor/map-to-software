# Printed Circuit Board (PCB) Design

**Problem:** go from a set of requirements or component datasheets to a complete printed circuit board (schematic, footprints, placement and routing) ready for manufacturing.

← Back to the [main README](../README.md)

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**Zener**](https://github.com/diodeinc/pcb), built on [Starlark](https://github.com/bazelbuild/starlark) |
| **Engine** | Diode's `pcb` command-line tool + [KiCad](https://www.kicad.org/) |
| **Output** | KiCad projects → Gerber and fabrication files |
| **Benchmark** | [PCB Gym](https://neurips.cc/virtual/2026/loc/paris/161602) (design intent given as Zener code) |

Zener is a PCB hardware description language from [Diode Computers](https://diode.computer/). It is built on Starlark, the Python-like configuration language Google created for Bazel. You describe components, nets, interfaces and reusable hierarchical modules in `.zen` files, and `pcb build` turns them into KiCad projects. It is open source (MIT license).

**Why:**

- Circuits become **code modules** that can be reused and configured with parameters, like functions.
- Starlark looks like Python, so LLMs write it easily.
- Designs live in **Git** and go through pull-request review like any other code.
- The output is standard **KiCad**, so the usual checks (ERC/DRC) and the rest of the open-source toolchain still work.
- It is the format used by **PCB Gym**, so models can be evaluated on the same representation you use in production.
- A **Claude Code skill** for the language is available in the [diodeinc/pcb](https://github.com/diodeinc/pcb) repository.

---

## Alternatives

| DSL | Language | Output | When to use it |
|---|---|---|---|
| [atopile](https://atopile.io/) | `ato` language | KiCad | Code-first electronics with modules, parameters and constraint solving (for example, picking component values from requirements). |
| [SKiDL](https://github.com/devbisme/skidl) | Python | Netlist (KiCad) | You only need the schematic/netlist as Python. Layout is still done in KiCad. |
| [tscircuit](https://tscircuit.com/) | TypeScript / React | Schematic, PCB, Gerber | You prefer a TypeScript/React ecosystem. |
| KiCad Python scripting | Python | KiCad | Automating changes to existing KiCad boards rather than describing new ones. |

---

## Benchmarks

| Benchmark | What it measures | Link |
|---|---|---|
| **PCB Gym** | **Agentic PCB layout**: placement and routing together, on real open-source hardware designs from 2 to 12 copper layers. Design intent is given as **Zener** code. Graded with deterministic checks plus a rubric-based agent grader. Anthropic describes it as Diode's placement and routing benchmark. | [NeurIPS 2026 workshop paper](https://neurips.cc/virtual/2026/loc/paris/161602) |
| PCB-Bench | LLMs and multimodal LLMs on PCB placement, routing and design understanding (text, images and real design files). ICLR 2026. | [Project page](https://digailab.github.io/PCB-Bench/) |
| PCBWorld | Open-source, KiCad-based routing environment and benchmark (PCBWorld-Bench) that compares LLM, RL and rule-based routers. | [Paper](https://arxiv.org/abs/2607.05915) |
| HWE-Bench | Whether LLMs can design board-level **schematics**. | [Paper](https://arxiv.org/abs/2603.18102) |
| PCB-QA | Question answering over PCB design files. | [Paper](https://arxiv.org/abs/2606.23704) |

---

## Used in practice

- [Anthropic and Diode Computers: Claude Fable 5.2 designed three working devices end to end](https://www.anthropic.com/research/claude-electronics-design) (Nov 2026): schematics, placement and routing in KiCad, enclosures, firmware and parts lists. Diode built the boards directly from Claude's files. Reported 69% on PCB Gym (vs. 25% for Fable 5). The devices are prototypes, not validated for mass production or certification.
- [A user reports Fable 5.2 completing a PCB layout on its own in about 1.5 hours](https://x.com/jlcjak/status/2119917708846260729) (@jlcjak, Nov 2026). Single user report, not a controlled evaluation.
