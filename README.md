# Harness Handbook

![hero](harness-handbook-hero.png)

AI Agent 系统是如何被构造的

---

## 这是什么

Harness Handbook 是一组围绕 AI Agent 运行时系统展开的技术分析资料。它不讨论如何使用某个产品，而是讨论这类系统在工程上是如何被构造的：启动链路、上下文管理、权限体系、工具系统、任务调度、终端渲染、扩展协议。

目前收录的主要内容是基于 Claude Code v2.1.88 源码快照的完整解析。

## 收录内容

### [Claude Code 源码解析](Claude%20Code%20Source%20Analysis/README.md)

基于 `restored-src v2.1.88`（1,884 个 TypeScript 文件，513,216 行）的系统性逆向工程分析，共 23 章 + 4 篇附录。

- **Part I Foundations** — 入口、启动、状态、提示词、主循环、上下文、缓存、推理
- **Part II Execution** — 工具、命令、Agent、任务、MCP、权限、配置、Hooks
- **Part III Infrastructure** — 特性开关、API 适配、渲染引擎、设计系统、记忆

### 其他资料

- [全网技术文章调研与核心认知](Claude%20Code%20Source%20Analysis/总纲A-全网技术文章调研与核心认知.md) — 120+ 篇文章的社区认知梳理
- [Harness 技术深度分析](Claude%20Code%20Source%20Analysis/总纲B-Claude-Code-Harness技术深度分析.md) — 从 harness 视角的技术主线提炼

## 源码来源

> **声明**：源码版权归 [Anthropic](https://www.anthropic.com) 所有。本仓库为非官方整理，基于公开 npm 发布包与 source map 分析还原，仅供研究与教育使用。

- npm 包：[@anthropic-ai/claude-code](https://www.npmjs.com/package/@anthropic-ai/claude-code)
- 还原版本：`2.1.88`
- 还原文件数：4,756 个（含 1,884 个 `.ts`/`.tsx` 源文件）
- 还原方式：提取 `cli.js.map` 中的 `sourcesContent` 字段
- 源码归档：[claude-code-src-2.1.88.zip](Claude%20Code%20Source%20Analysis/Appendix/claude-code-src-2.1.88.zip)

## License

本仓库内容基于对公开可获取信息的分析和评论，用于教育和研究目的。
