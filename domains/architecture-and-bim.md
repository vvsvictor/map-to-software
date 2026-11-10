# Architecture and Building Information Modeling (BIM)

**Problem:** go from a brief or a floor plan to a building model with walls, floors, doors, windows, spaces and their properties, which architects, engineers and builders can use.

← Back to the [main README](../README.md)

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**IfcOpenShell**](https://ifcopenshell.org/) (Python) |
| **Engine** | IfcOpenShell + [Bonsai](https://bonsaibim.org/) (the open-source BIM add-on for Blender) |
| **Output** | **IFC** (Industry Foundation Classes), the open ISO standard for BIM |
| **Leaderboard** | None public yet (see Benchmarks) |

**Why:**

- **IFC is the open standard** (ISO 16739) that Revit, ArchiCAD, Tekla and most BIM tools can import and export.
- IfcOpenShell lets you **create, query and edit** IFC models from Python, which LLMs write well.
- Models can be **checked automatically**: element counts, spatial relationships, properties and rule-based checks.
- It is **open source** and runs locally.

---

## Alternatives

| Tool | Language | When to use it |
|---|---|---|
| Revit API ([pyRevit](https://github.com/pyrevitlabs/pyRevit)) | C# / Python | Offices that work in Revit. Requires a Revit licence and runs on Windows. |
| [Grasshopper](https://www.grasshopper3d.com/) + Python (Rhino) | Python / visual | Parametric and computational design of forms and façades. |
| SketchUp Ruby API | Ruby | Quick massing and conceptual models. |

---

## Benchmarks

**Best model right now:** there is no public leaderboard yet. The most complete comparison of models is in the BIM-Edit paper.

| Benchmark | What it measures | Results |
|---|---|---|
| **BIM-Edit** | Natural-language editing of IFC models: create, update and delete tasks on realistic and synthetic buildings. Best model about 49.5%; no model fully solves more than 3.4% of tasks. | No public leaderboard · [Paper](https://arxiv.org/abs/2606.20146) |
| BIBIMBAP | 100 text-to-BIM programming tasks (create, read, update, delete). Best baseline about 50%. EC3 2026. | No public leaderboard · [Paper](https://ec-3.org/publication/ec32026_271/) |
| IFC-Copilot / MCP4IFC | MCP server on IfcOpenShell + Bonsai, with its own benchmark and results on IFC-bench-v1 (querying). | No public leaderboard · [Paper](https://tsesterh.github.io/papers/IFC-Copilot.pdf) |
