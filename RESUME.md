**English** | [简体中文](RESUME.zh-CN.md) · [← Profile](https://github.com/ming1219)

# Resume · ming1219

I build **LLM agents, executable task environments and automated evaluation** for tool-using models in scientific computing.
My work spans the whole loop: designing tasks and verification criteria, building environments agents can actually run in, collecting and validating tool-call trajectories, and analyzing model failures to drive the next iteration.

**What I focus on**

- **Task design with verifiable criteria**: turning real domain workflows into tasks with clear instructions, expected steps and pass/fail standards
- **Reproducible, executable environments**: tool servers, backends and deployments that agents run against end to end
- **Trajectory data and quality control**: capturing multi-step tool-call trajectories and validating them with code execution, domain normalization and numeric tolerances
- **Evaluation and reward design**: success criteria, multi-dimensional scoring and self-validating benchmarks whose binary verdicts can double as reward signals
- **Failure analysis**: comparing models and agent architectures, locating root causes, and iterating on tasks, prompts and environments

---

## Experience

### EMBench: open-source benchmark for tool-using chemistry agents · 2026 · Author
[github.com/ming1219/EMBench](https://github.com/ming1219/EMBench)

- Re-engineered my agent evaluation into a standalone benchmark: **74 tasks in 9 families**, one self-contained directory per task (instruction, declarative verifier, reference trajectory, negative examples)
- Designed **10 reusable check types**: ordered trajectory matching, argument constraints, numeric tolerance on tool outputs, candidate coverage and consistency, final-answer correctness, call budget, plus a custom-Python escape hatch. They replaced ~2.2k lines of per-experiment grading scripts
- Made the suite **self-validating**: every reference trajectory must pass, while empty, truncated and known-wrong trajectories must fail. Unknown or misspelled parameters are rejected, and mutation tests confirm that broken tasks are caught. 38 unit tests
- Binary pass/fail backed by multi-dimensional scores (tool choice, arguments, numeric results, coverage, consistency, answer, efficiency); **pass@k, pass^k** and Wilson confidence intervals; token and wall-clock cost; resumable runs and offline re-grading of past trajectories
- Validated the migration against **111 historical judgments: 110 agreed**. The single difference was a real defect the old grader had missed
- Released under MIT with bilingual, beginner-friendly documentation

### EM-Agent: LLM agent for molecular design and chemistry computation · 2026 · Creator and main developer

**Agent and tool environment**
- Designed two LangGraph workflows: a single-agent ReAct loop, and a multi-agent planner–executor graph with executor subgraphs and conversation summarization
- Built an **MCP tool server with 29 domain tools**: structure lookup and validation, 2D/3D rendering, property prediction, molecule generation, retrosynthesis (AiZynthFinder), crystal-structure search, and statistics. All tools return unified JSON results, classify errors and validate inputs (length, batch and time limits)
- Added a PubChem grounding tool and RDKit pre-validation so the model stops inventing structures and CAS numbers
- Integrated several LLM providers through OpenAI-compatible APIs (GLM, DeepSeek, Qwen), including a wrapper that parses DeepSeek's DSML tool-call format; added per-user model configuration (bring your own key)

**Evaluation and failure analysis**
- Built a trajectory-level evaluation over 9 experiment families. It grades tool selection and order, arguments (canonical SMILES, alias normalization, float tolerance) and numeric results. For stochastic generation tasks it uses behavioral scoring (coverage, self-consistency, compliance)
- Ran single- vs multi-agent and cross-model comparisons and turned the results into figures:
  - multi-agent raised candidate completion on multi-objective design tasks **from 40% to 94%** (DeepSeek-V4-Flash), at about 2.3× wall-clock time
  - on the design pipeline, **100% vs 67%** (GLM-5.1) at about 2× tool calls
  - Qwen3-32B scored 0% because it filled tool arguments with placeholders
- Traced failures to root causes and fixed them: checkpointer state leaking across evaluation runs, models passing list arguments as JSON strings, redundant tool calls (tightened prompts). The outcome checks also surfaced a multi-agent run returning the planner's internal instruction instead of a final answer

**Data**
- Wrote scripts that convert molecular property tables (density, melting point, decomposition temperature, PubChem compounds, SemDB) into **~81k JSONL records** for model training
- Wrote a generator for a 38-item agent benchmark covering single, sequential and parallel tool calls, conditional reasoning, error handling and end-to-end workflows

**Backend, product and operations**
- Rebuilt the Streamlit prototype into a **FastAPI backend with SSE streaming** and a React + TypeScript (Vite) frontend. Sessions, messages, users and LangGraph checkpoints are persisted in SQLite
- Added bcrypt + HMAC-token authentication, user registration with per-call credit billing, a global concurrency cap (asyncio semaphore) to prevent OOM, a usage-analytics dashboard (ECharts), the Ketcher structure editor and 3D molecule rendering
- Removed leaked API keys and default passwords from the repository and moved secrets out of version control
- **Deployed to two production Linux servers**:
  - an Ubuntu 24.04 host with 2 CPU cores and 2 GB RAM, using swap, systemd with a memory limit, and nginx for static files and the reverse proxy
  - a shared host behind an existing Caddy server, with nginx on a separate port and a pinned dependency set to work around glibc compatibility issues
- Wrote step-by-step deployment runbooks, plus a Dockerfile and docker-compose setup with a health check

---

## Skills

| | |
|---|---|
| **Languages** | Python (primary), TypeScript, SQL, Bash |
| **Agents and LLMs** | LangGraph, LangChain, MCP (FastMCP), tool calling, prompt design, OpenAI-compatible APIs (GLM, DeepSeek, Qwen) |
| **Evaluation** | Trajectory-level grading, task success criteria, pass@k / pass^k, failure analysis |
| **Backend and frontend** | FastAPI, SSE, SQLite, React, Vite, ECharts |
| **Infrastructure** | Linux (Ubuntu), nginx, systemd, conda, Docker, Git |
| **Domain** | RDKit, PubChem, cheminformatics |
| **AI-assisted development** | Daily use of AI coding assistants for development, debugging and testing, with results verified by running code and tests |
