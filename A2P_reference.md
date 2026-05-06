# A2P References — LLM × PBL Literature

本文档收录 A2P 论文 Related Work 需要的相关文献。

**版本：** v7（P1-2 完成，§2.4 Learner Modeling 扩充）  
**最后更新：** 2026-04-21  
**规划目录结构：** 见 `/root/A2P_reference/LANDSCAPE.md`（后续补充）

---

## 📋 Related Work 规划骨架

```
§2 Related Work
├── §2.1 Background: Educational AI & Tutoring Systems
│   └── 综述 / 背景锚定
│
├── §2.2 LLM-Based Content Generation for Education  ⭐ Step A 主力
│   ├── Presentation / Slides Generation
│   ├── Lesson Plan & Curriculum Generation
│   ├── PBL-Specific Support
│   └── Course-Aware Tutoring
│
├── §2.3 LLM Agents & Hierarchical/Structured Generation
│   └── 多智能体、分层规划、structured output，为 "hierarchical constrained generation" 背书
│
├── §2.4 Learner Modeling & Scaffolding
│   └── Knowledge Tracing / Student Model / Scaffolding 理论
│
├── §2.5 Human-in-the-Loop LLM Generation  (P1-1, TODO)
│
├── §2.6 Evaluation & Benchmarks for Educational AI
│   └── AI-as-judge for edu materials / PBL benchmarks
│
└── §2.7 Repository-Level Code Generation  (次要，讨论 A2P 里 code artifact 生成)
```

---

## ✅ 已入库文献

### §2.1 Background: Educational AI Surveys

#### [1] LLM Agents for Education: Advances and Applications
- **Paper ID:** 2503.11733
- **一句话：** 系统性综述 LLM 智能体在教育领域的应用，按任务类型分类（教学辅助 + 学生支持），涵盖记忆、工具、规划、个性化、多智能体通信等六种核心能力。
- **用法：** Related Work 起手综述引用，定位 A2P 在"LLM for education"中的位置。

#### [2] Advancing Education through Tutoring Systems: A Systematic Literature Review
- **Paper ID:** 2503.09748
- **一句话：** 系统性综述 86 项研究，将智能教学系统分为三类（基于软件的 ITS、基于机器人的 RTS、多模态系统）。
- **用法：** 与 [1] 并列作为教育 AI 大背景引用；可选。

---

### §2.2 LLM-Based Content Generation for Education ⭐ Step A 主力弹药

#### 📽 Presentation / Slides Generation

#### [3] PPTAgent: Generating and Evaluating Presentations Beyond Text-to-Slides
- **Paper ID:** 2501.03936
- **发表：** arXiv 2025-01
- **一句话：** 提出两阶段 edit-based 方法（模仿人类工作流），先从参考 PPT 抽取 slide 功能类型和内容 schema，再起草 outline、迭代生成编辑动作生成新 slide；同时提出 PPTEval 三维评估框架（Content / Design / Coherence）。
- **用法：** ⭐ **Step A 第一张牌**。经典"任意输入 → 特定教育载体"工作。A2P 与其根本区别：PPTAgent 做**单一载体（slides）**，而 A2P 生成**完整可执行项目仓库**（包含代码、任务分解、脚手架反馈等多模态教学组件）。PPTEval 的三维评估可为 A2P benchmark 设计提供借鉴。

#### [4] DeepPresenter: Environment-Grounded Reflection for Agentic Presentation Generation
- **Paper ID:** 2602.22839
- **发表：** arXiv 2026-02（PPTAgent 后续工作，同组）
- **一句话：** 相比 PPTAgent 的固定流水线，DeepPresenter 用 agentic 框架做自主 plan-render-revise 循环，基于"**环境扎根的反思**"（环境观察：渲染后的 slide 状态）而非 reasoning trace 式的自我反思。
- **用法：** 作为 slides generation 最新 SOTA 代表；对比 A2P 的 HITL 是"人类反馈 in the loop"而非 agent 自主反思。

#### 📚 Lesson Plan & Curriculum Generation

#### [5] LessonPlanner: Assisting Novice Teachers to Prepare Pedagogy-Driven Lesson Plans with LLMs
- **Paper ID:** 2408.01102
- **发表：** UIST 2024 (cs.HC)
- **一句话：** 基于 Gagne's nine events of instruction（教学事件理论）的交互式 lesson plan 辅助系统，N=12 内部受试者实验证明比 ChatGPT baseline 显著提升 lesson plan 质量并降低工作量。
- **用法：** ⭐ **教学理论 + LLM 生成"教学载体"的直接先例**。A2P 可参考其"以教学理论锚定生成"的做法；区别在于 LessonPlanner 生成的是**文档化 lesson plan 供教师参考**，而 A2P 生成**学生可直接上手的项目**。

