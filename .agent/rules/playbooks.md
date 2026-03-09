# Multi-AI DevOps Playbooks

## Playbook 1: Adding a new Guide (指南)
1. **Initial Search**: 使用 `find_by_name` 查找同类指南。
2. **Template Alignment**: 参照 `技术设计指南.md` 的结构设计大纲。
3. **Cross-Link Check**: 使用 `grep_search` 查找关键词，并在相关指南中添加双向链接。
4. **Validation**: 运行 `markdownlint` (如有) 检查语法。

## Playbook 2: Updating a Skill (专属技能)
1. **Read SKILL.md**: 完整阅读现有的指令集。
2. **Isolated Edit**: 仅修改目标函数或指令块。
3. **Internal Test**: 在 `task.md` 中记录对该技能修改后的具体验证步骤。
4. **Documentation**: 更新技能的版本或更新日志。
