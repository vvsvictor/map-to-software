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
| **Benchmark** | [BenchCAD](https://benchcad.github.io/BenchCAD_webpage/) (CadQuery) |

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

## Agent tooling

| Tool | What it does |
|---|---|
| [**text-to-cad**](https://github.com/earthtojake/text-to-cad) ([website](https://www.texttocad.dev/)) | Open-source (MIT) plugin and skill bundle for coding agents (Claude Code, Codex, Cursor, Gemini and others). The agent writes **build123d** models, runs them and shows them in a CAD viewer. Exports STEP, STL, 3MF, GLB, DXF and PDF drawings. Also includes skills for KiCad boards, manufacturing checks, FEA stress checks (CalculiX), renders (Blender), 3D-print slicing and robot descriptions (URDF/SDF). |

---

## Benchmarks

| Benchmark | What it measures | Link |
|---|---|---|
| **BenchCAD** | Reading and writing **CadQuery** code for real mechanical parts: about 17,900 execution-verified programs across 106 part families from industrial standards (ISO, DIN, EN, ASME, IEC). Tasks: *Vision2Code* (images → CadQuery, scored by voxel IoU against the reference), *CodeEdit* (edit a program from an instruction), and numeric *Vision-QA* / *Code-QA*. Scoring is automatic, with no LLM judge. | [Project page and leaderboard](https://benchcad.github.io/BenchCAD_webpage/) · [Paper](https://arxiv.org/abs/2605.10865) |
| Text2CAD-Bench | Generating parametric CAD from text descriptions. | [Paper](https://arxiv.org/abs/2605.18430) |
| CADGenBench | CAD generation leaderboard hosted on Hugging Face. | [GitHub](https://github.com/huggingface/cadgenbench) |

> **Best current model:** rankings change every few weeks, and third-party aggregators often disagree because they track different task variants and dates. Check the **[official BenchCAD leaderboard](https://benchcad.github.io/BenchCAD_webpage/)**.

---

## Used in practice

- [Robot designed entirely as build123d code written by Claude Opus, with a YAML spec for the global parameters and Fusion 360 used only as a viewer](https://x.com/observie/status/2106301475261423651) (@observie, Oct 2026).
- [Anthropic reports 83.5% on BenchCAD 2.1 for Claude Fable 5.2](https://www.anthropic.com/research/claude-electronics-design) (Nov 2026), as part of designing 3D-printable enclosures for electronic devices.