#### [6] New Curriculum, New Chance — RAG for Lesson Planning in Ugandan Secondary Schools
- **Paper ID:** 2408.07542
- **发表：** arXiv 2024-08 (cs.CY)
- **一句话：** 基于 Cohere LLM + RAG，从政府认证教材向量库生成 lesson plan；24 份生成 plan 经 LPAP 评分 75-80%（"very good"），超过 Rwanda 同类人工研究（均 <50%）。
- **用法：** Real-world deployment 类代表；支持"LLM lesson plan 生成已实用化"这一论断，但指出其仅生成**教案文档**，不是**可执行项目**。

#### 🎯 PBL-Specific Support

#### [7] Co-designing LLM Tools for Project-Based Learning with K12 Educators
- **Paper ID:** 2502.09799
- **发表：** arXiv 2025-02 (cs.HC/AI/CY, CHI 风格共设计研究)
- **一句话：** 通过教师访谈、协作 workshop 和迭代 wireframe，识别 LLM 可支持的 PBL 实施痛点（项目设计、管理、评估、引导与自主平衡），提出 LLM-PBL 工具的设计指南。
- **用法：** ⭐ **最直接的动机引用**。说明"PBL 实施困难 + LLM 有潜力辅助"已是教育界共识（CHI 视角）；A2P 是对这些设计指南的**技术落地**——把教师痛点（project design automation）做成端到端生成系统。

#### [8] Generative AI as a Tool for Enhancing Reflective Learning in Students
- **Paper ID:** 2412.02603
- **发表：** arXiv 2024-11 (cs.HC)
- **一句话：** 在 PBL 语境下，用精心设计的 prompt 让 LLM 充当反思辅导工具，通过多轮对话模拟提供个性化反思引导。
- **用法：** 对比点——LLM 在 PBL 中当**反思辅导者**（过程支持）与 A2P 的 LLM 当**项目生成者**（产物支持）是两条互补路径；引用时明确区分。

#### 🤖 Course-Aware Tutoring (辅助)

#### [9] Design and Deployment of a Course-Aware AI Tutor in an Introductory Programming Course
- **Paper ID:** 2604.11836
- **一句话：** 部署课程感知的在线 Python 导师，集成检索增强、苏格拉底提问和课程材料对齐的解释功能，避免直接提供完整解决方案。
- **用法：** 与 A2P 间接相关——"课程感知"思路类似 A2P 的 learner-aware；但该工作是**运行时辅导**，A2P 是**项目生成前的设计决策**。

---

### §2.3 LLM Agents & Hierarchical/Structured Generation

> 这节为 A2P 方法名 **"hierarchical constrained generation"** 和**五阶段 Pipeline** 提供方法学支撑。

#### 🧩 Educational Agent Pipelines

#### [10] AWE: Agentic Workflow for Education
- **Paper ID:** 2509.01517
- **一句话：** 提出四组件模型（自我反思、工具调用、任务规划、多智能体协作），使 LLM 智能体能够自主执行教育工作流。
- **用法：** 对照 A2P 的五阶段 Pipeline；区别：AWE 偏向**执行**教学任务（答疑、实验模拟），A2P 偏向**生成**项目资源。

#### [11] AI Agent for Education: von Neumann Multi-Agent System Framework
- **Paper ID:** 2501.00083
- **一句话：** 提出冯·诺依曼多智能体系统框架，支持教师、课程和学生三类智能体协作，实现任务分解和自主协调。
- **用法：** 证明"多角色 agent 协作"在教育场景有先例；A2P 的对比点是 HITL 而非纯多 agent 自主协作。

#### 🔧 Hierarchical Task Decomposition & Prompting

#### [12] Plan-and-Solve Prompting
- **Paper ID:** 2305.04091
- **发表：** ACL 2023 (cs.CL)
- **一句话：** 提出 Plan-and-Solve (PS) zero-shot prompting——先让 LLM 起草 plan 将任务拆为子任务，再按 plan 执行；PS+ 扩展加入详细指令，十数据集上显著超 Zero-shot-CoT。
- **用法：** ⭐ **方法名直接背书之一**。A2P 的"先规划项目蓝图再逐阶段生成"思路可引 Plan-and-Solve 作为 prompting-level 先例，说明"plan-first decomposition"已是被验证的 LLM 范式。

