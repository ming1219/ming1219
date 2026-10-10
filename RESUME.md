**English** | [简体中文](RESUME.zh-CN.md) · [← Profile](https://github.com/ming1219)

# Resume · ming1219

**M.S. student (3rd year), Southwest University of Science and Technology**

I build LLM agents, executable task environments and automated evaluation for tool-using models.

## Projects

### EMBench: evaluation framework for tool-using agents · Author · [GitHub](https://github.com/ming1219/EMBench)

The point is the workflow, not a fixed question set: a repeatable path from *task design* → *verification* → *grading* → *failure analysis*.

- **Task spec**: each task is a directory holding an instruction, a declarative verifier, a reference trajectory and negative examples. Any agent plugs in through a standard trajectory format
- **Verifiers from reusable checks**: trajectory matching, argument constraints, numeric tolerance and coverage/consistency. Answers must name an actually generated candidate, so matching a keyword isn't enough. Results are reported as multi-dimensional scores plus pass@k / pass^k
- **Grading that can be trusted**: missing evidence fails the task instead of being skipped. Every result is bound to the agent that produced it, so scores can't be inherited across agents. Confidence intervals count tasks, not repeated trials. Self-validation: references must pass; empty, truncated, evidence-stripped and known-wrong trajectories must fail
- **Hardened through external review**: fixed the loopholes a reviewer found (refusals counted as recommendations, passing without evidence, inherited scores, inflated intervals). Each one is now a regression test (55 tests)

### EM-Agent: LLM agent for molecular design · Creator & main developer

- **Agent**: LangGraph single-agent ReAct loop and multi-agent planner–executor workflow; an MCP tool server with 29 domain tools; PubChem grounding so the model can't invent structures; multiple LLM providers (GLM / DeepSeek / Qwen)
- **Evaluation and failure analysis**: trajectory-level grading of tools, arguments and results. Multi-agent raised candidate completion **40% → 94%** (DeepSeek-V4-Flash). Root causes found and fixed: state leaking across runs, list arguments passed as JSON strings, redundant tool calls
- **Engineering**: FastAPI + SSE backend and React + TypeScript frontend, with auth, billing and a concurrency cap; deployed to 2 production Linux servers (nginx, systemd); Dockerfile

## Skills

Python, TypeScript, Bash · LangGraph, MCP, FastAPI · RDKit · Linux, nginx, systemd, Docker, Git · AI coding assistants, with results verified by tests
