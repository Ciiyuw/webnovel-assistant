# webnovel-assistant · 网文共创助手

服务于长篇网文人机共创。双方共同扫榜、构思、设计剧情与情绪，也可以接力写正文；作者决定采用与定稿，AI 主动提出走法、检查和维护跨卷档案。

这是一个采用 [Agent Skills 格式](https://agentskills.io/specification) 的技能包，可供 Claude Code、Codex、Cursor 和 OpenCode 使用。基础文档共创无需 API Key、数据库或外部知识库。实际扫榜使用宿主可用的搜索、网页/浏览器阅读、作者提供的文件或已授权数据服务，覆盖范围按真实来源确定。`webnovel-writer` 与 Oh Story 是可选集成。

## 安装

在已安装 Node.js 的终端运行：

```bash
npx skills add Ciiyuw/webnovel-assistant --skill webnovel-assistant -g -a claude-code -a codex -a cursor -a opencode
```

该命令使用 [Skills CLI](https://github.com/vercel-labs/skills)，全局安装到所选工具支持的技能目录。只需一个工具时，保留相应的 `-a` 参数即可。安装时确认 CLI 显示的目标目录；若已有同名技能，先备份自己的改动。

先查看可识别的技能：

```bash
npx skills add Ciiyuw/webnovel-assistant --list
```

### 手动安装

也可以直接克隆到某个工具的全局技能目录，选择其中一条执行：

| 工具 | 全局技能目录 | 官方说明 |
|---|---|---|
| Claude Code | `~/.claude/skills/webnovel-assistant` | [Skills](https://code.claude.com/docs/en/skills) |
| Codex | `~/.agents/skills/webnovel-assistant` | [Build skills](https://learn.chatgpt.com/docs/build-skills) |
| Cursor | `~/.cursor/skills/webnovel-assistant` | [Agent Skills](https://cursor.com/docs/skills) |
| OpenCode | `~/.config/opencode/skills/webnovel-assistant` | [Agent Skills](https://opencode.ai/docs/skills/) |

```bash
# Claude Code
git clone https://github.com/Ciiyuw/webnovel-assistant.git ~/.claude/skills/webnovel-assistant

# Codex
git clone https://github.com/Ciiyuw/webnovel-assistant.git ~/.agents/skills/webnovel-assistant

# Cursor
git clone https://github.com/Ciiyuw/webnovel-assistant.git ~/.cursor/skills/webnovel-assistant

# OpenCode
git clone https://github.com/Ciiyuw/webnovel-assistant.git ~/.config/opencode/skills/webnovel-assistant
```

目标目录已存在时不要直接覆盖。安装后新开会话，或按宿主的技能刷新方式加载。技能安装在本机，云端或其他机器需在对应环境另行安装。

## 使用

在作品项目中开启会话，说明书项目路径和当前任务。Claude Code 可显式输入 `/webnovel-assistant`；Codex 可用 `$webnovel-assistant`。其他工具可在技能列表选择，或在请求中明确使用该技能。

```text
使用 webnovel-assistant。我想和你共同创作一本长篇。
先讨论故事方向、剧情与情绪；近几章详细，远期保留方向和备选。这轮不写正文。
```

日常不用从头走完整流程，按当前任务调用即可：

| 时机 | 可以这样说 |
|---|---|
| 扫榜拆书 | “查这个平台的同类新书榜，注明数据日期、出处和覆盖，再选作品共同拆书。” |
| 榜单变化 | “比较这两份同口径快照，区分指标变化、名次变化和进入/退出可见样本。” |
| 开新书 | “一起构思故事核、读者体验与可持续写作的方向。” |
| 卡文 | “主角现在有这些信息和资源，讨论三种走法与后续代价。” |
| 写前准备 | “准备第 12 章，整理承接、人物知识边界和本章目标，我来写正文。” |
| 正文共创 | “按已采纳计划起草第 12 章，或从我的停笔处接力，另存候选稿。” |
| 检查稿件 | “检查这个文件的因果、人物和承接问题，先给原文证据与修改建议。” |
| 局部修改 | “按我确认的建议改这一段，保留原稿和候选版本。” |
| 定稿归档 | “这一版已定稿，根据正文更新摘要、人物状态和开放问题，注明出处。” |
| 换卷交接 | “根据本卷定稿整理人物变化、知情边界、伏笔与承诺，延续到下一卷。” |
| 连载复盘 | “复盘这个故事段，结合我的感受和真实反馈，只细化接下来需要写的部分。” |

有自己的写作流程、风格样本或知识库时，直接提供路径即可。技能不依赖固定的机器目录。多本书并存时明确本次作品，避免混用设定。

## 文件结构

```text
webnovel-assistant/
├── SKILL.md                         # 入口与合作规则
├── agents/openai.yaml               # Codex 展示元数据
├── references/
│   ├── author-workflow.md           # 共创、滚动规划、剧情与情绪
│   ├── market-reading.md            # 扫榜与共同拆书
│   ├── rank-data.md                 # 获取、查询、快照与历史比较
│   ├── project-records.md           # 分卷记忆、事实与版本
│   ├── webnovel-writer-integration.md
│   └── oh-story-integration.md
└── assets/templates/                # 十份可裁剪模板
```

十份模板覆盖开书定位、拆书、章节准备、AI 协作约定、稿件验收与事实结转、发布反馈、周期复盘、故事段与情绪设计、卷末交接及扫榜观察。AI 根据对话和材料整理，作者无需填满每张表。仅在任务需要时加载对应参考与模板。

扫榜按找方向、找对标、查作品、看变化或准备拆书选择材料。使用 [榜单数据获取与比较](references/rank-data.md) 核对日期、筛选、分页与指标口径；按需保存 [扫榜观察单](assets/templates/10-扫榜观察单.md)。只有同口径历史快照才比较变化，只有实际可读正文才分析具体开局与剧情。

## 创作与事实边界

- 按任务选择作者独写、AI 起草、接力或逐场景共写；只讨论或规划时不自动进入正文。
- 近章详细、当前故事段抓节点、远期保留方向；双方都可以提出关键转折，由作者取舍。
- 分卷目录配合全书档案和按章读取，换卷延续人物、伏笔、承诺及知情边界。
- 候选想法、计划、作者确定的设定、定稿已发生事实分别记录。
- 事实检查附原文位置和依据；审美意见说明效果与取舍。
- 保留作者认可的表达，不以统一禁词表改造整章文风。
- AI 模拟阅读意见不充当真实读者数据；发布需作者明确授权。
- 小说正文与作品设定留在书项目，通用方法留在技能包。

## 可选：webnovel-writer

若作品使用 [webnovel-writer](https://github.com/lingfengQAQ/webnovel-writer)，技能会按需读取 [接入边界](references/webnovel-writer-integration.md)，核对实际插件版本与可用工具。

本技能提供独立的文档共创流程，未实现作者稿或共创最终稿的自动导入、插件事实提交或发布脚本。原插件的 `webnovel-write --fast/--minimal` 仍会起草正文，不能当作仅审查作者稿的入口。参考中的插件细节基于 v6.2.1，后续版本须重新核对。

## 可选：Oh Story

作者要求接入 [Oh Story](https://github.com/zenstory-ai/oh-story-claudecode) 或作品已有其追踪状态时，读取 [接入边界](references/oh-story-integration.md)，核对实际版本与工具。两套系统的方法可以参考，同一本书的运行事实只由一套系统维护，不双写状态或手改派生视图。候选稿、作者定稿与系统提交分别报告。

本仓库不包含上游代码、课程原文、个人知识库全文或任何作品正文。

## 更新

通过 Skills CLI 安装的技能可按其 [更新说明](https://github.com/vercel-labs/skills) 管理；使用 Git 克隆安装的目录可执行 `git pull --ff-only`。若修改过技能，先保存自己的修改，再处理更新。

## 许可

本 skill 采用 [MIT 许可证](LICENSE) 开源，可使用、修改和分发，包括商业用途；分发时保留版权及许可声明。外部参考项目按其各自许可证使用，本仓库不包含它们的代码。
