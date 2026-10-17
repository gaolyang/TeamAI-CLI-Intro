# TeamAI CLI 项目介绍

> 项目地址：<https://github.com/Tencent/teamai-cli/tree/main>  
> 开源方：Tencent  
> 项目定位：基于 Git 的团队 AI 资产管理与协作工具

---

## 1. TeamAI 是什么？

TeamAI 是腾讯开源的一套面向团队的 AI 工程协作工具。

它解决的核心问题不是“再做一个 AI Agent”，而是：

> **如何把个人调教好的 AI 能力，沉淀成团队可以统一管理、共享、复用和持续迭代的能力。**

在日常使用 Claude Code、Codex、Qoder、Kiro 等 AI 开发工具时，团队成员通常会逐渐积累：

- Skill
- Prompt / Rule
- Agent
- MCP Server
- 模型配置
- 环境配置
- 项目知识
- AI 使用经验
- 测试与运维流程

如果这些内容只保存在个人电脑中，就容易出现：

- 同一个能力重复开发
- 不同成员使用不同版本的 Prompt / Skill
- 团队规范更新后无法统一同步
- 优秀经验无法复用
- Skill 缺少 Review、版本管理和发布机制

TeamAI 的目标，就是把这些内容统一作为 **Team AI Assets（团队 AI 资产）** 管理，并借助 Git 完成版本控制、Review、发布与同步。

---

## 2. 可以怎样理解 TeamAI？

可以把 TeamAI 理解成：

> **Git + Skill 仓库 + Agent 配置中心 + 团队 AI 知识库 + 使用反馈体系**

传统 Git 仓库主要管理：

```text
代码
文档
配置文件
```

TeamAI 希望进一步管理：

```text
AI 团队资产

├── Skills
├── Rules
├── Docs
├── Agents
├── Environment
├── Hooks
├── MCP
├── Models
├── Learnings
├── Team Wiki
└── Sessions / Usage
```

整体逻辑可以理解为：

```text
                    TeamAI Git Repository
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
        Skills            Rules              MCP
          │                 │                 │
          ├──────────┬──────┴──────┬──────────┤
          ↓          ↓             ↓          ↓
     Claude Code   Codex         Qoder       Kiro
          │          │             │          │
          └──────────┴──────团队成员───────────┘
```

也就是说，团队可以开始拥有一个统一的 **AI 能力仓库**。

---

## 3. TeamAI 的三层核心能力

TeamAI 的整体能力可以分为三层：

| 能力层 | 解决的问题 | 典型内容 |
|---|---|---|
| Team Execution | 让不同 Agent 按团队统一方式工作 | Skills、Rules、Agents、Hooks、MCP、Env、Models |
| Team Context | 让 AI 理解团队和项目 | Learnings、团队知识、Team Wiki |
| Team Improvement | 从 AI 使用过程中持续沉淀经验 | Sessions、Usage、Digest、Dashboard |

其中，现阶段最适合团队优先落地的是：

> **Team Execution**

也就是先把 Skill、Rule、Agent、MCP 等能力统一起来。

---

## 4. Team Execution：统一团队 AI 执行能力

Team Execution 的核心目标可以理解为：

> **一个团队，一套统一 AI 工作规范，多种 Agent 共同使用。**

例如团队可以维护：

```text
team-ai-repo/

├── skills/
│   ├── linux-test/
│   ├── security-review/
│   ├── log-analysis/
│   └── report-generator/
│
├── rules/
│   ├── coding-standard.md
│   ├── security-rule.md
│   └── test-standard.md
│
├── agents/
│   ├── test-agent.yaml
│   └── security-agent.yaml
│
├── docs/
│   ├── architecture.md
│   └── test-specification.md
│
├── mcp/
│   └── mcp.yaml
│
├── env/
│   └── env.yaml
│
└── models/
    └── models.yaml
```

这样可以避免：

```text
A 同事维护一套 Prompt
B 同事维护另一套 Prompt
C 同事自己开发一个 Skill
D 同事不知道这个 Skill 已经存在
```

最终形成：

```text
团队能力
   ↓
TeamAI Repository
   ↓
统一发布和同步
   ↓
不同 AI Agent
   ↓
整个团队使用
```

---

## 5. Skill 是 TeamAI 中最重要的资产之一

假设团队开发了一个：

```text
linux-security-test
```

Skill，它可以定义：