#### [13] Least-to-Most Prompting
- **Paper ID:** 2205.10625
- **发表：** ICLR 2023 (cs.AI/CL)
- **一句话：** 将复杂问题分解为一系列更简单子问题并顺序求解，后续子问题的求解可利用前序答案；GPT-3 + 14-shot 在 SCAN 上达 99% 准确率（CoT 仅 16%）。
- **用法：** 与 [12] 并列作为 **task decomposition 经典**；支撑 A2P 五阶段 Pipeline 之"复杂生成任务必须分解求解"的合理性。

#### [14] Hierarchical Chain-of-Thought Prompting (Hi-CoT)
- **Paper ID:** 2604.00130
- **发表：** arXiv 2026-03 (cs.CL)
- **一句话：** 提出 Hi-CoT——在"指令规划"与"逐步执行"之间交替的分层推理结构，相比 flat CoT 提升平均准确率 6.2%（最高 61.4%），推理 trace 长度缩短 13.9%。
- **用法：** **直接为"hierarchical"方法名背书的最新工作**。A2P 的 hierarchical constrained generation 可类比 Hi-CoT 的"planning + execution 分层"结构，但 A2P 的约束层次是**教学语义**（learner-aware scaffolding）而非推理步骤。

#### 🤝 Multi-Agent Code Generation Pipelines

#### [15] Self-collaboration Code Generation via ChatGPT
- **Paper ID:** 2304.07590
- **发表：** arXiv 2023-04 (cs.SE, 广泛引用)
- **一句话：** 将软件开发方法论引入 LLM——三个 LLM 角色（分析师/编码者/测试者）分阶段协作完成代码生成，相比单 LLM 在各代码基准上提升 Pass@1 29.9%-47.1%。
- **用法：** ⭐ **A2P 五阶段 Pipeline 最接近的方法学亲属**。A2P 的每个 stage（输入解析/蓝图设计/任务分解/内容生成/验证反馈）对应 Self-collaboration 的 role 分工思路；但 A2P 的角色约束是**教学价值**（学习目标、脚手架、挑战度）而非纯软工流程。

#### [16] Small LLMs Are Weak Tool Learners: A Multi-LLM Agent
- **Paper ID:** 2401.07324
- **一句话：** 将 LLM 能力拆解为规划器、调用器、总结器三个模块，协同工作，在工具学习任务上超越单 LLM 方案。
- **用法：** 方法学锚点，证明"分阶段/模块化 LLM pipeline"有效；A2P 的五阶段可类比此分解思路。

#### [17] AutoP2C: Paper-to-Code Repository Generation from Multimodal Academic Papers
- **Paper ID:** 2504.20115
- **发表：** arXiv 2025-04 (cs.SE/AI)
- **一句话：** ⭐⭐⭐ 定义新任务 **P2C (Paper-to-Code)**——把学术论文（含文本/图表/公式）转成**可执行代码仓库**；四阶段 multi-agent 流水线：仓库蓝图抽取 → 多模态内容解析 → 分层任务分解 → 迭代反馈调试；在 8 篇论文基准上全部成功，o1/R1 仅成功 1 篇。
- **用法：** ⭐⭐⭐ **A2P 的"ML 研究版兄弟"**。两者都做"多模态输入 → 完整可执行仓库"，且四阶段流水线架构高度相似。必须 **direct contrast**：
  - AutoP2C：**保真还原论文实验代码**，忠实性是唯一目标
  - A2P：**生成教学项目**，challenge-noise separation + learner-aware 是核心约束——同一 input 对不同学习者要生成**不同**项目
  - 两者的"hierarchical task decomposition"一节可共享方法学引用，但目标函数本质不同。

---

### §2.4 Learner Modeling & Scaffolding

> 本节分两块：**理论承重柱**（经典心理学/教育学理论，非 arxiv）+ **现代 LLM 版 learner modeling**。
> 支撑 A2P 的 **Challenge-Noise Separation via Learner-Aware Scaffolding** 结构性主张。

#### 📚 经典理论基础（非 arxiv）

