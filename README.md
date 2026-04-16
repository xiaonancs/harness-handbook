# Claude Code 源码解析

![cover](book-cover-banner.png)

## 引言

本书基于 `restored-src v2.1.88` 的源码快照写成。
<br><br>写作重点不在使用说明，而在结构、约束、边界与实现。如果把 Claude Code 只看成"会写代码的命令行工具"，许多设计都会显得过重；如果把它放回到 Agent 运行时系统的语境中，启动链路、上下文管理、权限体系、任务调度、终端渲染与扩展协议之间的关系就会清晰得多。因此采用"结构先于结论"的写法：先交代对象、边界与路径，再讨论判断与启示。

## 全书结构

全书采用"两层前言 + 三部正文"的展开方式。

- `总纲A` 是导论，交代社区讨论的背景、问题意识和阅读这本书的理由。
- `总纲B` 是方法篇，交代理解 Claude Code 时最重要的技术主线，尤其是 harness、context、permissions 与 runtime 的关系。
- `Part I Foundations` 处理入口、启动、状态、提示词、主循环、上下文、记忆与缓存。
- `Part II Execution` 处理工具、安全、权限、配置、命令、Agent、任务、MCP 与 Hooks。
- `Part III Infrastructure` 处理特性开关、API 适配、渲染引擎与设计系统。
- 附录收纳扩展点、架构模式、消息附件、LSP 与源码归档。

`总纲A` 负责提出问题，`总纲B` 负责给出读法，正文三部则分别展开系统的基础层、执行层与工程层。

## 参考来源

- **Claude-Code-Source-Study** — 25 篇同主题深度分析，包含详细源码引用和设计模式分析
- **Harness 技术深度分析** — 基于源码的 Harness 核心技术完整剖析
- **全网 120+ 篇技术文章调研** — 社区认知的系统性梳理与误解纠正
- **Anthropic 官方工程博客** — 第一手的设计意图和架构决策

## 目录

### 总纲

- [全网技术文章调研与核心认知](总纲A-全网技术文章调研与核心认知.md)
- [Harness 技术深度分析](总纲B-Claude-Code-Harness技术深度分析.md)

### Part I Foundations

| 章节 | 提要 |
|------|------|
| [项目全景](Part%20I%20Foundations/01-项目全景.md) | 从入口到模块划分的整体轮廓 |
| [启动优化](Part%20I%20Foundations/02-启动优化.md) | 一条为冷启动让路的执行链 |
| [状态管理](Part%20I%20Foundations/03-状态管理.md) | React 内外状态之间的桥接方式 |
| [System Prompt](Part%20I%20Foundations/04-SystemPrompt.md) | 系统提示词的分层组装 |
| [对话循环](Part%20I%20Foundations/05-对话循环.md) | 主循环与恢复分支的组织 |
| [上下文管理](Part%20I%20Foundations/06-上下文管理.md) | 预算与压缩路径的设计 |
| [Memory](Part%20I%20Foundations/07-Memory.md) | 记忆写入与召回路径 |
| [Prompt Cache](Part%20I%20Foundations/08-PromptCache.md) | 缓存边界与成本控制 |
| [Thinking 与推理](Part%20I%20Foundations/09-Thinking与推理.md) | 推理深度的控制面 |

### Part II Execution

| 章节 | 提要 |
|------|------|
| [工具系统](Part%20II%20Execution/10-工具系统.md) | 工具抽象与注册机制 |
| [BashTool](Part%20II%20Execution/11-BashTool.md) | 命令执行与安全约束的交汇点 |
| [权限系统](Part%20II%20Execution/12-权限系统.md) | 权限与沙箱的分层判定 |
| [Settings](Part%20II%20Execution/13-Settings.md) | 配置合并与企业策略 |
| [命令系统](Part%20II%20Execution/14-命令系统.md) | 命令加载与扩展分发 |
| [Agent 系统](Part%20II%20Execution/15-Agent系统.md) | 子 Agent 的隔离与共享 |
| [内置 Agent](Part%20II%20Execution/16-内置Agent.md) | 角色化 Prompt 的组织方式 |
| [任务系统](Part%20II%20Execution/17-任务系统.md) | 任务执行与前后台切换 |
| [MCP](Part%20II%20Execution/18-MCP.md) | 外部工具接入的协议层 |
| [Hooks](Part%20II%20Execution/19-Hooks.md) | 生命周期自动化与执行边界 |

### Part III Infrastructure

| 章节 | 提要 |
|------|------|
| [Feature Flag](Part%20III%20Infrastructure/20-FeatureFlag.md) | 特性开关与构建裁剪 |
| [API 调用](Part%20III%20Infrastructure/21-API调用.md) | 不可靠网络下的请求恢复 |
| [Ink 引擎](Part%20III%20Infrastructure/22-Ink引擎.md) | 终端渲染管线的自定义实现 |
| [设计系统](Part%20III%20Infrastructure/23-设计系统.md) | 终端界面的组件化组织 |

### Appendix

- [附录A Skill 与 Plugin](Appendix/A1-Skill与Plugin.md) — 扩展点与打包路径
- [附录B 架构模式](Appendix/A2-架构模式.md) — 可迁移的设计抽象
- [附录C 消息与附件](Appendix/A3-消息与附件.md) — 消息管线与附件处理
- [附录D LSP 集成](Appendix/A4-LSP集成.md) — 代码智能的协议接口
- [源码归档](Appendix/claude-code-src-2.1.88.zip) — restored-src v2.1.88 源码快照

## 源码基线

- **版本**: Claude Code v2.1.88
- **文件数**: 1,884 个 TypeScript/TSX 源文件
- **代码行数**: 513,216 行
- **技术栈**: TypeScript + Bun + React/Ink (Fork) + Yoga (Fork)

## License

本书内容基于对公开可获取信息的分析和评论，用于教育和研究目的。