```text
如何连接服务器
        ↓
如何读取测试用例
        ↓
如何执行 Linux 命令
        ↓
如何判断 PASS / FAIL
        ↓
如何保存日志
        ↓
如何截图
        ↓
如何生成测试报告
```

如果这个 Skill 只存在某位同事电脑里：

```text
~/skills/linux-security-test/
```

那么它仍然属于“个人能力”。

如果发布到 TeamAI 管理的团队仓库：

```text
team-repo/
└── skills/
    └── linux-security-test/
        └── SKILL.md
```

就可以进入：

```text
开发
 ↓
Git 提交
 ↓
PR / MR
 ↓
Code Review
 ↓
Merge
 ↓
团队同步
 ↓
所有成员使用
```

这意味着：

> **Skill 从个人 Prompt / 脚本，升级成了可以版本管理、评审、发布和复用的团队工程资产。**

---

## 6. TeamAI 的典型发布流程

TeamAI 充分复用了 Git 的工程流程。

可以理解为：

```text
成员开发 Skill / Rule / Agent
            │
            ↓
         Git 提交
            │
            ↓
         分支开发
            │
            ↓
         PR / MR
            │
            ↓
        Code Review
            │
            ↓
           Merge
            │
            ↓
     TeamAI Repository
            │
            ↓
         同步更新
            │
            ↓
       团队成员本地
            │
            ↓
Claude Code / Codex / 其他 Agent
```

它的优势是：

- 不需要重新设计一套权限体系
- 可以继续使用 Git Review
- 可以保留版本历史
- 可以回滚
- 可以明确责任人
- 可以方便审计变更

---

## 7. Team Context：让 AI 理解团队经验

TeamAI 不只是管理 Skill。

它还希望逐渐解决：

> **AI 是否能够理解“我们团队以前是怎么解决问题的”。**

例如某位工程师解决了一个 FusionOS 问题：

```text
升级后 systemd 服务启动失败
        ↓
排查发现配置文件路径发生变化
        ↓
形成解决经验
```

传统情况下，这些内容可能只存在于：

```text
聊天记录
个人笔记
Issue
人的记忆
```

TeamAI 希望逐步沉淀到：

```text
Learnings
Team Wiki
项目知识
```

未来其他成员再遇到类似问题时，AI 可以优先复用团队已有经验。

---

## 8. Team Improvement：让团队 AI 能力持续进化

TeamAI 还希望从日常 AI 使用过程中持续提取经验。

例如：

```text
AI 第一次执行失败
        ↓
用户进行纠正
        ↓
第二次仍存在问题
        ↓
再次修正
        ↓
最终形成正确方法
```

这种会话本身就包含有价值的经验。

长期可以形成：

```text
AI 执行
   ↓
发现问题
   ↓
人工纠正
   ↓
经验沉淀
   ↓
团队共享
   ↓
下一次执行更准确
```

最终实现：

> **AI 用得越多，团队积累的能力越强。**

---

## 9. 支持的 AI Agent

TeamAI 的一个重要特点是：

> **不绑定单一 AI Agent。**

目前项目中可以看到对多种 AI 工具的支持，例如：

- Claude Code
- Codex
- Qoder
- Kiro
- ZCode
- JoyCode

不同 Agent 对以下能力的支持程度可能不同：

- Skills
- Rules
- Env
- Hooks
- MCP
- Models

因此实际落地时，需要结合团队当前使用的 AI 工具进行适配。

整体架构可以理解为：

```text
Claude Code ──┐
Codex ────────┤
Qoder ────────┤
Kiro ─────────┤
              ↓
           TeamAI
              ↓
        团队统一 AI 资产
```

---

## 10. 支持企业内部 Git 仓库

TeamAI 的团队资产本质上是 Git Repository。

因此它非常适合企业内部使用。

团队可以将以下内容放入自己的私有 Git：

```text
内部测试 Skill
内部安全 Skill
内部运维 Skill
内部 API Skill
产品知识
测试规范
开发规范
Agent 配置
MCP 配置
```

而不需要把内部资产公开到 GitHub。

这对于企业内部 AI 工程建设尤其重要。

---

## 11. 基础安装方式

可以通过 npm 安装：

```bash
npm install -g teamai-cli
```

之后初始化团队仓库：

```bash
teamai init https://github.com/your-org/your-repo
```

也可以使用用户级安装方式：

```bash
teamai init https://github.com/your-org/your-repo --scope user
```

完成后，即可通过团队仓库进行 AI 资产同步和管理。

---

## 12. 一个实际使用示例

