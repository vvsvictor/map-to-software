# Laboratory Automation and Life Sciences

**Problem:** go from an experiment (*"run a serial dilution across a 96-well plate"*, *"set up a PCR"*) to a protocol that a liquid-handling robot executes, and from molecules or data to analyses that can be checked.

← Back to the [main README](../README.md)

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**Opentrons Python Protocol API**](https://docs.opentrons.com/) |
| **Engine** | Opentrons simulator (`opentrons_simulate`) → Opentrons OT-2 / Flex robots |
| **Output** | A protocol executed by the robot, with a full log of every step |
| **Leaderboard** | [LABBench2 (BenchLM)](https://benchlm.ai/benchmarks/labbench2) · [ChemBench](https://huggingface.co/spaces/jablonkagroup/ChemBench-Leaderboard) |

**Why:**

- A protocol is a **Python file**: labware, pipettes, volumes and steps are all code.
- Protocols can be **simulated** before running, which catches errors such as missing tips, wrong volumes or impossible moves, without wasting reagents.
- Opentrons robots are **affordable and open**, and widely used in academic labs.
- Opentrons itself already offers **OpentronsAI**, a tool that generates protocols with this API.

**For molecules:** [**RDKit**](https://www.rdkit.org/) (Python) with **SMILES** strings is the standard way to represent and compute on molecules as text.

---

## Alternatives

| Tool | When to use it |
|---|---|
| [PyLabRobot](https://github.com/PyLabRobot/pylabrobot) | Hardware-independent Python control of liquid handlers from several vendors (Hamilton, Tecan, Opentrons...). |
| Vendor scripting (Hamilton Venus, Tecan Fluent) | Labs with existing commercial robots. Mostly proprietary formats. |
| [Benchling](https://www.benchling.com/) | Not a protocol language, but where many labs keep their experiments and data. |

---

## Benchmarks

**Best model right now:** [LABBench2 on BenchLM](https://benchlm.ai/benchmarks/labbench2) (a third-party aggregator) for practical biology research, and the [ChemBench leaderboard](https://huggingface.co/spaces/jablonkagroup/ChemBench-Leaderboard) for chemistry.

| Benchmark | What it measures | Results |
|---|---|---|
| **LAB-Bench / LABBench2** (FutureHouse) | Practical biology research tasks, including **ProtocolQA** (finding and fixing errors in published protocols). LABBench2 is the newer version with more than 1,900 tasks. | [**Leaderboard (BenchLM)**](https://benchlm.ai/benchmarks/labbench2) · [Paper](https://arxiv.org/abs/2407.10362) |
| **ChemBench** | Chemistry knowledge and reasoning compared with human chemists, over 2,700 questions. | [**Leaderboard**](https://huggingface.co/spaces/jablonkagroup/ChemBench-Leaderboard) · [GitHub](https://github.com/lamalab-org/chembench) |
| BioProBench | Biological protocols: question answering, step ordering, error correction, protocol generation and reasoning. | No public leaderboard · [Paper](https://arxiv.org/abs/2505.07889) |
| BioBasicsBench (OpenAI + Ligo) | 100 routine wet-lab tasks with raw data: gel images, colony plates, microscopy, instrument exports and sequencing files. Checks whether agents interpret the data correctly, spot errors and recognise when evidence is not enough. | Results only for OpenAI models · [Results](https://openai.com/index/measuring-how-ai-agents-handle-wet-lab-science/) |
