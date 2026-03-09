# 独立产品 UI 设计指南 (基于 Stitch 与 MCP)

在明确了 `产品设计/全流程交互细节.md` 之后，我们需要将枯燥的线框图和流程图转化为高保真的 UI 界面。

目前在 AI 驱动的 UI 领域，由于我们已经在 Antigravity 中成功接入了 **Stitch MCP** 和专属的 **Stitch UI Design 技能 (Skill)**，我们实现了全流程的闭环：写完 PRD -> Antigravity 直接下发指令给 Stitch -> 原地生成炫酷的 UI 页面并提取代码。

---

## 一、 为什么现阶段选择 Stitch 与 MCP 结合？

1. **术业有专攻**：Antigravity 擅长全栈架构、复杂后端逻辑与长下文文档的“状态管理”；而 Stitch 的模型经过高度的前端 UI 渲染和交互调优，能极快地生成不仅“跑得通”而且“好看”的 React/Vue/Tailwind 组件。
2. **全流程自动化**：凭借 MCP (Model Context Protocol) 的打通，Stitch 的 UI 渲染能力已经被直接集成到了本地工作流中。不再需要进行繁琐的复制粘贴和窗口切换，直接让 AI 提取当前工作区的上下文并自动生成完美页面。
3. **可视化的所见即所得**：UI 设计需要极强的即时视觉反馈。生成后可以直接预览、获取在线链接并直接将产物下载到工作区。

---

## 二、 Stitch 协同实操步骤 (The Handoff SOP)

既然 Stitch 已经自动化接入，我们的主要工作是“指挥 Antigravity 调度 Stitch”。

### 1. 准备“确定性的上下文” (Prerequisites)
切记：**绝对不要让 Stitch 替你发散产品需求！** 它的作用是强悍的“执行画师”，而非“产品经理”。
在调用技能前准备好：
*   **PRD 文档**：如 `产品设计/初步产品设计_PRD.md` 中的目标模块。
*   **交互细节**：如 `产品设计/全流程交互细节.md` 中的状态要求（如加载态、空状态）。

### 2. 下达 UI 灵魂指令 (The Aesthetic Prompt)
除了基本的业务逻辑，还需要给 Antigravity 注入设计灵魂（Design Token），以便其转发给 Stitch：
> “请使用 Stitch UI Design 技能，基于现有的 PRD，为这个应用设计主界面。
> 视觉风格要求：
> - 采用现代、极简的 SaaS 风格（可以参考 Linear 或 Vercel 的设计语言）。
> - 交互细腻：按钮需要有平滑的 Hover 态微动效，关键数据加载时需要顺滑的骨架屏。
> - 色调：请使用冷色调为主（如 Zinc/Slate/Indigo 体系），配合深色模式（Dark Mode）。”

### 3. 自动执行流 (Behind the Scenes)
收到指令后，Antigravity 将自动完成以下流程，你只需等待验收：
1. **锁定上下文**：解析 PRD 确定设计要求。
2. **创建项目**：通过 `mcp_StitchMCP_create_project` 初始化工程。
3. **生成 UI**：通过 `mcp_StitchMCP_generate_screen_from_text` 传递设计 Prompt 和要求，生成高质量前端代码。
4. **资产回传**：提供在线预览链接，或将代码资产（HTML/组件）下载回存至 `UI设计/` 目录。

### 4. 组件化与反馈微调 (Component-Driven)
*   不要试图让 AI 一下子生成整个庞大的中台页面。
*   **按组件攻破**：先设计顶部导航栏（Navbar），再设计核心的数据卡片（Data Card），最后是侧边抽屉（Drawer）。
*   将生成得非常好的组件代码（例如一段极具动效的 `Button`），提取出来作为“团队设计系统规范（Design System）”，**存入 `UI设计/DesignSystem.md`**，指导后续开发。

---

## 三、 从设计到代码的无缝交接

当通过 Stitch 确定了核心页面（通常包含：登录、大盘仪表盘、核心列表、设置页）的高保真样式后，你的“独立产品设计系统”就已经成型。

接下来，带着 Stitch 生成的核心前端组件代码和样式 Token，我们无缝进入**技术设计 (Technical Design)** 与**全面开发**阶段！
