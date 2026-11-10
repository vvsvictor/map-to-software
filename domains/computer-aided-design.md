# Computer-Aided Design (CAD)

**Problem:** go from a description, a drawing or reference images to a precise, manufacturable 3D model of a mechanical part or assembly.

← Back to the [main README](../README.md)

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**CadQuery**](https://github.com/CadQuery/cadquery) or [**build123d**](https://github.com/gumyr/build123d) (Python) |
| **Engine** | [Open CASCADE Technology (OCCT)](https://dev.opencascade.org/), an exact B-rep geometry kernel |
| **Output** | **STEP** (exchange with other CAD tools and manufacturing), **STL** / 3MF (3D printing) |
| **Leaderboard** | [BenchCAD](https://benchcad.com/leaderboard) |

**Why:**

- They are **plain Python**, the language LLMs write best.
- They are **parametric**: dimensions are variables, so one program describes a whole family of parts.
- OCCT is an **exact (B-rep) geometry kernel**, the same one behind FreeCAD, so the output is real CAD geometry with exact surfaces, not just a mesh.
- They export **STEP**, the standard format that any CAD tool (Fusion 360, SolidWorks, FreeCAD, Onshape...) and any manufacturer can open.
- Both are **open source** and run locally, with no API limits.

**CadQuery or build123d?** Both use the same kernel and produce the same kind of geometry.

- Choose **CadQuery** when you want to compare models against the main public benchmark (BenchCAD is written in CadQuery) or need its larger body of existing examples.
- Choose **build123d** for new projects. Its API is more modern and "Pythonic", and the main agent tooling ([text-to-cad](https://github.com/earthtojake/text-to-cad)) and recent real-world uses are built on it.

---

## Alternatives

| DSL | Language | Geometry kernel | When to use it |
|---|---|---|---|
| [OpenSCAD](https://openscad.org/) | OpenSCAD language | CGAL / Manifold (mesh) | Simple parts for 3D printing. Mesh-based, so STEP export and exact geometry are limited. |
| [KCL](https://zoo.dev/docs/kcl) | KCL (Zoo) | Zoo's own engine | If you work inside Zoo's text-to-CAD platform. |
| [FeatureScript](https://cad.onshape.com/FsDoc/) | FeatureScript | Parasolid (Onshape) | Custom features inside Onshape. Cloud only, and the Onshape API has usage limits that make heavy agent use hard. |

---

## Benchmarks

**Best model right now:** [BenchCAD leaderboard](https://benchcad.com/leaderboard). It has two boards: models with the standard harness, and agents with their own harness (for example Claude Code or Codex).

| Benchmark | What it measures | Results |
|---|---|---|
| **BenchCAD** | Reading and writing **CadQuery** code for real mechanical parts: about 17,900 execution-verified programs across 106 part families from industrial standards (ISO, DIN, EN, ASME, IEC). Tasks: images → CadQuery (scored by voxel IoU), editing programs, and numeric questions about parts. Scores are re-graded by the authors, not self-reported. | [**Leaderboard**](https://benchcad.com/leaderboard) · [Paper](https://arxiv.org/abs/2605.10865) |
| CADGenBench | CAD generation benchmark hosted on Hugging Face. | [**Leaderboard**](https://huggingface.co/spaces/HuggingAI4Engineering/CADGenBench) · [GitHub](https://github.com/huggingface/cadgenbench) |
| Text2CAD-Bench | 600 human-curated text-to-parametric-CAD examples at four difficulty levels. | No public leaderboard yet (planned) · [Paper](https://arxiv.org/abs/2605.18430) |

---

## Used in practice

- [Robot designed entirely as build123d code written by Claude Opus, with a YAML spec for the global parameters and Fusion 360 used only as a viewer](https://x.com/observie/status/2106301475261423651) (@observie, Oct 2026).
- [Anthropic reports 83.5% on BenchCAD 2.1 for Claude Fable 5.2](https://www.anthropic.com/research/claude-electronics-design) (Nov 2026), as part of designing 3D-printable enclosures for electronic devices.
- [OpenAI's hardware teams](https://openai.com/index/accelerating-engineering-for-the-physical-world/) (Nov 2026) use Codex to create and modify CAD models, turn 3D designs into production-ready 2D drawings and prepare FEA simulations. In the same article, two people designed a complete test device (enclosure, PCB and firmware) with GPT-6 Astra in under a week, although it needed several review rounds before manufacturing because the model missed tolerances and assembly details.
- [Chip Ganassi Racing + OpenAI](https://openai.com/index/accelerating-engineering-for-the-physical-world/) (Nov 2026): turning **3D scans of existing parts into editable CAD models and 2D manufacturing drawings**, useful when the original design files are missing. CGR engineers check accuracy and manufacturability.
