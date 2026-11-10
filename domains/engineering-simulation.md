# Engineering Simulation (FEA and CFD)

**Problem:** go from a physical question (*"will this bracket bend under 500 N?"*, *"how does air flow around this housing?"*) to a numerical simulation that answers it.

← Back to the [main README](../README.md)

Simulations are the usual metric for the [improvement loop](../README.md#the-improvement-loop): generate variants, simulate them, keep the best.

---

## Recommended tool

The right tool depends on the physics:

| Kind of problem | Recommended tool | Language | Why |
|---|---|---|---|
| **Structural analysis** (stress, deformation, vibration) | [**CalculiX**](http://www.calculix.de/) | Abaqus-style input files, driven from Python | Open source, compatible with the widely known Abaqus format, and already used by agent tooling (text-to-cad). |
| **General multiphysics** (heat, elasticity, custom equations) | [**FEniCSx**](https://fenicsproject.org/) | Python | The equations are written almost as in mathematics, so a model can set up new problems, not just fill in templates. |
| **Fluid dynamics** (CFD) | [**OpenFOAM**](https://www.openfoam.com/) | Text case files (dictionaries) | The most widely used open-source CFD package. Each case is a folder of text files, and `forceCoeffs` gives drag and lift directly. |
| **Crash and impact** | [**OpenRadioss**](https://openradioss.org/) | Input decks | Open-source explicit solver for crashes, open-sourced by Altair. |

**Why this approach works:** a simulation is already a program: geometry, mesh, material properties, loads, boundary conditions and solver settings. All of it can be written as text, run headless, and checked against known solutions or physical limits.

---

## Alternatives

| Tool | When to use it |
|---|---|
| [COMSOL](https://www.comsol.com/) (Java/MATLAB API) | Commercial multiphysics. The FEABench benchmark uses it. |
| Ansys (PyAnsys) | Commercial, industry standard. Python API available. |
| [Gmsh](https://gmsh.info/) | Meshing from Python, used together with the solvers above. |
| [Elmer](https://www.elmerfem.org/) | Open-source multiphysics alternative. |
| Adjoint solvers ([DAFoam](https://dafoam.github.io/), [SU2](https://su2code.github.io/)) | Optimizing a shape with many parameters at once. |
| Surrogate models ([DrivAerNet++](https://github.com/Mohamedelrefaie/DrivAerNet)) | Screening thousands of car shapes in seconds before running full CFD. |

---

## Benchmarks

**Best model right now:** there is no public leaderboard yet. The reference results are in the FEABench paper.

| Benchmark | What it measures | Results |
|---|---|---|
| **FEABench** (Google) | Solving physics and engineering problems by operating COMSOL Multiphysics through its API. 15 verified problems plus 200 parsed from tutorials. In the paper, no model fully and correctly solved any problem. | No public leaderboard · [Paper](https://arxiv.org/abs/2504.06260) · [Code](https://github.com/google/feabench) |
| FoamBench (CFDLLMBench) | Setting up and running OpenFOAM simulations from natural-language descriptions (110 basic and 16 advanced cases). | No public leaderboard · [Paper](https://arxiv.org/abs/2509.20374) |
| ShapeBench | 103 aerodynamic shape-optimization problems, comparing LLM-driven and classical optimizers. Far from saturation. | No public leaderboard · [Paper](https://arxiv.org/abs/2605.20763) |

---

## Used in practice

- [Mazda + OpenAI](https://openai.com/index/accelerating-engineering-for-the-physical-world/) (Nov 2026): the model generates front-end shapes, simulates the airflow of dozens of variants and refines the best ones to reduce drag; the collaboration also covers crash safety.
- [OpenAI's hardware teams](https://openai.com/index/accelerating-engineering-for-the-physical-world/) use Codex to prepare simulations and FEA with much less manual work.
