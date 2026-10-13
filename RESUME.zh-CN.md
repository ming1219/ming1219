[English](RESUME.md) | **简体中文** · [← 主页](https://github.com/ming1219)

# 文健 · Wen Jian

我是西南科技大学的硕士三年级学生，2024 – 2026 年在研究院联合培养。我的工作集中在**大模型智能体**、**可执行任务环境**和**自动化评测**：搭建能调用领域工具完成任务的 agent，把任务做成能由程序验证的环境。

我也做分子 AI：用强化学习做分子从头设计，微调预训练的 3D 分子模型做性质预测，相关工作以第一作者发表于 *Information Sciences* 和 CSCWD 2026。

[GitHub](https://github.com/ming1219) · [EM-Agent 在线访问](https://em.dkelab.cn/)

## 经历

- **2024 – 2026**　联合培养研究生，研究院
- **在读**　硕士研究生（三年级），西南科技大学

## 论文

- **De Novo Design of Energetic Molecules via Domain-Guided Reinforcement Learning and Unified 3D Representation**
  *Information Sciences*　第一作者（新锐一区 TOP，中科院二区）　[代码](https://github.com/ming1219/EMDP)
- **U3R-EMPP: Unified 3D Representations via Pre-trained Models for Energetic Molecule Property Prediction**
  CSCWD 2026　第一作者（CCF-C）　[代码](https://github.com/ming1219/U3R-EMPP)

## 项目

### Security Task Factory：基于真实 CVE 的大模型评测与强化学习任务环境

- **复现真实 CVE**：比对漏洞版本与修复版本的源码，在官方 Docker 镜像上用最小的反向补丁去掉修复中的防护
- **使用 LLM 出题**：用注入配方驱动 LLM，生成环境构建脚本、题面和不公开的参考解
- **审核**：未作修改的目标必须失败、参考解必须能解出、错误提交必须失败、重复判分结果一致；另有三层泄露扫描
- **判分**：flag 逐字节比对、按配方定义的部分得分，既可作为评测的成功判定，也可作为强化学习的奖励
- **难度标定**：用模型 3 × 2 小时的试做并阅读轨迹来标定难度；把 10 多类容器环境故障沉淀为构建规则

### QA Studio：大模型训练数据生成平台 · [在线访问](https://qa.dkelab.cn)

在企业指导下构建 CoT 问答数据集：设计并实现多阶段数据生成系统，接入大模型，累计产出 10 万+ 条高质量问答数据。

- **六阶段可视化流水线**：预处理 → 生成 → 校验 → 评估 → 过滤 → 导出，把原始语料转化为高质量 QA 训练集
- **流水线引擎**：支持断点续跑、任意阶段重跑；自建全局线程池与公平限流，把 6 个阶段的 LLM 调用改为分批并发，解决多用户同时提交的问题
- **质量控制**：专业 CoT 构建、多层质检门控、按题型重试的闭环
- **可追溯**：配置中心 + 提示词版本管理 + 快照追溯

### EMBench：工具调用智能体评测框架 · 作者 · [GitHub](https://github.com/ming1219/EMBench)

一条可复用的流程：**任务设计 → 验证 → 判分 → 失败分析**。

- **任务规范**：每道题是一个目录，包含指令、声明式判分规则、参考轨迹和反例；任何智能体都能通过统一的轨迹格式接入
- **用可复用的检查组合判分**：轨迹匹配、参数约束、数值容差、覆盖与一致性；被推荐的分子必须全部来自本次生成结果，只提到生成过的分子或只命中关键词都不算数；输出多维度得分和 pass@k / pass^k
- **判分可信**：缺少证据或证据为 `null` 就判不通过，不再跳过；每条成绩都绑定产生它的 agent 和判分时的题目版本；置信区间按题目数计，重复试验不会让它变窄。判分自检：参考答案必须通过，空轨迹、截断轨迹、去掉工具结果、结果全是 `null` 的轨迹以及错误轨迹都必须失败
- **借助 Harbor 在 Docker 中运行**：每道题启动 agent 容器和一个模拟 MCP 工具服务，工具服务回放已记录的结果并在服务端记录每次调用；判分程序用只在判分阶段注入的密钥读取这份记录，agent 无法伪造轨迹。已端到端验证：参考解得 1.0 分，白卷得 0.0 分
- **经外部评审加固**：修复了评审发现的漏洞：暂缓或推荐生成集外分子被当成有效推荐、没有证据或用 `null` 冒充证据也能通过、换 agent 继承成绩、续跑时沿用旧版题目的成绩、置信区间虚假收窄。每个漏洞都变成了回归测试（共 80 个）

### EM-Agent：分子设计智能体 · 创建者、主要开发者 · [GitHub](https://github.com/ming1219/EM-Agent) · [在线访问](https://em.dkelab.cn/)

- **智能体**：LangGraph 单智能体 ReAct，以及并行调度子任务的多智能体「规划者–执行者」工作流（`Send()` map-reduce）；26 个以上领域工具的 MCP 工具服务（结构查询、性质预测、分子生成、逆合成、晶体结构搜索）；接入 PubChem 检索，防止模型编造分子结构；支持多家大模型（GLM / DeepSeek / Qwen）
- **评测与失败分析**：在轨迹层面检查工具、参数和结果。多智能体把候选完成率从 **40% 提升到 94%**（DeepSeek-V4-Flash）。定位并修复的根因：评测运行之间状态泄漏、列表参数被传成 JSON 字符串、冗余工具调用
- **工程**：FastAPI + SSE 后端，React + TypeScript 前端，含认证、计费和并发上限；部署到 2 台生产 Linux 服务器（nginx、systemd）；编写 Dockerfile

### 分子 AI 模型：生成与性质预测

- **EMDP** · [GitHub](https://github.com/ming1219/EMDP) · 论文 *Information Sciences*：分子从头设计。先在领域分子上对 REINVENT 预训练模型做迁移学习，再做分阶段强化学习，奖励由领域知识构成（子结构计数、几何平均聚合、骨架多样性过滤）；采样 5000 个分子，用微调的 Uni-Mol v2（1.64 亿参数）多任务模型预测 8 项性质，再按能量、稳定性（BDE）、可合成性（SA、SYBA）做帕累托筛选，得到 24 个候选
- **U3R-EMPP** · [GitHub](https://github.com/ming1219/U3R-EMPP) · 论文 CSCWD 2026：性质预测。微调预训练的 3D 分子表示模型（Uni-Mol），同时预测 7 项性质；数据集整合自三个已发表的数据来源（3DCNN、MDGNN、q-RASPR）；按分子骨架划分做 10 折交叉验证

## 荣誉

- 2023 届四川省优秀大学毕业生
- 校级一等奖学金
- 研究生学业三等奖学金

## 技能

Python、TypeScript、Bash · LangGraph、MCP、FastAPI · Docker、Harbor · CVE 复现、补丁比对 · Uni-Mol、REINVENT、RDKit · Linux、nginx、systemd、Git · 使用 AI 编程助手并通过测试验证结果

## 爱好

ACM 程序设计竞赛
