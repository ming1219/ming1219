## Hi, I'm ming1219 👋

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

---

<details>
<summary><b>中文简历（点击展开）</b></summary>

## 你好，我是 ming1219 👋

我做**大模型智能体、可执行任务环境和自动化评测**，面向科学计算领域中需要调用工具的大模型。
工作覆盖完整闭环：设计任务和验证标准，搭建智能体能真正运行的环境，采集并验证工具调用轨迹，分析模型的失败案例，再驱动下一轮迭代。

**我关注的方向**

- **可验证的任务设计**：把真实的领域工作流整理成任务，给出清晰的指令、预期步骤和判定标准
- **可复现、可执行的运行环境**：工具服务、后端与部署，让智能体端到端地真实运行
- **轨迹数据与质量控制**：采集多步工具调用轨迹，并通过代码执行、领域归一化和数值容差来验证
- **评测与奖励设计**：成功判定、多维度打分、能自我检验的评测集；通过与否的二值判定可以直接作为奖励信号
- **失败分析**：比较不同模型和智能体架构，定位根因，迭代任务、提示词和环境

---

## 经历

### EMBench：面向化学工具调用智能体的开源评测集 · 2026 · 作者
[github.com/ming1219/EMBench](https://github.com/ming1219/EMBench)

- 把自己的智能体评测重构为独立的评测集：**9 类共 74 道题**，每道题是一个自包含目录（指令、声明式判分规则、参考轨迹、反例）
- 设计 **10 种可复用的检查类型**：有序轨迹匹配、参数约束、工具输出数值容差、候选覆盖与一致性、最终回答正确性、调用预算，以及自定义 Python 检查。替代了原来约 2200 行、每个实验单独手写的判分脚本
- 让题库**能自我检验**：参考轨迹必须通过，空轨迹、截断轨迹和已知错误轨迹必须失败。未知或拼错的参数会直接报错，并用变异测试确认坏题一定会被发现。共 38 个单元测试
- 二值判定背后有多维度得分（工具选择、参数、数值结果、覆盖、一致性、回答、效率）；支持 **pass@k、pass^k** 和 Wilson 置信区间；统计 token 和耗时；支持断点续跑，以及对历史轨迹离线重新判分
- 用 **111 次历史判定**验证迁移结果：**110 次一致**，唯一的差异是旧判分器漏掉的一个真实缺陷
- 以 MIT 许可证开源，配有中英双语、面向初学者的文档

### EM-Agent：分子设计与化学计算智能体 · 2026 · 创建者、主要开发者

**智能体与工具环境**
- 设计两套 LangGraph 工作流：单智能体 ReAct 循环；多智能体「规划者–执行者」图，带执行子图和对话摘要
- 搭建包含 **29 个领域工具的 MCP 工具服务**：结构查询与校验、2D/3D 渲染、性质预测、分子生成、逆合成（AiZynthFinder）、晶体结构搜索、统计分析。所有工具统一返回 JSON 结果、对错误分类，并校验输入（长度、批量、时间上限）
- 新增 PubChem 检索工具和 RDKit 预校验，防止模型编造分子结构和 CAS 号
- 通过 OpenAI 兼容接口接入多家大模型（GLM、DeepSeek、Qwen），其中包括一个解析 DeepSeek DSML 工具调用格式的包装层；支持每个用户自配模型（自带 key）

**评测与失败分析**
- 搭建轨迹级评测，覆盖 9 类实验：判工具选择与顺序、参数（SMILES 规范化、别名归一、浮点容差）和数值结果；对输出随机的生成类任务，改用行为式评分（覆盖率、自洽性、合规性）
- 做单/多智能体对比和跨模型对比，并把结果做成图：
  - 多目标设计任务上，多智能体把候选完成率**从 40% 提升到 94%**（DeepSeek-V4-Flash），耗时约为单智能体的 2.3 倍
  - 设计流水线上，多智能体 **100%**、单智能体 **67%**（GLM-5.1），工具调用约多一倍
  - Qwen3-32B 得分 0%，原因是它用占位符填写工具参数
- 定位并修复失败根因：评测运行之间 checkpointer 状态泄漏；模型把列表参数传成 JSON 字符串；冗余工具调用（收紧提示词）。新加的结果检查还发现了多智能体把规划者的内部指令当作最终回答输出的问题

**数据**
- 编写脚本，把分子性质数据表（密度、熔点、热分解温度、PubChem 化合物、SemDB）转换为约 **8.1 万条 JSONL 训练数据**
- 编写 38 题智能体评测集的生成器，覆盖单工具、顺序与并行多工具调用、条件推理、异常处理和端到端工作流

**后端、产品与运维**
- 把 Streamlit 原型重构为 **FastAPI 后端（SSE 流式输出）** 加 React + TypeScript（Vite）前端；会话、消息、用户和 LangGraph checkpoint 持久化到 SQLite
- 实现 bcrypt + HMAC token 认证、用户注册与按次积分计费、全局并发上限（asyncio 信号量，防止内存耗尽）、使用统计大屏（ECharts）、Ketcher 分子编辑器和 3D 分子渲染
- 清除仓库中泄露的 API key 和默认密码，把敏感配置移出版本控制
- **部署到两台生产 Linux 服务器**：
  - 一台 2 核 2 GB 的 Ubuntu 24.04 主机：swap、带内存上限的 systemd 服务、nginx 负责静态文件和反向代理
  - 一台已有 Caddy 的共享主机：nginx 走独立端口，通过固定一组可用的依赖版本解决 glibc 兼容问题
- 编写分步部署手册；编写带健康检查的 Dockerfile 和 docker-compose 配置

---

## 技能

| | |
|---|---|
| **编程语言** | Python（主力）、TypeScript、SQL、Bash |
| **智能体与大模型** | LangGraph、LangChain、MCP（FastMCP）、工具调用、提示词设计、OpenAI 兼容接口（GLM、DeepSeek、Qwen） |
| **评测** | 轨迹级判分、任务成功判定、pass@k / pass^k、失败分析 |
| **前后端** | FastAPI、SSE、SQLite、React、Vite、ECharts |
| **基础设施** | Linux（Ubuntu）、nginx、systemd、conda、Docker、Git |
| **领域** | RDKit、PubChem、化学信息学 |
| **AI 辅助开发** | 日常使用 AI 编程助手完成开发、调试和测试，并通过运行代码和测试验证结果 |

</details>