假设测试团队维护：

```text
skills/

├── security-check
├── testcase-generator
├── linux-runner
├── webssh-runner
├── playwright-runner
├── report-generator
└── log-analyzer
```

成员 A 开发：

```text
playwright-runner
```

然后提交到团队仓库。

成员 B 更新 TeamAI 后，在 Codex 中就可以直接使用：

```text
使用 playwright-runner，
执行当前 Web 测试任务，
并生成测试结果截图。
```

成员 B 不需要重新：

- 学习 Playwright
- 编写脚本
- 设计执行流程
- 复制 Prompt
- 手工配置 Skill

因为这些已经成为：

> **团队公共 AI 能力。**

---

## 13. 对测试团队的价值

对于测试、OS、安全、运维团队，TeamAI 特别适合用于构建统一的 Skill Library。

例如：

```text
skills/

├── linux-command-runner
├── ssh-test-runner
├── webssh-runner
├── playwright-runner
├── testcase-parser
├── security-hardening
├── vulnerability-check
├── log-analyzer
├── rpm-check
├── test-report-generator
└── issue-analyzer
```

最终可以形成：

```text
             TeamAI
                │
      ┌─────────┼─────────┐
      ↓         ↓         ↓
   测试人员   开发人员   运维人员
      │         │         │
      └─────────┼─────────┘
                ↓
         使用统一 Skill
                ↓
         使用统一测试规范
                ↓
         生成统一测试证据
                ↓
         输出统一测试报告
```

---

## 14. TeamAI 与普通 Skill 仓库的区别

| 普通 Skill 仓库 | TeamAI |
|---|---|
| 保存 Skill | 管理 Skill |
| 主要靠手动下载 | 提供统一同步机制 |
| 很少考虑不同 Agent | 面向多个 AI Agent |
| 缺少发布流程 | 可以结合 Git Review |
| 缺少团队规范 | 支持 Rules / Docs |
| 很少管理 MCP | 可以统一管理 MCP |
| 很少沉淀经验 | 支持 Learnings |
| 无团队知识体系 | 可扩展 Team Wiki |
| 无使用反馈 | 可扩展 Sessions / Usage |

因此，TeamAI 并不是简单的：

> “把 Skill 放进 Git”。

而是进一步把：

```text
Skill
Prompt
Rule
Agent
MCP
Model
Knowledge
Experience
```

统一纳入团队 AI 工程体系。

---

## 15. 建议的团队落地方式

不建议一开始就启用 TeamAI 的全部能力。

建议分阶段推进：

```text
Phase 1
统一管理 Skills
        ↓
Phase 2
加入 Rules / Docs
        ↓
Phase 3
接入 MCP / Agent / Hooks
        ↓
Phase 4
沉淀 Team Learnings
        ↓
Phase 5
建立 Team Wiki
        ↓
Phase 6
分析 Sessions / Usage
```

第一阶段只需要解决一个最重要的问题：

> **让团队开发出来的 Skill，不再属于某一个人的电脑，而是真正变成团队资产。**

---

## 16. 对我们团队的启发

如果团队目前已经在研究：

- Agent 自动执行
- WebSSH
- Playwright
- 自动截图留痕
- Linux 自动化测试
- 安全加固测试
- 测试报告自动生成
- 内部 Skill 封装

那么 TeamAI 非常适合作为这些能力上层的：

> **统一 Skill / Agent / Rule 管理与分发层**

例如未来可以形成：

```text
                TeamAI
                   │
         ┌─────────┼──────────┐
         │         │          │
      WebSSH   Playwright   SSH Runner
         │         │          │
         └─────────┼──────────┘
                   ↓
             Test Agent
                   ↓
              读取测试用例
                   ↓
              自动执行测试
                   ↓
              截图 / 日志
                   ↓
              PASS / FAIL
                   ↓
              自动生成报告
```

TeamAI 不负责替代 WebSSH、Playwright 或 Agent。

它更适合作为：

> **这些 AI 能力的统一管理层。**

---

## 17. 一句话总结

如果用一句话介绍 TeamAI：

> **TeamAI 是一个基于 Git 的团队 AI 资产管理平台，将原本分散在个人电脑上的 Skill、Rule、Agent、MCP、模型配置和 AI 使用经验，变成可以统一管理、评审、同步、复用并持续沉淀的团队资产。**

它真正解决的问题是：

> **如何把“个人会使用 AI”，升级成“团队拥有可以持续复用的 AI 工程能力”。**
