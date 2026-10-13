**English** | [简体中文](RESUME.zh-CN.md) · [← Profile](https://github.com/ming1219)

# Wen Jian
Email：1282295467@qq.com

M.S. student at Southwest University of Science and Technology, graduating in 2027. From 2024 to 2026 I was a joint-training student at a research institute.

My research is on **evaluating LLM agents and building training data for LLMs**. I have designed and implemented an evaluation framework for agents, built an LLM evaluation set from real CVEs, and built chain-of-thought training data for LLMs.

I also work on molecular AI, publishing as first author in *Information Sciences* and at CSCWD 2026.

[GitHub](https://github.com/ming1219) · [EM-Agent (live)](https://em.dkelab.cn/)

## Experience

- **2024 – 2026**　Joint-training graduate student, Research Institute
  - Designed and built the molecular-design agent [EM-Agent](https://github.com/ming1219/EM-Agent) (see Projects), now deployed online
- **Graduating 2027**　M.S. student, Southwest University of Science and Technology

## Publications

- **De Novo Design of Energetic Molecules via Domain-Guided Reinforcement Learning and Unified 3D Representation**
  *Information Sciences*　published　first author　[code](https://github.com/ming1219/EMDP)
- **U3R-EMPP: Unified 3D Representations via Pre-trained Models for Energetic Molecule Property Prediction**
  CSCWD 2026　published　first author (CCF-C)　[code](https://github.com/ming1219/U3R-EMPP)

## Projects

### Security Task Factory · an LLM evaluation set built from real CVEs

Rebuilds real, already-patched vulnerabilities as standardized tasks, and a program decides whether each task is solved. Every task has a reproducible environment, exactly one solution and calibrated difficulty. The set can be used to evaluate LLMs and also as training environments and reward signals for reinforcement learning.

- **Reviving the vulnerability**　Starting from the official Docker image, a minimal reverse patch brings a fixed CVE back. Depending on how the software is shipped, one of three injection methods is used, namely removing the fix, enabling a vulnerable configuration or exposing a native defect
- **Generating the task**　An injection recipe is first written by hand for each vulnerability, stating its mechanism, how to build it and the single solution. A sandboxed LLM then generates the full task package in one pass, with environment orchestration scripts, a two-layer task statement and a private reference solution. The package is also exported in a general evaluation format compatible with terminal-bench
- **Proving it works**　Every generated task must run its reference solution successfully on an image built for real. An independent model then checks four things, namely that the task is solvable, resists cheating, has no shortcut and can be solved without blind guessing
- **Calibrating difficulty**　The models under test solve the tasks in the same environments, and difficulty is set by their pass rate. Reading the trajectories then confirms that each failure is a genuine one and not caused by an environment fault

### EMBench: evaluation framework for tool-using agents · Author · [GitHub](https://github.com/ming1219/EMBench)

An open-source framework that grades agents with executable checks and keeps the run evidence needed to re-check every result.

- **Executable checks**: each task is a directory holding an instruction, declarative checks and a reference solution. Before a grader is trusted, it must pass the reference and fail empty, truncated and known-wrong runs
- **Evidence that can be re-checked**: missing or `null` evidence fails the task. Each result is tied to the agent and task version that produced it. In Docker, the tool server keeps its own call log, so an agent cannot fake its trajectory. Every loophole found in external review is now a regression test
- **Checking outcomes, not just steps**: re-grading 15 earlier runs (111 judgments) agreed with the old grader 110 times. The one difference was a real bug that step-level checks had missed: a multi-agent run ended on the planner's internal instruction and never gave the user a conclusion

### EM-Agent: LLM agent for molecular design · Creator & main developer · [GitHub](https://github.com/ming1219/EM-Agent) · [Live](https://em.dkelab.cn/)

Researchers describe a molecular-design goal in plain language; the agent calls domain tools and returns analyzed, ranked candidates. Deployed online.

- **Agent**: LangGraph single-agent ReAct loop, and a multi-agent planner–executor that runs subtasks in parallel. 26+ domain tools served over MCP. Names are resolved through PubChem so the model cannot invent structures
- **Measured effect**: on 3 multi-objective design tasks (4–5 candidates each, DeepSeek-V4-Flash), the share of candidates analyzed end to end (property prediction, performance calculation, retrosynthesis) rose from **40% with a single agent to 94% with multi-agent**, at about 2.3× the wall-clock time
- **Engineering**: FastAPI + SSE backend, React + TypeScript frontend, auth and billing; running on 2 production Linux servers (nginx, systemd)

### QA Studio: training-data generation platform for LLMs · [Live](https://qa.dkelab.cn)

Turns raw corpora into chain-of-thought QA training data. Built under industry guidance; produced 100k+ QA pairs.

- **Pipeline**: six visual stages (preprocess → generate → validate → evaluate → filter → export). Runs can resume, and any stage can be re-run
- **Concurrency**: a global thread pool with fair rate limiting batches the LLM calls, so several users can submit at once
- **Quality**: multi-layer quality gates with retries per question type; prompt versions and snapshots make every output traceable

### Molecular AI models

- **EMDP** · [GitHub](https://github.com/ming1219/EMDP) · *Information Sciences*: designs new molecules with reinforcement learning guided by domain knowledge, then screens them with a fine-tuned Uni-Mol v2 property model and Pareto ranking (energy, stability, synthesizability): 5,000 samples down to 24 candidates
- **U3R-EMPP** · [GitHub](https://github.com/ming1219/U3R-EMPP) · CSCWD 2026: predicts 7 molecular properties at once by fine-tuning a pre-trained 3D molecular model (Uni-Mol); evaluated with 10-fold scaffold-split cross-validation on data merged from three published sources

## Honors

- Silver Medal, 2023 ACM Programming Contest, Sichuan Province
- Outstanding Graduate of Sichuan Province (class of 2023)
- University First-Class Scholarship
- Graduate Academic Scholarship (third class)

## Skills

Python, TypeScript, Bash · LangGraph, MCP, FastAPI · Docker, Harbor · CVE reproduction, patch diffing · Uni-Mol, REINVENT, RDKit · Linux, nginx, systemd, Git · AI coding assistants, with results verified by tests

## Interests

ACM-ICPC-style competitive programming