#### [18] The Role of Tutoring in Problem Solving (Scaffolding 经典)
- **Citation:** Wood, D., Bruner, J. S., & Ross, G. (1976). *Journal of Child Psychology and Psychiatry*, 17(2), 89-100.
- **一句话：** ⭐ 首次提出 **scaffolding** 比喻——通过 mother-child 教学实验，划出助学者完成"独立无法解决的任务"的 6 种脑手架功能（recruitment / reduction in degrees of freedom / direction maintenance / marking critical features / frustration control / demonstration）。
- **用法：** ⭐⭐⭐ **A2P 中所有"scaffolding"一词的必引之源**。可在 §1 Intro 和 §2.4 双引用。
- **PDF:** `https://sachafund.wordpress.com/wp-content/uploads/2018/10/wood_et_al-1976-journal_of_child_psychology_and_psychiatry.pdf`

#### [19] Mind in Society (Vygotsky / ZPD)
- **Citation:** Vygotsky, L. S. (1978). *Mind in Society: The Development of Higher Psychological Processes*. Harvard University Press.
- **一句话：** 提出 **Zone of Proximal Development (ZPD)**——学习者独立能力与在他人帮助下可达到能力之间的区域，是 Scaffolding 日后被契合的理论基础。
- **用法：** ⭐⭐⭐ **learner-aware scaffolding 的核心理论来源**。写 A2P 的 Challenge-Noise 切割规则时——"挺一挺达得到的东西是 challenge，一挺还是达不到的是 noise"——直接对应 ZPD 上下界，是方法合理性的核心论据。

#### [20] Cognitive Load During Problem Solving: Effects on Learning
- **Citation:** Sweller, J. (1988). *Cognitive Science*, 12(2), 257-285.
- **一句话：** 提出 **Cognitive Load Theory (CLT)**——演示了 "means-ends analysis" 这种传统解题过程因工作记忆负负过重而让学习效果极差，为后来 scaffolding / worked examples 的必要性提供根本解释。
- **用法：** **Challenge-Noise Separation 的心理学根基**。论述"为什么要给初学者减负 noise" 时，引 CLT 比引 ZPD 更准确——ZPD 讲上限，CLT 讲下限（工作记忆承载）。
- **DOI:** 10.1016/0364-0213(88)90023-7

#### [21] Project-Based Learning (Cambridge Handbook of the Learning Sciences)
- **Citation:** Krajcik, J. S., & Shin, N. (2014). "Project-Based Learning." In R. K. Sawyer (Ed.), *The Cambridge Handbook of the Learning Sciences* (2nd ed., pp. 275-297). Cambridge University Press.
- **一句话：** ⭐ **PBL 的权威式定义**——列出 PBL 五要素：driving question / situated inquiry / collaboration / learning technologies / tangible artifact；特别强调"批判性项目载体 (tangible artifact)"是 PBL 的防护性特征。
- **用法：** ⭐⭐⭐ **写 A2P 为什么选 PBL 而不是题库/对话/反馈作为载体时的唯一权威引用**。用来给 PBL 定义定锥。
- **历史兴起引用**（可选采一）：Blumenfeld, P. C., Soloway, E., Marx, R. W., Krajcik, J. S., Guzdial, M., & Palincsar, A. (1991). "Motivating project-based learning." *Educational Psychologist*, 26(3-4), 369-398.

#### [22] Scaffolding in Complex Learning Environments (现代技术扩展)
- **Citation:** Puntambekar, S., & Hübscher, R. (2005). "Tools for scaffolding students in a complex learning environment: What have we gained and what have we missed?" *Educational Psychologist*, 40(1), 1-12.
- **一句话：** 将 Wood 等的 scaffolding 原初概念从 1v1 教学扩展到**技术介导的复杂学习环境**，指出在扩展过程中丢失的关键特征：ongoing diagnosis / calibrated support / fading。
- **用法：** ⭐ **A2P 把 scaffolding 卡到模型生成里的理论桥梁**。引用时可写成："我们延续 Puntambekar & Hübscher (2005) 所提 scaffolding 三特征，将 ongoing diagnosis 具体化为 learner profile 驱动的任务决策。"

