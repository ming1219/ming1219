## `cat` `ming1219_info`

**Wen Jian (文健)** · M.S. @ [Southwest University of Science and Technology](https://www.swust.edu.cn/), graduating 2027 · joint training @ a research institute `2024 – 2026`

I build LLM agents, put them to work on executable tasks, and check with programs whether they really finished the job.

- **Built and deployed** [**EM-Agent**](https://github.com/ming1219/EM-Agent), a molecular-design agent in online use ([live](https://em.dkelab.cn/))
- **Measured**: on 3 multi-objective design tasks, multi-agent raised the share of candidates analyzed end to end from **40% to 94%** (DeepSeek-V4-Flash, about 2.3× the wall-clock time)
- **Published** two first-author papers on molecular AI: *Information Sciences*, CSCWD 2026

[My Resume (English)](https://github.com/ming1219/ming1219/blob/main/RESUME.md) | [我的简历（中文）](https://github.com/ming1219/ming1219/blob/main/RESUME.zh-CN.md)

### 🛠 Projects

- **Security Task Factory**: turns real CVEs into evaluation and RL tasks. Automated gates prove every task before use: the untouched target fails, the reference solves it, wrong submissions fail
- [**EMBench**](https://github.com/ming1219/EMBench) `MIT`: open-source framework that grades agents with executable checks and keeps the evidence for re-checking. Its final-answer check caught a multi-agent run that never gave the user a conclusion
- [**EM-Agent**](https://github.com/ming1219/EM-Agent): molecular-design agent with single- and multi-agent LangGraph workflows over 26+ MCP tools; FastAPI + React, deployed on Linux
- [**QA Studio**](https://qa.dkelab.cn): training-data platform for LLMs. A six-stage pipeline builds chain-of-thought QA data; 100k+ pairs produced
- [**EMDP**](https://github.com/ming1219/EMDP): molecular design with reinforcement learning and a fine-tuned 3D property model
- [**U3R-EMPP**](https://github.com/ming1219/U3R-EMPP): multi-property prediction by fine-tuning a pre-trained 3D molecular model

### 🧰 Stack

`Python` `TypeScript` `LangGraph` `LangChain` `MCP` `FastAPI` `SSE` `SQLite` `React` `Vite` `Docker` `Uni-Mol` `REINVENT` `RDKit` `Linux` `nginx` `systemd` `Git`
