## `cat` `ming1219_info`

**Wen Jian (文健)** · M.S. student @ [Southwest University of Science and Technology](https://www.swust.edu.cn/) `3rd year` · joint training @ a research institute `2024 – 2026`

I build LLM agents, executable task environments and evaluation frameworks for tool-using models

Built: [**EM-Agent**](https://github.com/ming1219/EM-Agent), an LLM agent for molecular design and chemistry computation ([live](https://em.dkelab.cn/)). It has 26+ MCP tools and single- and multi-agent LangGraph workflows, and runs on 2 production servers

Open-sourced: [**EMBench**](https://github.com/ming1219/EMBench), a framework for building verifiable agent tasks. It takes you from task spec to declarative verifier to self-validation to grading and re-grading, and runs tasks for any agent in Docker with server-side tool-call logs

Found: multi-agent raised candidate completion **40% → 94%** on multi-objective design tasks (DeepSeek-V4-Flash). The outcome checks also caught a multi-agent run that returned the planner's internal instruction as the final answer

Shipped: **security task environments from real CVEs** — reviving patched CVEs on official Docker images with minimal reverse patches, driving an LLM creator with injection recipes, and gating every task with program-run proofs: untouched target fails, reference solution solves, wrong submissions fail, re-grading agrees

[My Resume (English)](https://github.com/ming1219/ming1219/blob/main/RESUME.md) | [我的简历（中文）](https://github.com/ming1219/ming1219/blob/main/RESUME.zh-CN.md)

### 🛠 Projects

| Project | What it is |
| ------- | ---------- |
| [**EMBench**](https://github.com/ming1219/EMBench) `MIT` | Evaluation framework for tool-using agents: task-as-directory spec, reusable declarative checks, self-validating verifiers, evidence-strict grading, results bound to the agent and task version that produced them, task-level pass@k / pass^k, offline re-grading; Docker runs with a fixture MCP tool server and server-side call logs |
| [**EM-Agent**](https://github.com/ming1219/EM-Agent) · [live](https://em.dkelab.cn/) | Molecular-design agent: LangGraph single-agent ReAct and parallel planner–executor workflows, MCP tool server (26+ tools), FastAPI + SSE backend, React + TypeScript frontend, trajectory-level evaluation, deployed on Linux with nginx and systemd |
| **Security Task Factory** | CVE-based task pipeline for LLM eval & RL: diff vulnerable vs fixed source and strip the patch's defenses with a minimal patch on the official image; recipe-driven LLM creator emits env build scripts, task statements and private reference solutions; four automated gates (untouched target fails, reference solves, wrong submissions fail, stable re-grading) plus three-layer leak scanning; difficulty calibrated by 3×2h model attempts with trajectory reading; grading trusts only observable outcomes (flag byte-compare, recipe-defined partial scores), usable as eval success criteria and RL reward; resolved 10+ classes of container env failures into build rules |
| [**EMDP**](https://github.com/ming1219/EMDP) | De novo molecular design: REINVENT transfer learning + staged reinforcement learning with domain-knowledge scoring; fine-tuned Uni-Mol v2 (164M) multi-task property model; Pareto screening across energy, stability and synthesizability |
| [**U3R-EMPP**](https://github.com/ming1219/U3R-EMPP) | Molecular property prediction by fine-tuning a pre-trained 3D molecular representation model (Uni-Mol) on 7 properties; datasets merged from three published sources; 10-fold scaffold-split cross-validation |

### 🧰 Stack

`Python` `TypeScript` `LangGraph` `LangChain` `MCP` `FastAPI` `SSE` `SQLite` `React` `Vite` `Docker` `Uni-Mol` `REINVENT` `RDKit` `Linux` `nginx` `systemd` `Git`