#### [23] Why Minimal Guidance During Instruction Does Not Work ⚠️ 辞峰篇
- **Citation:** Kirschner, P. A., Sweller, J., & Clark, R. E. (2006). "Why minimal guidance during instruction does not work: An analysis of the failure of constructivist, discovery, problem-based, experiential, and inquiry-based teaching." *Educational Psychologist*, 41(2), 75-86.
- **一句话：** ⭐著名的"反 PBL"战雄文——用 cognitive load theory 主张 minimal guidance (含纯粹 PBL) 的学习效率次于 direct instruction，对初学者尤其不利。
- **用法：** ⭐⭐⭐ **A2P 五阶段 HITL + learner-aware scaffolding 的最强辩护理由**。引用时写成："Kirschner et al. (2006) 警告纯粋的 minimal-guidance PBL 会造成认知过载——这正是我们按 learner profile 调节 challenge-noise 边界的动机。"
- **引用策略：** 必须和 [24] Hmelo-Silver 2007 **配对引用**——先见辣延续 Kirschner的批评，再追追 Hmelo-Silver 的回应，然后说我们的技术方案调解两者。

#### [24] Scaffolding and Achievement in PBL and Inquiry Learning
- **Citation:** Hmelo-Silver, C. E., Duncan, R. G., & Chinn, C. A. (2007). "Scaffolding and achievement in problem-based and inquiry learning: A response to Kirschner, Sweller, and Clark (2006)." *Educational Psychologist*, 42(2), 99-107. (**2535 citations**)
- **一句话：** ⭐对 Kirschner 等的经典回应——指出现实 PBL/inquiry 并非 minimal guidance，而是通过**结构化 scaffolding 提供大量指导**；有效的 PBL 必须包含 question elaboration / concept mapping / argumentation support 等 scaffolding 工具。
- **用法：** ⭐⭐⭐ **A2P 的理论正当性声明**：我们做的不是 minimal-guidance PBL，而是 sophisticated scaffolded PBL——此篇是给 reviewer 看的**"我站在哪边"**声明。
- **PDF:** `http://www.davidlewisphd.com/courses/EDD8121/readings/2007-Hmelo-Silver_et_al.pdf`

#### 📊 经典 Knowledge Tracing & ITS 综述（非 arxiv）

#### [26] Knowledge Tracing: Modeling the Acquisition of Procedural Knowledge (BKT)
- **Citation:** Corbett, A. T., & Anderson, J. R. (1995). "Knowledge Tracing: Modeling the Acquisition of Procedural Knowledge." *User Modeling and User-Adapted Interaction*, 4(4), 253-278.
- **一句话：** ⭐⭐⭐ **学生建模的里程碑**。提出 Bayesian Knowledge Tracing (BKT)——用隐马尔可夫模型追踪学生对知识组件的掌握概率，四参数（p(L₀), p(T), p(G), p(S)）至今仍是 ITS 标配。
- **用法：** A2P 的 learner profile 输入虽然比 BKT 简单（不做实时追踪），但必须回溯到 BKT 才能说明"学生建模"这条线的源头。引 1 句即可："我们的 learner-aware 设计继承了 Corbett & Anderson (1995) 以来的学生建模传统——不同之处在于 A2P 使用一次性画像而非实时 trace。"

#### [27] Deep Knowledge Tracing (DKT)
- **Citation:** Piech, C., Bassen, J., Huang, J., Ganguli, S., Sahami, M., Guibas, L. J., & Sohl-Dickstein, J. (2015). "Deep Knowledge Tracing." *Advances in Neural Information Processing Systems* (NeurIPS), 28.
- **一句话：** ⭐⭐ 将 RNN 引入 Knowledge Tracing，用 LSTM 端到端预测学生下题表现，比 BKT 精度显著提升，开创了 DLKT 时代。
- **用法：** 与 [26] BKT 构成经典→深度学习的演进对照。A2P §2.4 讲 learner modeling 时，"BKT → DKT → LLM-based"三步走线索。

#### [28] The Relative Effectiveness of Human Tutoring, ITS, and Other Tutoring Systems
- **Citation:** VanLehn, K. (2011). "The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems, and Other Tutoring Systems." *Educational Psychologist*, 46(4), 197-221.
- **一句话：** ⭐⭐ 对 ITS 有效性的最权威 meta-review——发现 ITS 在 step-level 交互下效果接近人类家教（σ=0.76），但在 answer-level 就不行了。
- **用法：** 支撑 A2P 为什么要做 scaffolding 而非简单输出——因为 VanLehn 证明了"交互粒度越细，学习效果越好"，A2P 的 5 阶段介入正是在 step-level 操作。

#### 💻 现代 LLM 版 Learner Modeling

