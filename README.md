# Obsidian-Skill

Obsidian-Skill 是一组面向 Obsidian 的“Skill”工作流包，用于把可执行的写作/整理/笔记规范、模板和 AI 辅助提示集成到 Obsidian 笔记流程中。

核心理念：把可重复的笔记活动抽象为职责单一、边界明确、可执行的 Skill（由一个 SKILL.md + 可选参考文件组成），并通过渐进式披露只在需要时加载完整指令。

---

## 主要用途

- 为 Obsidian 提供可配置、可复用的笔记工作流（模板、输出规范、生成器）。
- 将 LLM（本地或远端）整合到笔记写作、整理、格式化、生成练习题与计划编制等任务中。
- 包含多套已成型的 Skill，覆盖信号与系统、工程数学与考研数学一的笔记规范与计划生成。

---

## 本仓库的 Skill（摘要）

仓库以子目录形式组织每个 Skill，每个 Skill 的说明存放在对应目录下的 `SKILL.md` 中。当前包含：

- book-note-organizer — 教科书/书籍笔记组织器：把一本书拆成章节笔记、索引与专题，保证每章有比较表、公式块与易错点。
- engineering-math-organizer — 工程数学笔记体系：面向工程应用的数学笔记规范，包含“思维外化”模板（错题归因、思路轨迹）与健康检查。
- math-formula-organizer — 考研数学一公式笔记系统：章节公式速查、专题、二级结论、错题归因与思路轨迹模版。
- math-note-pattern-sync — 数学笔记模式同步：跨章节/跨科目的模式与格式化规范（编号、模板、审计与同步流程）。
- signals-systems-organizer — 信号与系统（奥本海姆）笔记体系统一规范：本质优先的方法笔记模板、三层结构与综合练习生成规则。
- signals-qianghua-planner — 843 信号与系统强化阶段计划生成器：按考纲权重拆周、生成强化计划与待补笔记清单（只写计划文件，不改已有笔记）。

---

## 代码与运行

本仓库主要是 Markdown 规范与模板，包含少量开发脚本（如果需要把 Skill 打包为 Obsidian 插件，请参阅下文开发段）。若你要开发或打包插件：

1. 安装依赖（开发环境）：

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

4. 将构建产物复制到 `.obsidian/plugins/<plugin-id>/` 进行测试。


---

## 仓库结构（顶层目录）

```text
book-note-organizer/            # 教科书笔记拆分与组织规范
engineering-math-organizer/     # 工程数学笔记体系 + 模板与健康检查
math-formula-organizer/         # 考研数学一公式汇总、专题与速查
math-note-pattern-sync/         # 数学笔记模式同步与审计流程
signals-qianghua-planner/       # 843 强化阶段计划生成器（计划文件，不改已有笔记）
signals-systems-organizer/      # 信号与系统（奥本海姆）笔记与方法体系
README.md                       # 本文件
```

如何配合使用：每个 Skill 目录下有 `SKILL.md`（frontmatter + 说明），在需要运行或调用该 Skill 的时候先阅读 `SKILL.md`，遵守其中的安全规则（例如只追加、不覆盖现有笔记、不得编造真题等）。

---

## 使用建议与注意事项

- 每次按 Skill 写作或批量修改前，先阅读目标 Skill 的 `SKILL.md`，遵守其中的安全与格式化规则（死链检测、表格内裸竖线检测、frontmatter 要求等）。
- 仓库中许多 Skill 强调“本质优先”（先讲为什么再讲怎么做）和“思维外化”（把顿悟与错题归因写进笔记），把笔记当活档案维护。 
- Skill 的职责通常限定明确（某个 Skill 只负责生成计划或只负责生成练习），不要跨 Skill 修改已有笔记内容，除非 Skill 明确允许。

---

## 贡献

欢迎贡献 Skill、Issue 或 PR：Fork → 新分支 → 提交 → 发起 PR。贡献前请先阅读并遵守各 Skill 目录下的 `SKILL.md` 中的安全与写作规则。

---

## 许可

MIT
