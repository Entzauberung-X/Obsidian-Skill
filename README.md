# Obsidian-Skill

这是一个用于 Obsidian 的扩展/插件（或“Skill”）项目，旨在将 AI 助手功能整合到 Obsidian 笔记工作流中，帮助加速写作、整理知识与生成内容模板。README 在此提供安装、配置、使用和开发说明；如果你的项目目标不同，可以在此基础上调整内容。

## 什么是 Skill

Skill 是一个**可复用的工作流包**，由 SKILL.md（YAML frontmatter + Markdown 指令）+ 可选的脚本/模板/参考文档组成。

核心机制是 **渐进式披露（Progressive Disclosure）**：
- 启动时只加载 `name` + `description`（约 100 tokens/skill）
- Claude 按任务匹配 description，**命中后才加载完整指令**
- 支持文件仅在显式需要时加载

## 设计原则

1. 职责单一 (Single Responsibility)
一个Skill只做一件事，并且把它做好。职责单一、边界清晰的Skill更容易在正确的时机被选中并稳定执行。

2. 边界明确 (Clear Boundaries)
这是Skill稳定性的基石。模型最容易犯的错误，就是“不知道什么时候该做”。因此，必须明确界定：

正向条件：明确什么情况下触发该Skill。

负向条件：明确什么情况下不触发该Skill。

输入输出：用清晰、结构化的方式定义Skill的Input和Output，如同定义函数的签名（Signature）。

3. 步骤可执行 (Actionable Steps)
Skill的核心是“步骤”，必须是指令式、具体的动作，而不是概括性的描述。要确保模型可以按部就班地执行。

4. 失败策略完备 (Graceful Failure)
必须预定义“失败路径”，告诉模型在不同异常情况下该如何处理，而不是让它自由发挥。

## 主要功能

- AI 辅助内容生成：基于提示生成笔记、提纲、总结和扩展段落。
- 模板与快捷命令：通过自定义模板快速插入常用结构（会议记录、读书笔记、代码片段等）。
- 本地/远程模型支持：支持配置第三方 LLM 服务（如 OpenAI、Azure、或其他兼容 API）。
- 热键与命令面板：在 Obsidian 命令面板或自定义热键中触发 Skill 功能。
- 可配置化：通过设置面板配置 API Key、默认提示、输出格式等。

## 要求

- Obsidian（建议最新版）
- Node.js & npm（仅在开发或本地构建时需要）
- 可选：OpenAI API Key 或其他 LLM 服务的凭证

## 安装（用户）

方法一：使用社区插件（如果已打包并发布）
1. 在 Obsidian 中打开「设置」→「社区插件」→ 搜索并安装 `Obsidian-Skill`。

方法二：手动安装
1. 克隆仓库或下载 ZIP。
2. 将插件文件夹放入你的 Vault 下的 `.obsidian/plugins/` 目录（创建该目录如果不存在）。
3. 在 Obsidian 的「设置」→「社区插件」中启用该插件。

## 配置

1. 打开 Obsidian 设置 → 插件 → Obsidian-Skill。
2. 在设置中填入你的 LLM 服务 API Key（例如 OpenAI 的 API Key）。
3. 配置默认模型、温度（creativity）、最大 tokens 等参数。
4. 根据需要自定义提示模板（Prompts）和快捷命令。

## 使用示例

- 在笔记中，选中一段文字，使用命令面板运行 `Obsidian-Skill: 扩展/改写选中文本`，插件会基于配置生成改写或扩展内容并插入。
- 使用 `Obsidian-Skill: 生成会议纪要` 命令，会基于会议要点生成结构化纪要。
- 通过 `Obsidian-Skill: 生成读书笔记` 快捷命令，自动将摘录整理成笔记模板。

（提示：具体命令名会根据插件实现而不同，参考插件设置页或命令面板中的条目）

## 开发

1. 安装依赖：

```bash
npm install
```

2. 本地开发（热加载）：

```bash
npm run dev
```

3. 打包发布：

```bash
npm run build
```

4. 将构建产物复制到 `.obsidian/plugins/<plugin-id>/` 下进行测试。

## 自定义提示（Prompts）示例

- 会议纪要："请基于以下会议要点生成一份简洁的会议纪要，包含结论、行动项与负责人：\n{{content}}"
- 阅读总结："将下面的文本浓缩为 5 个要点并给出 2 个可执行的反思/行动建议：\n{{content}}"

## 隐私与安全

- 请勿在未受信任的环境中暴露 API Key。
- 插件默认不上传你的 Vault 内容到任何第三方，除非你在配置中明确允许（或在实现中启用了远程处理）。如果插件需要发送数据到远端 LLM，请在设置中提供明确提示并在文档中说明。

## 贡献

欢迎贡献！你可以：
- 提交 Issue 报告 bug 或建议功能
- 提交 Pull Request 添加功能或修复问题
- 在 Discussions 中提出想法或使用场景

贡献流程：Fork → 新分支 → 提交 → 发起 PR。

## 许可

默认使用 MIT 许可证（根据需要替换为其他许可证）。
