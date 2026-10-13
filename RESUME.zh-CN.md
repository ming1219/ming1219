[English](RESUME.md) | **简体中文** · [← 主页](https://github.com/ming1219)

# 文健 · Wen Jian
邮箱：1282295467@qq.com

西南科技大学硕士研究生，2027 年毕业；2024 – 2026 年在研究院联合培养。

我的工作是**构建 Agent，让它执行真实任务，再用程序验证它是否真正完成。** 

我也做分子 AI，相关工作以第一作者发表于 *Information Sciences* 和 CSCWD 2026。

[GitHub](https://github.com/ming1219) · [EM-Agent 在线访问](https://em.dkelab.cn/)

## 经历

- **2024 – 2026**　联合培养研究生，研究院
  - 设计并开发分子设计智能体 [EM-Agent](https://github.com/ming1219/EM-Agent)（见下方项目），已部署上线
- **2027 年毕业**　硕士研究生，西南科技大学

## 论文

- **De Novo Design of Energetic Molecules via Domain-Guided Reinforcement Learning and Unified 3D Representation**
  *Information Sciences*　已发表　第一作者（新锐一区 TOP，中科院二区）　[代码](https://github.com/ming1219/EMDP)
- **U3R-EMPP: Unified 3D Representations via Pre-trained Models for Energetic Molecule Property Prediction**
  CSCWD 2026　已发表　第一作者（CCF-C）　[代码](https://github.com/ming1219/U3R-EMPP)

## 项目

### Security Task Factory：基于真实 CVE 的大模型评测与强化学习任务

把已修复的真实漏洞做成能由程序判定是否完成的任务，用于评测大模型，也可作为强化学习的奖励。

- **构建任务**：在官方 Docker 镜像上用最小的反向补丁复现 CVE；由注入配方驱动 LLM，生成环境构建脚本、题面和不公开的参考解
- **证明任务可用**：四道自动审核（未作修改的目标必须失败、参考解必须能解出、错误提交必须失败、重复判分结果一致），另有泄露扫描；判分只认可观测的结果，例如逐字节比对 flag
- **标定难度**：用模型做 3 × 2 小时的试做，并阅读轨迹；把 10 多类反复出现的容器故障沉淀为构建规则

### EMBench：工具调用智能体评测框架 · 作者 · [GitHub](https://github.com/ming1219/EMBench)

开源的智能体评测框架：用可执行的检查验证任务结果，并保留可供复核的运行证据。

- **可执行的检查**：每道题是一个目录，包含指令、声明式检查和参考解。判分程序先要通过自检才能使用：参考解必须通过，空的、截断的和已知错误的运行必须失败
- **证据可复核**：缺少证据或证据为 `null` 就判不通过；每条成绩都绑定产生它的 agent 和题目版本；在 Docker 中由工具服务自己记录调用，agent 无法伪造轨迹。外部评审发现的每个漏洞都已变成回归测试
- **检查结果，而不只检查步骤**：用新判分程序重判 15 份历史结果（111 次判定），110 次与旧版一致；唯一的差异是一个只看步骤时漏掉的真实缺陷：多智能体以 planner 的内部指令收尾，没有给用户结论

### EM-Agent：分子设计智能体 · 创建者、主要开发者 · [GitHub](https://github.com/ming1219/EM-Agent) · [在线访问](https://em.dkelab.cn/)

科研人员用自然语言描述分子设计目标，智能体调用领域工具，返回经过分析和排序的候选分子。已部署上线。

- **智能体**：LangGraph 单智能体 ReAct，以及并行执行子任务的多智能体「规划者–执行者」工作流；26 个以上领域工具通过 MCP 提供；名称经 PubChem 解析，防止模型编造分子结构
- **效果**：在 3 道多目标设计题上（每题 4–5 个候选，DeepSeek-V4-Flash），完整走完分析流程（性质预测、性能计算、逆合成）的候选比例，**单智能体为 40%，多智能体为 94%**，代价是耗时约为 2.3 倍
- **工程**：FastAPI + SSE 后端，React + TypeScript 前端，含认证和计费；运行在 2 台生产 Linux 服务器上（nginx、systemd）

### QA Studio：大模型训练数据生成平台 · [在线访问](https://qa.dkelab.cn)

把原始语料加工成 CoT 问答训练数据。在企业指导下完成，累计产出 10 万+ 条问答数据。

- **流水线**：六个可视化阶段（预处理 → 生成 → 校验 → 评估 → 过滤 → 导出），支持断点续跑和任意阶段重跑
- **并发**：全局线程池加公平限流，把 LLM 调用分批并发，支持多用户同时提交
- **质量**：多层质检门控，按题型重试；提示词版本和快照让每条输出都可追溯

### 分子 AI 模型

- **EMDP** · [GitHub](https://github.com/ming1219/EMDP) · *Information Sciences*：用领域知识引导的强化学习设计新分子，再用微调的 Uni-Mol v2 性质模型和帕累托排序（能量、稳定性、可合成性）筛选，从 5000 个采样分子中得到 24 个候选
- **U3R-EMPP** · [GitHub](https://github.com/ming1219/U3R-EMPP) · CSCWD 2026：微调预训练的 3D 分子模型（Uni-Mol），同时预测 7 项性质；数据整合自三个已发表来源，按分子骨架划分做 10 折交叉验证

## 荣誉

- 2023 年 ACM 程序设计竞赛四川省赛银牌
- 2023 届四川省优秀大学毕业生
- 校级一等奖学金
- 研究生学业三等奖学金

## 技能

Python、TypeScript、Bash · LangGraph、MCP、FastAPI · Docker、Harbor · CVE 复现、补丁比对 · Uni-Mol、REINVENT、RDKit · Linux、nginx、systemd、Git · 使用 AI 编程助手并通过测试验证结果

## 爱好

ACM 程序设计竞赛
