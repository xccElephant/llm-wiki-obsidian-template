# Agent Wiki

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Obsidian Compatible](https://img.shields.io/badge/Obsidian-compatible-7C3AED)
![Cursor](https://img.shields.io/badge/Cursor-supported-111827)
![Claude Code](https://img.shields.io/badge/Claude_Code-supported-111827)
![Codex](https://img.shields.io/badge/Codex-supported-111827)

[English](README.md) | [简体中文](README_zh.md)

一个会随着资料持续生长的、由 agent 维护的持久化 wiki。

把原始资料放进 `raw/`。你的 agent 会读取它们、提炼知识、建立交叉链接，并维护成一个会不断积累的 Markdown wiki。

![展示由摄入资料逐步生长出来的 Obsidian graph view](assets/obsidian-graph-view.png)

Obsidian 是最适合浏览结果的查看器，但知识本身保存在纯 Markdown 中，同时适配 Cursor、Claude Code 和 Codex 风格 agent。

## 这个项目解决什么问题

大多数笔记系统仍然要求你自己做维护工作：

- 自己读原文
- 自己写摘要
- 自己拆分概念页
- 自己补链接
- 自己记住后来发生了什么变化

`agent-wiki` 的核心思路是把这些维护工作交给 agent。你保留原始资料，agent 负责维护派生出来的 wiki。

## 快速开始

1. 把这个仓库克隆到一个新 vault 或空目录里：

```bash
git clone https://github.com/xccElephant/agent-wiki.git
cd agent-wiki
```

2. 运行引导脚本，生成起始文件：

```bash
./install.sh
```

3. 把资料放进 `raw/articles/`，然后同时在 Obsidian 和你的 coding agent 中打开这个目录。

接着让 agent 摄入资料、更新相关 wiki 页面，或者直接基于已编译的 wiki 回答问题。

## 你会得到什么

- `raw/`：不可变的原始资料层
- `wiki/`：由 agent 维护的知识层
- `wiki/source-notes/`：每个来源一篇派生笔记
- `wiki/entities/`、`wiki/concepts/`、`wiki/synthesis/`：不同类型的持久知识页
- `logs/log.md`：记录 ingest 和维护历史
- `AGENTS.md`、`CLAUDE.md` 和 `.cursor/rules/`：为不同 agent 提供工作流约束

## 为什么它会越用越强

- 一份新资料可以同时更新多个下游页面，而不是只留下一个孤立摘要。
- 查询得到的高价值答案可以继续回写到 `wiki/synthesis/`，形成新的持久知识。
- 原始文件保持不变，所以来源层始终可审计、可回溯。
- 借助 Obsidian 的 backlinks 和 graph view，整个知识结构会越来越容易浏览。

## Agent Wiki、RAG 和普通笔记的区别

| 工作流 | 主要单位 | 每次提问时发生什么 | 会长期积累什么 |
| --- | --- | --- | --- |
| 聊天记录 | 消息 | 模型从过去对话里继续推理 | 脆弱上下文 |
| RAG | 文本块 | 模型每次都从检索到的 chunks 重新组织答案 | 检索索引 |
| 手写笔记 | 你手工维护的页面 | 你自己维护摘要、链接和结构 | 分散笔记 |
| Agent Wiki | 被维护的 Markdown 页面 | agent 基于已综合过的知识作答，并可把新综合结果回写 | 持久的互联 wiki |

## 它是怎么工作的

```text
原始资料 -> 来源笔记 -> 实体 / 概念 / 综合页 -> index 和 log
```

- `raw/` 是不可变的来源层。
- `wiki/` 是被维护的知识层。
- `schemas/` 和 agent 指令文件定义 ingest、query 和 lint 的行为。
- `install.sh` 用来生成 `wiki/index.md`、`logs/log.md` 等起始文件。

## 用在已有 Obsidian Vault 中

如果你已经有自己的 Obsidian vault，可以把这些内容复制进去：

- `AGENTS.md`
- `CLAUDE.md`
- `.cursor/rules/`
- `raw/`
- `wiki/`
- `logs/`
- `schemas/`
- `install.sh`

然后运行：

```bash
./install.sh
```

这个仓库有意只跟踪起始文件、模板和工作流规则，而不是你日常维护的真实知识库内容。

## Agent 兼容性

- **Cursor** 读取 `.cursor/rules/`，也可以同时参考 `AGENTS.md`
- **Claude Code** 读取 `CLAUDE.md`
- **Codex 风格 agent** 读取 `AGENTS.md`

如果你修改了工作流，最好保持 `AGENTS.md` 和 `CLAUDE.md` 一致。

## 示例提示词

- `Read AGENTS.md and ingest raw/articles/article.md into wiki/source-notes/. Update related concept or entity pages and append to logs/log.md.`
- `Read CLAUDE.md and ingest raw/articles/article.md into wiki/source-notes/. Update related concept or entity pages and append to logs/log.md.`
- `Read wiki/index.md and answer: what do we currently know about <topic>? File the answer back into wiki/synthesis/ if it is durable.`
- `Lint this vault for unsupported claims, stale syntheses, missing source-notes, orphan pages, and broken wikilinks.`

## 项目结构

```text
.
├── assets/               # 截图和展示素材
├── docs/                 # 包装与补充说明文档
├── raw/                  # 不可变原始资料
├── wiki/                 # 被维护的知识页面
├── logs/                 # 追加式操作历史
├── schemas/              # 工作流与结构文档
├── AGENTS.md             # Codex 风格说明
├── CLAUDE.md             # Claude Code 说明
├── .cursor/rules/        # Cursor 规则
└── install.sh            # 起始文件引导脚本
```

如果你要同步修改 GitHub 仓库名、描述和 topics，可以参考 `docs/github-metadata.md`。

## 致谢

灵感来自 Andrej Karpathy 提出的 **LLM Wiki**：

- [Karpathy gist: LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f#file-llm-wiki-md)

这个仓库是一个独立的实现模板和工作流起点，不是原始 concept note，也不是 Karpathy 官方仓库。

## License

MIT.
