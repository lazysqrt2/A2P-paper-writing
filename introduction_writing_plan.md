# Introduction Writing Plan

本文档记录当前版本 Introduction 的写作思路。它的作用不是存放正文,而是说明为什么要这样组织引言、每段承担什么功能,方便后续改稿时保持主线一致。

## 核心判断

这版 Introduction 不从 "PBL 是什么" 开始,也不从 "We study..." 开始。

原因是 ACL 审稿人未必熟悉 PBL,但他们一定熟悉一个事实:LLM 已经让 explanation、summary、slides、quiz 变得便宜。真正仍然稀缺的是把知识变成一个学生可以亲手完成、能获得反馈、能真正练会的环境。

因此开头要从事实引出:

```text
explanations are cheap
practice environments remain costly
```

这能快速说明:

- 这件事为什么重要:技术学习不能只靠解释,很多能力必须在 working artifact 里做出来;
- 这件事为什么难:好的训练项目不是完整 repo,而是 runnable yet deliberately incomplete repo;
- A2P 为什么有价值:它不是更会生成文本或代码,而是把 source knowledge 编译成 learner-owned actions。

## 总体叙事弧线

```text
LLM 让解释变便宜
→ 技术学习的瓶颈变成 practice environment
→ training repository 必须能跑,但又必须在正确位置留空
→ 留空不是随便删代码,而是 controlled incompletion
→ controlled incompletion 需要知道 source concept 对应哪些 learner actions
→ direct generation 没有显式写出这条关系,所以无法验证教了什么
→ 现有 code generation 和 educational content generation 都缺这条 contract
→ A2P 先产出 Pedagogical Repository Contract,再实现成 runnable repo
→ 评测自然围绕 traceability、embodiment、controlled incompletion 等维度展开
```

## 每段功能

### Paragraph 1: 从时代事实和学习瓶颈切入

功能:建立共识,说明为什么这个问题重要。

这一段不急着介绍 PBL,而是先说 LLM 已经能低成本生成 summary、slides、quiz、walkthrough。但对很多技术能力来说,解释不是瓶颈;真正的掌握发生在学生构建、调试、测试、修复 working artifact 的过程中。

核心句:

```text
What remains costly is not telling students about knowledge, but turning knowledge into a practice environment where they must act on it.
```

这句话把 A2P 的位置钉住:不是 educational content generation,而是 knowledge-to-practice-environment construction。

### Paragraph 2: 定义目标 artifact

功能:让读者立刻知道 A2P 的输出是什么。

输出不是 summary、lesson plan、quiz,也不是 complete implementation,而是面向特定 learner 的 runnable training repository。它必须能运行,因为学生需要从代码、测试、数据、系统行为里获得真实反馈;同时它必须有意不完整,因为未完成部分就是学生要完成的学习动作。

这一段只用一句话带出 PBL:

```text
This is the artifact-construction setting of Project-Based Learning (PBL).
```

不要展开 PBL 的教育学背景,避免 intro 变成 PBL 科普。

### Paragraph 3: 点出关键矛盾 controlled incompletion

功能:说明为什么这个任务不同于普通 software generation。

普通代码生成里,incompletion 是 defect;训练仓库里,某些 incompletion 是 teaching interface。难点不是"留洞",而是"留对洞":

- 太完整会导致 cognitive offloading;
- 太不完整会导致 overload;
- 留错地方会变成 prerequisite work、busywork 或 unguided debugging;
- 同一个缺口对不同 learner 的意义不同。

这一段正式引入 controlled incompletion。

### Paragraph 4: 抽象出真正的教学关系

功能:把问题从"生成仓库"提升到"source concept 与 learner action 的对应关系"。

一个 repo 教 RAG,不是因为它包含 RAG 代码,而是因为它要求 learner 做 chunking、diagnose retrieval failures、evaluate answer quality、mitigate hallucinations 等 knowledge-bearing actions。

这一段要让读者接受:

```text
educational value is not a property of code alone;
it lies in source concepts ↔ learner actions.
```

### Paragraph 5: 解释为什么 direct generation 不够

功能:给出最硬的防守逻辑。

直接 prompt 生成 practice project 只给出 final artifact,没有显式写出:

- 选了哪些 source concepts;
- 哪些依赖关系决定学习顺序;
- 哪些 project tasks embody 哪些 concepts;
- 为什么某个 function 留给 learner 而不是系统实现;
- hint 是否泄露答案;
- test 验证的是 learning objective 还是 software behavior。

所以它无法真正验证项目教了什么,只能判断它看起来像不像教育产物。

### Paragraph 6: 定位 existing work

功能:把已有工作放进我们已经定义好的问题空间。

Repository-level code generation 优化 executable completeness,会倾向于填平实现缺口。Educational content generation 生成 slides、lesson plans、textbooks、quizzes、tutoring dialogue,但通常不生成 executable environment,也不把 learning objectives 变成 learner-owned actions。

结论:

```text
Neither line of work explicitly represents the contract among source knowledge, learner action, scaffolding, and validation.
```

### Paragraph 7: 介绍 A2P 的核心对象

功能:说明我们做的为什么好。

A2P 的核心不是 repo alone,而是 Pedagogical Repository Contract。Contract 把 source concepts 映射到:

- learning objectives;
- project tasks;
- learner-owned actions;
- scaffolds;
- tests;
- checkpoints。

这样 repo 不是 unconstrained end-to-end artifact,而是 contract 的实现。

### Paragraph 8: 介绍 pipeline 的作用

功能:说明五阶段 pipeline 服务于 contract,而不是让 pipeline 抢主线。

五阶段分别是 source analysis、project design、scaffolding calibration、repository construction、validation。重点是它维护 traceability,并让 instructor 在真正需要 pedagogical judgment 的地方介入。

这一段要把 incompletion 从 accidental property 变成 design object:

```text
incompletion can be checked, edited, and evaluated.
```

### Paragraph 9: 实验与评测

功能:说明 evaluation 是从问题定义自然长出来的。

因为任务不是仅仅生成 runnable repository,所以不能只看 test pass rate。要评测 compilation chain 是否成立:

- source faithfulness;
- embodiment;
- controlled incompletion;
- leakage avoidance;
- profile sensitivity;
- traceability;
- executability。

### Contributions

功能:把贡献压成四件事:

1. formulation: pedagogical compilation;
2. intermediate representation: Pedagogical Repository Contract;
3. implementation: five-stage human-in-the-loop A2P pipeline;
4. empirical evidence: better source faithfulness, embodiment, controlled incompletion, leakage control, traceability, and pedagogical quality。

## 写作禁忌

- 不要从 "We study..." 开头,因为太像自我声明,没有从事实引出重要性。
- 不要花太多段落介绍 PBL;PBL 只是 setting 的名字,不是 intro 的主角。
- 不要把贡献写成 "we generate PBL projects";这会把 A2P 降格成普通 generation system。
- 不要让五阶段 pipeline 成为主角;主角是 contract 和 controlled incompletion。
- 不要只用 "runnable project" 做 gap;真正的 gap 是 source knowledge、learner action、scaffolding、validation 之间没有显式 contract。
