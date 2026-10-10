## `cat` `ming1219_info`

**M.S. student** @ [Southwest University of Science and Technology](https://www.swust.edu.cn/) `3rd year`

I build LLM agents, executable task environments and evaluation frameworks for tool-using models

Built: **EM-Agent**, an LLM agent for molecular design and chemistry computation. It has 29 MCP tools and single- and multi-agent LangGraph workflows, and runs on 2 production servers

Open-sourced: [**EMBench**](https://github.com/ming1219/EMBench), a framework for building verifiable agent tasks. It takes you from task spec to declarative verifier to self-validation to grading and re-grading

Found: multi-agent raised candidate completion **40% → 94%** on multi-objective design tasks (DeepSeek-V4-Flash). The outcome checks also caught a multi-agent run that returned the planner's internal instruction as the final answer

[My Resume (English)](https://github.com/ming1219/ming1219/blob/main/RESUME.md) | [我的简历（中文）](https://github.com/ming1219/ming1219/blob/main/RESUME.zh-CN.md)

> 简历只列了能用代码、提交记录和评测数据证明的部分。做 Agent 的很多经验，比如怎么定义「任务成功」、怎么让评测本身不出错、怎么从失败轨迹里找根因，在简历上不容易体现，期望有所交流

### 🛠 Projects

| Project | What it is |
| ------- | ---------- |
| [**EMBench**](https://github.com/ming1219/EMBench) `MIT` | Evaluation framework for tool-using agents: task-as-directory spec, reusable declarative checks, self-validating verifiers, pass@k / pass^k, offline re-grading |
| **EM-Agent** `private` | Molecular-design agent: LangGraph single- and multi-agent workflows, MCP tool server (29 tools), FastAPI + SSE backend, React + TypeScript frontend, trajectory-level evaluation, deployed on Linux with nginx and systemd |

### 🧰 Stack

`Python` `TypeScript` `LangGraph` `LangChain` `MCP` `FastAPI` `SSE` `SQLite` `React` `Vite` `RDKit` `Linux` `nginx` `systemd` `Docker` `Git`