#### [25] LLM-Assisted Knowledge Graph Completion for Curriculum and Domain Modelling
- **Paper ID:** 2501.12300
- **一句话：** 提出人机协作方案，利用 LLM 辅助构建课程-领域-用户三层知识图谱，实现跨学科个性化学习路径推荐。
- **用法：** ⭐ 与 A2P 的"learner profile → scaffolding"最接近的先例；direct contrast：他们做**推荐**（在已有资源中选路径），A2P 做**生成**（按 profile 造新项目）。

#### [35] Adaptive Learning Systems: Personalized Curriculum Design Using LLM-Powered Analytics
- **Paper ID:** 2507.18949
- **一句话：** 基于 LLM 分析的自适应学习系统框架，通过实时数据分析动态调整学习路径。
- **用法：** 自适应学习对照；说明 A2P 的学习者画像是**一次性输入**而非持续反馈；也显示"learner-aware content"是活跃方向。

#### [40] SINKT: A Structure-Aware Inductive Knowledge Tracing Model with LLM
- **Paper ID:** 2407.01245
- **发表：** arXiv 2024-07 (cs.AI/CY)
- **一句话：** ⭐ 首次将 LLM 引入 inductive KT——用 LLM 编码概念/题目语义并构建异构图，解决冷启动问题；在 4 个数据集上超过 12 个 transductive baseline。
- **用法：** 展示 KT 领域已进入 LLM 时代；与 A2P 的 learner-aware 设计形成技术生态对照。A2P 不做实时 KT 但受益于同一趋势（LLM 理解学习者）。

#### [41] NTKT: Next Token Knowledge Tracing via Pretrained LLM Representations
- **Paper ID:** 2511.02599
- **发表：** arXiv 2025-11 (cs.CL/AI)
- **一句话：** ⭐ 把 KT 重构为 next-token prediction——将学生历史 + 题目内容编码为文本序列，用 pretrained LLM 做预测；在 cold-start 用户/题目上泛化能力显著优于 DLKT。
- **用法：** 最新的 LLM × KT 突破，证明 pretrained representations 对理解学生行为有效。呼应 A2P 的假设——LLM 有能力理解学习者画像并据此调整生成内容。

---

### §2.5 Human-in-the-Loop LLM Generation

> 本节为 A2P 的**五阶段 HITL Pipeline** 方法学承诺背书。重点不在"HITL 有效"（已是共识），而在于 A2P 的五个介入点如何与已有 HITL 设计模式对齐。

