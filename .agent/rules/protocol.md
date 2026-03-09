# Multi-AI DevOps Protocol (Workspace)

This protocol defines the engineering standards for the `Multi-ai-devops` repository.

## 1. Repository Context
`Multi-ai-devops` is a documentation-driven initiative to define guidelines and skills for high-quality, multi-agent AI development. The "stability backbone" of this repository consists of the `.agents/skills` and various `*指南.md` (Guideline) files.

## 2. Engineering Principles (Mandatory)
- **KISS (Keep It Simple, Stupid)**: 优先使用清晰的 Markdown 结构，避免复杂的交叉引用。
- **YAGNI (You Aren't Gonna Need It)**: 不要添加尚未被主流 AI 最佳实践证明有效的 speculative rules。
- **DRY + Rule of Three**: 仅在同样的提示词模式出现三次后，才考虑提取为全局 Skill 或 Workflow。

## 3. Risk Tiers
- **Low Risk**: 拼写纠正、格式微调、非核心文档（如 README 补充）。
- **Medium Risk**: 新增指南文件、修改现有指南逻辑。
- **High Risk**: 修改 `.agents/skills/` 核心逻辑、修改 `GEMINI.md` 全局配置。

## 4. Vibe Coding Guardrails
- **Verification First**: 在修改指南前，使用 `grep_search` 确认是否与其他指南存在逻辑冲突。
- **Small Batches**: 禁止在一个任务中混合“重构指南结构”和“新增指南内容”。
