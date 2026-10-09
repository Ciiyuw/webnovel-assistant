# webnovel-assistant · 网文创作助手

服务于作者主导的长篇网文创作。作者决定方向、写正文、做最终取舍；AI 负责讨论、整理、检查和档案维护。

这是一个采用 [Agent Skills 格式](https://agentskills.io/specification) 的技能包，可供 Claude Code、Codex、Cursor 和 OpenCode 使用。无需 API Key、数据库或外部知识库。`webnovel-writer` 是可选集成。

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
使用 webnovel-assistant。我准备另开一本长篇，正文由我写。
先和我讨论故事方向，根据讨论整理定位卡；未确定的内容标为候选。
```

日常不用从头走完整流程，按当前任务调用即可：

| 时机 | 可以这样说 |
|---|---|
| 开新书 | “帮我梳理故事核、读者体验与可持续写作的方向。” |
| 卡文 | “主角现在有这些信息和资源，讨论三种走法与后续代价。” |
| 写前准备 | “准备第 12 章，整理承接、人物知识边界和本章目标，我来写正文。” |
| 检查作者稿 | “检查这个文件的因果、人物和承接问题，先给原文证据与修改建议。” |
| 局部修改 | “按我确认的建议改这一段，保留原稿和候选版本。” |
| 定稿归档 | “这一版已定稿，根据正文更新摘要、人物状态和开放问题，注明出处。” |
| 连载复盘 | “复盘最近五章，结合我的感受和真实反馈，整理下一段的改进。” |

有自己的写作流程、风格样本或知识库时，直接提供路径即可。技能不依赖固定的机器目录。多本书并存时明确本次作品，避免混用设定。

## 文件结构

```text
webnovel-assistant/
├── SKILL.md                         # 入口与合作规则
├── agents/openai.yaml               # Codex 展示元数据
├── references/
│   ├── author-workflow.md           # 六种工作模式
│   ├── project-records.md           # 档案、事实与版本
│   └── webnovel-writer-integration.md
└── assets/templates/                # 七份可裁剪模板
```

七份模板覆盖开书定位、拆书、章节准备、AI 协作约定、作者验收与事实结转、发布反馈、周期复盘。AI 根据对话和材料整理，作者无需填满每张表。仅在任务需要时加载对应参考与模板。

## 创作与事实边界

- 默认由作者写正文；AI 试写和修改按作者指定的范围执行。
- 候选想法、计划、作者确定的设定、定稿已发生事实分别记录。
- 事实检查附原文位置和依据；审美意见说明效果与取舍。
- 保留作者认可的表达，不以统一禁词表改造整章文风。
- AI 模拟阅读意见不充当真实读者数据；发布需作者明确授权。
- 小说正文与作品设定留在书项目，通用方法留在技能包。

## 可选：webnovel-writer

若作品使用 [webnovel-writer](https://github.com/lingfengQAQ/webnovel-writer)，技能会按需读取 [接入边界](references/webnovel-writer-integration.md)，核对实际插件版本与可用工具。

本技能提供独立的作者辅助流程，未实现作者稿自动导入、事实提交或发布脚本。原插件的 `webnovel-write --fast/--minimal` 仍会起草正文，不能当作仅审查作者稿的入口。参考中的插件细节基于 v6.2.1，后续版本须重新核对。

本仓库不包含原插件代码、课程原文、个人知识库内容或任何作品正文。

## 更新

通过 Skills CLI 安装的技能可按其 [更新说明](https://github.com/vercel-labs/skills) 管理；使用 Git 克隆安装的目录可执行 `git pull --ff-only`。若修改过技能，先保存自己的修改，再处理更新。

## 许可

当前未指定开源许可证。仓库公开可读取，安装说明方便作者在自己的工具中使用；公开可见不代表已授予任意转载或再分发许可。
