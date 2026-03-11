# 独立产品立项与 GitHub 准备指南

在“Idea 阶段”完成了市场调研与痛点挖掘后，**在正式进入“产品设计”之前，第一要务就是落实工程基建——建立你的 GitHub 仓库**。

不要等到代码写了一大半才想到要建库。独立开发者的产品设计、架构文档甚至是私有的 AI 规则 (Rules)，从 Day 1 起就必须沉淀在 Git 版本控制中。

---

## 一、 为什么在“设计阶段”前就要建库？

1. **“真理唯一”的文档沉淀**：产品设计（PRD、交互文档）和后续的技术方案，将作为 AI (如 Antigravity) 的上下文核心。它们必须存放在代码库的 `docs/` 等目录中，与代码同宗同源，同步演进。
2. **AI 工作流的基础**：Antigravity 许多高级能力（例如触发带有 `// turbo` 的规则，审查 Git Diff 生成单测，或是自动构建 CI/CD）都严重依赖 Git 环境。没有 `.git` 目录，AI 的自动机能力将大打折扣。
3. **防止思路丢失**：Idea 最初的火花和早期的讨论记录是最宝贵的资产。及早建库，哪怕只 Push 了几个 Markdown 文件，这也是对抗不确定性的最佳保障。

---

## 二、 Git / GitHub 初始化标准动作 (SOP)

### 1. 在 GitHub 创建远端仓库
1.  登录 GitHub，点击 `New repository`。
2.  填写规范的项目名称（建议全小写连字符，如 `my-awesome-app`）。
3.  设定为 **Private（私有）**（若尚未准备开源，保护你的创意资产）。
4.  **初始化设置**：
    *   勾选 `Add a README file`（作为项目的门面和索引）。
    *   根据你预想的技术栈添加 `.gitignore`（如 Node/Java/Python 等），避免后续把本地 `node_modules` 等垃圾推上远端。

### 2. 克隆到本地工作区
在你的本地开发目录（如 `~/Workspace/`）打开终端：
```bash
git clone git@github.com:your_username/your-repo-name.git
cd your-repo-name
```

### 3. 建立“AI 友好”的初始目录结构
不要等代码启动，先用如下结构拉好架子，告诉 AI（Antigravity）之后产生的设计文档该往哪里放：

```bash
mkdir -p docs/01_产品设计 docs/02_UI设计 docs/03_技术设计 .agent/rules .agent/workflows scripts
```

此时你的项目哪怕连一行代码都没有，看起来依然像一支正规军：
*   **`docs/`**：存放接下来的 PRD、领域模型、架构文档。
*   **`.agent/`**：专为 Antigravity 预留的大脑配置区（用于存放自定义 Rules、Workflows）。
*   **`README.md`**：作为大纲，存放你在 Idea 阶段调研过的结论和竞品分析。

### 4. 提交第一次基建代码 (First Commit)
```bash
git add .
git commit -m "chore: 初始化基础设施目录与空 README"
git push origin main
```

---

## 三、 在 Antigravity 中挂载 GitHub 项目

当上述结构在本地完成后，你可以使用 Antigravity **直接打开这个包含 `.git` 的根目录作为你的 Workspace（工作区）**。

从这一刻起：
*   **你可以开始放心地让 AI 撰写产品设计**：如果回答不满意，你可以放肆地要求修改而不用担心历史版本丢失，随时使用版本对比能力。
*   **你可以随时要求 AI 回顾上下文**：例如让它“基于 `docs/01_产品设计/` 里的三个文件，帮我推演下一阶段的 UI”。一切尽在掌控。

### AI 智能体 GitHub 联动进阶
*   **生成 Commit Message**：后续在写文档或代码时，每完成一个逻辑闭环，直接告诉 Antigravity：_“帮我生成一段符合 Angular 规范的 commit message 并执行 push。”_ 它会自动读取 `git diff` 并妥善提交。
*   **Review Code**：在 Push 远端之前，让 Agent 帮你 `git diff` 扫一遍，检查是否有无意中带入的秘钥 (API Keys) 或者是 TODO 标记。

## 推荐的 AI 驱动型项目目录结构 (AI-Native Project Structure)

为了让 Antigravity 能够最精准地读取上下文，同时保持独立开发者全栈项目（通常采用 Monorepo）的整洁，建议采用以下“文档与代码同构”的常用目录规范：

```text
/your-indie-product
├── .agent/                  # 🤖 AI 研发大脑配置区 (规则、工作流)
│   ├── rules/               # 局部代码规范 (如 frontend.md, backend.md)
│   ├── skills/              # AI 专属技能组 (如 code-review.md)
│   └── workflows/           # 自动化工作流 (如 deploy-prod.md)
├── docs/                    # 📄 AI 的上下文之源 (真理唯一)
│   ├── 01_产品设计/          # 存放 PRD、用户故事、功能清单
│   ├── 02_UI设计/            # 存放 Stitch 设计规范/切图参考
│   └── 03_技术设计/          # 存放 架构图、数据库 DDL、OpenAPI.yaml
├── apps/                    # 💻 源代码区 (业务逻辑主程序)
│   ├── web/                 # 前端应用 (例如 Next.js / Vue3)
│   ├── api/                 # 后端服务 (例如 Spring Boot / NestJS / Go)
│   └── mobile/              # 移动端应用 (可选，如 React Native / Flutter)
├── packages/                # 📦 共享物料区 (可选，全栈项目强烈推荐)
│   ├── shared-types/        # 前后端共享的类型定义 (如 OpenAPI 自动生成的 Types)
│   ├── ui-components/       # 基础 UI 组件库 (内部复用)
│   └── core-utils/          # 核心算法与工具函数
├── scripts/                 # 🛠️ 运维与辅助脚本 (数据库迁移、Docker 构建、CI/CD)
├── docker-compose.yml       # 基础设施一键启动 (DB, Redis, MQ 等)
└── README.md                # 项目导航与大盘入口
```

**结构优势解析**：
*   **上下文精准隔离**：当 AI 写前端逻辑时，你可以精准地仅将 `apps/web/` 目录和 `docs/03_技术设计/OpenAPI.yaml` 挂载给它，避免庞杂的后端代码干扰它的注意力，导致“幻觉”。
*   **真理唯一法则**：所有由前序环节（产品策划、技术设计）产出的文档全部集中收敛在 `docs/` 下。这是 AI 编写代码时唯一的“需求与技术法则”，改需求先改文档，彻底杜绝代码和文档脱节。
*   **规范就近约束**：`.agent/` 下的规则库和业务代码放在同一个 Git 仓库。这意味着不论你在哪台电脑上拉取代码，都能获得完全一致的 AI 编码行为约束。

---