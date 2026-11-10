# Mathematics (Formal Proofs)

**Problem:** go from a mathematical statement and its informal proof to a proof that a computer can check line by line, so there is no doubt that it is correct.

← Back to the [main README](../README.md)

This is the purest case of Map to Software: in a proof assistant, **a proof is a program** and checking the proof is compiling it. If it compiles, it is correct.

---

## Recommended tool

| | |
|---|---|
| **DSL** | [**Lean 4**](https://lean-lang.org/) with [**Mathlib**](https://leanprover-community.github.io/) |
| **Engine** | The Lean compiler / kernel |
| **Output** | A machine-checked proof |
| **Leaderboard** | [PutnamBench](https://trishullab.github.io/PutnamBench/leaderboard.html) |

**Why:**

- The verifier is **perfect**: the Lean kernel accepts a proof only if every step is correct. There is no way to "almost" pass, which makes it ideal for an AI feedback loop.
- **Mathlib** is a huge, actively maintained library of formalized mathematics, so the model does not start from zero.
- Lean is where most current AI-for-math work happens, so it has the most tooling and training data.

---

## Alternatives

| Tool | When to use it |
|---|---|
| [Isabelle/HOL](https://isabelle.in.tum.de/) | Large existing libraries (Archive of Formal Proofs), strong automation. |
| [Rocq (formerly Coq)](https://rocq-prover.org/) | Programming-language theory and verified software. |
| [Dafny](https://dafny.org/) | Verifying that programs meet their specifications rather than pure mathematics. |

---

## Benchmarks

**Best model right now:** [PutnamBench leaderboard](https://trishullab.github.io/PutnamBench/leaderboard.html), with separate tracks for Lean, Isabelle and Rocq. In Lean the top systems already solve every problem, so the featured ranking now orders them by cost.

| Benchmark | What it measures | Results |
|---|---|---|
| **PutnamBench** | Putnam competition problems formalized in Lean, Isabelle and Rocq. | [**Leaderboard**](https://trishullab.github.io/PutnamBench/leaderboard.html) · [GitHub](https://github.com/trishullab/PutnamBench) |
| miniF2F | 488 competition-level problems (AMC, AIME, IMO). Saturated: top systems solve almost all of it. | No maintained leaderboard · [GitHub](https://github.com/openai/miniF2F) |
| FATE | Formal benchmark series for frontier algebra at several difficulty levels. | No public leaderboard · [Paper](https://arxiv.org/abs/2511.02872) |

---

## Used in practice

- [Anthropic: Formalizing Fermat's Last Theorem](https://www.anthropic.com/news/formalizing-fermats-last-theorem) (Sep 2026).