#### [29] Guidelines for Human-AI Interaction (HAI 设计经典)
- **Citation:** Amershi, S., Weld, D., Vorvoreanu, M., Fourney, A., Nushi, B., Collisson, P., Suh, J., Iqbal, S., Bennett, P. N., Inkpen, K., Teevan, J., Kikin-Gil, R., & Horvitz, E. (2019). "Guidelines for Human-AI Interaction." *Proceedings of the 2019 CHI Conference on Human Factors in Computing Systems* (CHI '19), 1-13.
- **一句话：** ⭐ Microsoft Research 提出的 **18 条 Human-AI 交互设计准则**，按互动时间线分 4 阶段（initially / during interaction / when wrong / over time）。
- **用法：** ⭐⭐⭐ **HAI 领域的铺路引用**。A2P 的 HITL 设计可直接映射到 Amershi 的 4 阶段（初始输入时的 capability clarity / 中间断点的 revision），讲方法论时以此为理论序。
- **注：** 非 arxiv，CHI 2019 (ACM DL, DOI: 10.1145/3290605.3300233)

#### [30] Prototypical Human-AI Collaboration Behaviors (PATHs)
- **Paper ID:** 2505.16023
- **发表：** arXiv 2025-05 (cs.CL/HC)
- **一句话：** 大规模分析 Bing Copilot / WildChat 写作任务中的多轮交互，提出 **PATHs**（典型协作行为模式）——包含 revising intents / exploring texts / posing questions / adjusting style / injecting content 等；少数 PATHs 占 majority of 交互方式。
- **用法：** ⭐ **支撑 A2P “5 阶段介入点”不是自创而是交互模式基于实证**。引用时可写："我们的介入点设计参考了 Mysore et al. (2025) 在写作任务中识别出的 PATHs——特别是 revising intents 和 injecting content 两大类。"

#### [31] Interaction-Required Suggestions for Control, Ownership, and Awareness in Human-AI Co-Writing
- **Paper ID:** 2504.08726
- **发表：** arXiv 2025-04 (cs.HC)
- **一句话：** 提出设计原则：生成式 AI 界面应"必须涉及人类介入"——通过预测式输入 + edit-opportunity highlight，促进认知投入 / 耐心决策 / 所有权感。
- **用法：** ⭐ **为 A2P “高介入点”的设计投余主义背书**。解释为什么 A2P 不选 end-to-end 一键生成——因为高介入保障老师的 ownership/control/quality。

#### [32] Human-in-the-Loop Development Workflow for Domain AI Assistants (Summit Concierge)
- **Paper ID:** 2511.03186
- **发表：** arXiv 2025-11 (cs.AI)
- **一句话：** Adobe Summit Concierge 实战案例：在数据稀缺/质保/快速部署约束下，采用 prompt engineering + RAG + **轻量级人工验证**的 HITL 开发工作流，能在 cold-start 场景可靠落地。
- **用法：** **实践型 HITL 案例引用**。A2P 在讨论为什么需要 HITL 而非全自动时可引一句：enterprise context 下相似约束（data sparsity + quality assurance）已被验证需要 HITL。

#### [33] Formalising Human-in-the-Loop: Computational Reductions and Failure Modes
- **Paper ID:** 2505.10426
- **发表：** arXiv 2025-05 (cs.CY/AI/HC)
- **一句话：** 用计算可归约理论（oracle machines + Turing/many-one reductions）**形式化区分**三种 HITL 设置：监控型 (total functions) / 单点动作型 (many-one) / 深度交互型 (Turing)，并提出 HITL 失效模式分类法。
- **用法：** **写方法讨论时用来 position A2P 的 HITL 属于哪种形式**——A2P 的五阶段介入属于"Turing reductions"（高度交互型）。供 reviewer 检验属性验证。

#### [34] Controllable Mixed-Initiative Dialogue Generation through Prompting
- **Paper ID:** 2305.04147
- **发表：** arXiv 2023-05 (cs.CL/AI/HC)
- **一句话：** 将 LLM 用于 mixed-initiative 对话的可控生成，在 PersuasionForGood 和 Emotional Support 两任务上超过监督学习 baseline。
- **用法：** 提供 "mixed-initiative" 在 LLM 时代的典型实践；与 [34] 交互用语形成 HITL 的旧新术语对照。


---

### §2.6 Evaluation & Benchmarks for Educational AI

#### [42] Towards Robust Evaluation of STEM Education: Leveraging MLLMs in PBL
- **Paper ID:** 2505.17050
- **发表：** arXiv 2025-05 (cs.CL/AI/CE/CY/MM)
- **一句话：** 发布 **PBLBench**——基于 AHP 层次分析法构建的 STEM PBL 评测基准，测 15 个 MLLM/LLM，最佳模型仅 59% rank accuracy；强调现有 benchmark 在自由输出结构和专家验证上的不足。
- **用法：** ⭐⭐⭐ **对 A2P 最具威胁的相关工作**。必须 direct contrast：
  - PBLBench：**评测 MLLM 在已有 PBL 任务上的表现**（reasoning + long-context）
  - A2P：**从非结构化输入生成新的 PBL 项目**（generation，非 evaluation）
  - 两者互补，但定位不能混淆；A2P 的 benchmark 是生成质量评测，目标任务和粒度都不同。

#### [43] Judging the Judges: Human Validation of Multi-LLM Evaluation for K-12 Science Instructional Materials
- **Paper ID:** 2602.13243
- **发表：** arXiv 2026-01 (cs.CY/AI)
- **一句话：** 选取 12 个高质量 OpenSciEd / 多元读写 PBL 课程单元，用 GPT-4o/Claude/Gemini 基于 EQuIP rubric 给出 648 条评分+理由，两位专家独立验证 agreement/disagreement；目标是为未来 GenAI 教学材料设计 agent 提供原则。
- **用法：** 支撑 A2P benchmark 设计中"LLM as judge 需专家校准"的论断；也引出"自动评估教学材料"方向，A2P 可沿用其 rubric 思路。

---

### §2.7 Repository-Level Code Generation

> 这条线服务于 A2P 的**项目仓库生成**这个具体形态——生成完整 repo（而非单函数）。

#### [44] CodeAgent: Tool-Integrated Agent for Real-World Repo-Level Coding
- **Paper ID:** 2401.07339
- **发表：** arXiv 2024-01 (cs.SE)
- **一句话：** 提出 **CodeAgentBench**（5 个 Python 项目 101 samples）和 CodeAgent 框架（集成信息检索、代码符号导航、代码测试等 5 种编程工具），在 repo 级代码生成上获 18-250% 提升。
- **用法：** Repo-level 代码生成奠基性工作之一；A2P 的**产出物是可执行仓库**，借鉴其"工具集成 + 多阶段 agent"思路，但目标不同——A2P 要生成的是**为学习设计的教学项目**（包含刻意挑战、脚手架、里程碑），而非还原真实项目。

#### [45] GraphCodeAgent: Dual Graph-Guided LLM Agent for RACG Repo-Level Code Generation
- **Paper ID:** 2504.10046
- **发表：** arXiv 2025-04 (cs.SE)
- **一句话：** 用双图（Requirement Graph + Structural-Semantic Code Graph）guided 的 agent 做多跳推理，实现 repo 级检索增强代码生成；在 DevEval 和 CoderEval 上超 SOTA。
- **用法：** 说明 repo 级代码生成**已走向图驱动、上下文感知**的方向；A2P 在"生成带依赖的项目"时可参考其思路，但 A2P 约束是**教学价值驱动**而非**还原真实 repo**。
---

## 🚧 待补充（按优先级）

### P0-1 LLM × PBL + 相邻生成  ✅ 完成 (2026-04-21) — 见 §2.2
### P0-2 Hierarchical / Structured LLM Agents  ✅ 完成 (2026-04-21) — 见 §2.3 [12]-[17]
### P0-3 Scaffolding & PBL 教育学理论  ✅ 完成 (2026-04-21) — 见 §2.4 [18]-[24]（非 arxiv 经典）
### P1-1 Human-in-the-Loop LLM Generation  ✅ 完成 (2026-04-21) — 见 §2.5 [29]-[34]

### P1-2: Learner Modeling / Knowledge Tracing  ✅ 完成 (2026-04-21) — 见 §2.4 [26]-[28] (经典) + [40]-[41] (LLM-KT)

### P1-3: Education Benchmarks 扩展 (1-2) ⏳
- [ ] 已有 PBLBench [36]、K-12 Science Judges [37]；再补 1-2 篇非 PBL 教育评测

### P2: Repo-level Code Benchmarks 扩展 (1-2) ⏳
- [ ] RepoBench, ClassEval, CoderEval（作为 context，无需精读）

---

## ❌ 已移除（13 篇，和 A2P 核心脱钩）

以下论文从旧版 reference 中移除：内容聚焦于**教育对话 / 反馈评价 / 题目生成 / 社会影响研究**，不是 A2P 的"生成完整项目载体"主题，放入 Related Work 会模糊 paper 定位。

- EduQG (2305.07871) — 题目生成
- LearnLens (2507.04295) — 学情测量
- Dean of LLM Tutors (2508.05952) — 反馈评价
- BEA 2023 Shared Task (2306.06941) — 教师对话竞赛
- Automated Educational Question Generation (2408.04394) — 题目生成
- LoRA Fine-Tuning (2504.15610) — 微调技术
- AI Literacy Cross-National (2507.03020) — 社会调查
- Tutor CoPilot (2410.03017) — 辅导实时指导
- I Don't Trust You (2406.14871) — 信任研究
- Training LLM-based Tutors (2503.06424) — 对话微调
- Improving Assessment of Tutoring Practices (2402.14594) — 辅导评价
- Ask-EDA (2406.06575) — EDA 设计助手
- Trace-and-Verify (2502.13311) — 编码辅导 DPO

> 备份见 `A2P_reference.md.bak`

---

## 📊 当前统计

| 章节 | 论文数 | 状态 |
|---|---|---|
| §2.1 Background Surveys | 2 | ✅ |
| §2.2 Content Generation | 7 | ✅ Step A 主力 |
| §2.3 LLM Agents / Hierarchical | 8 | ✅ 方法名背书 |
| §2.4 Learner Modeling (经典 10 + LLM 4) | 14 | ✅ 理论+经典KT+现代LLM |
| §2.5 HITL | 6 | ✅ HITL 承诺充足 |
| §2.6 Evaluation | 2 | ✅ |
| §2.7 Repo-level Code | 2 | ✅ |
| **合计** | **41** | |

**进度：** P0 全完成，P1-1/P1-2 完成；剩 P1-3、P2（两项都属于"锦上添花"类别，未做不影响 Related Work 主骨架）。
