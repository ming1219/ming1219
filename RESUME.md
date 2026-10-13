**English** | [简体中文](RESUME.zh-CN.md) · [← Profile](https://github.com/ming1219)

# Wen Jian

I am a third-year M.S. student at Southwest University of Science and Technology, and from 2024 to 2026 I was in a joint training program with a research institute. I work on **LLM agents**, **executable task environments** and **automated evaluation**: building agents that get real work done with domain tools, and turning tasks into environments a program can verify.

I also work on molecular AI: de novo molecular design with reinforcement learning, and property prediction by fine-tuning pre-trained 3D molecular models, published as first author in *Information Sciences* and at CSCWD 2026.

[GitHub](https://github.com/ming1219) · [EM-Agent (live)](https://em.dkelab.cn/)

## Experience

- **2024 – 2026**　Joint-training graduate student, Research Institute
  - Designed and built the molecular-design agent [EM-Agent](https://github.com/ming1219/EM-Agent) (see Projects), now deployed online
- **Current**　M.S. student (3rd year), Southwest University of Science and Technology

## Publications

- **De Novo Design of Energetic Molecules via Domain-Guided Reinforcement Learning and Unified 3D Representation**
  *Information Sciences*　published　first author　[code](https://github.com/ming1219/EMDP)
- **U3R-EMPP: Unified 3D Representations via Pre-trained Models for Energetic Molecule Property Prediction**
  CSCWD 2026　published　first author (CCF-C)　[code](https://github.com/ming1219/U3R-EMPP)

## Projects

### Security Task Factory: CVE-based task environments for LLM evaluation and RL

- **Reviving real CVEs**: diff the vulnerable and fixed source, then strip the patch's defenses with a minimal reverse patch on the official Docker image
- **LLM task creation**: injection recipes drive an LLM that emits environment build scripts, task statements and private reference solutions
- **Review gates**: the untouched target fails, the reference solution solves, wrong submissions fail, re-grading agrees; plus three-layer leak scanning
- **Grading**: byte-compared flags and recipe-defined partial scores, usable both as an evaluation success criterion and as an RL reward
- **Difficulty calibration**: difficulty calibrated by 3 × 2-hour model attempts with trajectory reading; 10+ classes of container environment failures turned into build rules

### QA Studio: training-data generation platform for LLMs · [Live](https://qa.dkelab.cn)

Built a chain-of-thought (CoT) QA dataset under industry guidance: designed and implemented a multi-stage data generation system connected to LLMs, producing 100k+ high-quality QA pairs.

- **Six-stage visual pipeline**: preprocessing → generation → validation → evaluation → filtering → export, turning raw corpora into high-quality QA training sets
- **Pipeline engine**: resumable runs and re-running any stage; a global thread pool with fair rate limiting turns the LLM calls of all 6 stages into batched concurrent requests, fixing submissions under multiple users
- **Quality control**: domain-specific CoT construction, multi-layer quality gates, and a per-question-type retry loop
- **Traceability**: configuration center, prompt versioning and snapshot tracing

### EMBench: evaluation framework for tool-using agents · Author · [GitHub](https://github.com/ming1219/EMBench)

A repeatable workflow: *task design* → *verification* → *grading* → *failure analysis*.

- **Task spec**: each task is a directory holding an instruction, a declarative verifier, a reference trajectory and negative examples. Any agent plugs in through a standard trajectory format
- **Verifiers from reusable checks**: trajectory matching, argument constraints, numeric tolerance and coverage/consistency. Every recommended molecule must come from the generated set; mentioning a generated molecule or matching a keyword isn't enough. Results are reported as multi-dimensional scores plus pass@k / pass^k
- **Grading that can be trusted**: missing or `null` evidence fails the task instead of being skipped. Every result is bound to the agent that produced it and to the task version it was graded against. Confidence intervals count tasks, not repeated trials. Self-validation: references must pass; empty, truncated, evidence-stripped, `null`-filled and known-wrong trajectories must fail
- **Runs in Docker via Harbor**: each task starts the agent's container plus a fixture MCP tool server that replays recorded results and logs every call on its own side. The grader reads that log with a key injected only at verification time, so agents can't fake their trajectories. Verified end to end: the reference solution scores 1.0, a blank submission 0.0
- **Hardened through external review**: fixed the loopholes a reviewer found: deferrals or off-list molecules counted as recommendations, passing without evidence or with `null` evidence, inherited scores, stale task versions on resume, inflated intervals. Each one is now a regression test (80 tests)

### EM-Agent: LLM agent for molecular design · Creator & main developer · [GitHub](https://github.com/ming1219/EM-Agent) · [Live](https://em.dkelab.cn/)

- **Agent**: LangGraph single-agent ReAct loop and a multi-agent planner–executor that runs subtasks in parallel (`Send()` map-reduce); an MCP tool server with 26+ domain tools (structure lookup, property prediction, generation, retrosynthesis, crystal-structure search); PubChem grounding so the model can't invent structures; multiple LLM providers (GLM / DeepSeek / Qwen)
- **Evaluation and failure analysis**: trajectory-level grading of tools, arguments and results. Multi-agent raised candidate completion **40% → 94%** (DeepSeek-V4-Flash). Root causes found and fixed: state leaking across runs, list arguments passed as JSON strings, redundant tool calls
- **Engineering**: FastAPI + SSE backend and React + TypeScript frontend, with auth, billing and a concurrency cap; deployed to 2 production Linux servers (nginx, systemd); Dockerfile

### Molecular AI models: generation and property prediction

- **EMDP** · [GitHub](https://github.com/ming1219/EMDP) · paper in *Information Sciences*: de novo molecular design. Transfer learning of a REINVENT prior on domain molecules, then staged reinforcement learning with domain-knowledge scoring (substructure counts, geometric-mean aggregation, scaffold diversity filter). 5,000 sampled molecules are scored by a fine-tuned Uni-Mol v2 (164M) multi-task model on 8 properties, then Pareto-screened across energy, stability (BDE) and synthesizability (SA, SYBA) down to 24 candidates
- **U3R-EMPP** · [GitHub](https://github.com/ming1219/U3R-EMPP) · paper at CSCWD 2026: property prediction by fine-tuning a pre-trained 3D molecular representation model (Uni-Mol) on 7 properties at once; datasets merged from three published sources (3DCNN, MDGNN, q-RASPR); 10-fold scaffold-split cross-validation

## Honors

- Silver Medal, 2023 ACM Programming Contest, Sichuan Province
- Outstanding Graduate of Sichuan Province (class of 2023)
- University First-Class Scholarship
- Graduate Academic Scholarship (third class)

## Skills

Python, TypeScript, Bash · LangGraph, MCP, FastAPI · Docker, Harbor · CVE reproduction, patch diffing · Uni-Mol, REINVENT, RDKit · Linux, nginx, systemd, Git · AI coding assistants, with results verified by tests

## Interests

ACM-ICPC-style competitive programming
