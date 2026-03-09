# 独立产品 UI 设计指南 (基于 Stitch)

在明确了 `产品设计/全流程交互细节.md` 之后，我们需要将枯燥的线框图和流程图转化为高保真的 UI 界面。

目前在 AI 驱动的 UI 领域，虽然理想状态是全流程都能在 Antigravity 中完成并直接输出前端代码，但当下的最佳实践（Sweet Spot）是引入 **Stitch** 这类专注于前端与 UI 设计的 AI 工具进行承接。

---

## 一、 为什么现阶段选择 Stitch？

1. **术业有专攻**：Antigravity 擅长全栈架构、复杂后端逻辑与长下文文档的“状态管理”；而 Stitch 的模型经过高度的前端 UI 渲染和交互调优，能极快地生成不仅“跑得通”而且“好看”的 React/Vue 组件。
2. **可视化的所见即所得**：UI 设计需要极强的即时视觉反馈。Stitch 的环境允许我们在输入指令后立刻看到组件的渲染效果，这是纯文本 IDE 暂时无法替代的体验。

> 💡 **未来展望：MCP (Model Context Protocol) 的打通**
> Stitch 官方已经声明支持 MCP 协议。这意味着在未来不久，我们可以直接在 Antigravity 中通过 MCP Server 唤起 Stitch 的 UI 渲染能力！
> 届时，“写完 PRD -> Antigravity 直接下发指令给 Stitch Worker -> 原地在 IDE 中预览生成的炫酷登录页” 的全闭环神仙操作将成为现实！
> 但在此之前，手动将 Antigravity 的产出“喂”给 Stitch 依然是最高效的过渡态。

---

## 二、 Stitch 协同实操步骤 (The Handoff SOP)

### 1. 投喂“确定性的上下文”
切记：**绝对不要让 Stitch 替你发散产品需求！** 它的作用是强悍的“执行画师”，而非“产品经理”。
打开 Stitch，直接将你在 Antigravity 中沉淀的心血丢进去：
*   复制 `产品设计/初步产品设计_PRD.md` 中的目标模块。
*   复制 `产品设计/全流程交互细节.md` 中的状态要求（如加载态、空状态）。

### 2. 设定 UI 灵魂提示词 (The Aesthetic Prompt)
除了业务逻辑，还需要给 Stitch 注入设计灵魂（Design Token）。这是一个通用且好用的 Prompt 模板：
> “请基于我刚刚提供的 PRD，为这个应用设计主界面。
> 视觉风格要求：
> - 采用现代、极简的 SaaS 风格（可以参考 Linear 或 Vercel 的设计语言）。
> - 交互细腻：按钮需要有平滑的 Hover 态微动效，关键数据加载时需要顺滑的骨架屏。
> - 色调：请使用冷色调为主（如 Slate/Indigo 体系），配合深色模式（Dark Mode）。
> 请直接生成相关的 React/Tailwind [或你所用的技术栈] 代码并预览。”

### 3. 组件化与反馈微调 (Component-Driven)
*   不要让 Stitch 一下子生成整个庞大的中台页面。
*   **按组件攻破**：先让它画顶部导航栏（Navbar），再画核心的数据卡片（Data Card），最后画侧边抽屉（Drawer）。
*   将你觉得生成得非常好的组件代码（例如一段极具动效的 `Button.tsx`），提取出来，作为“团队设计系统规范（Design System）”，**反向复制回你的 Antigravity 工作区**中，存入 `UI设计/DesignSystem.md` 或具体的代码库中。

---

## 三、 从设计到代码的无缝交接

当在 Stitch 中确定了核心四个页面（通常包含：登录、大盘仪表盘、核心列表、设置页）的高保真样式后，你的“独立产品设计系统”就已经成型。

接下来，带着 Stitch 生成的核心前端组件代码和样式 Token，我们要重新杀回 Antigravity 工作区，进入**技术设计 (Technical Design)** 与**全面开发**阶段！
