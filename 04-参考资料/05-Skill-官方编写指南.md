# Skill 编写官方指南

> 本文档翻译自 Claude Code 官方 skill-creator skill 的核心内容，是编写 Skill 的权威参考。

---

## 什么是 Skill？

Skill 是模块化、自包含的包，通过提供专业知识、工作流程和工具来扩展 AI Agent 的能力。

把 Skill 看作是特定领域的"入门指南"——它们把通用 AI 变成配备专业流程知识的专精 AI。

### Skill 能提供什么？

1. **专业工作流** - 特定领域的多步骤流程
2. **工具集成** - 特定文件格式或 API 的操作说明
3. **领域知识** - 公司专属知识、模式、业务逻辑
4. **打包资源** - 复杂重复任务的脚本、参考资料和资产

---

## 核心原则

### 1. 简洁是关键

上下文窗口是公共资源。Skill 与其他内容共享上下文窗口：系统提示、对话历史、其他 Skill 的元数据，以及实际的用户请求。

**默认假设：AI 已经非常聪明。** 只添加 AI 没有的上下文。审视每个信息：AI 真的需要这个解释吗？这个段落值得它的 token 消耗吗？

用简洁的示例替代冗长的解释。

### 2. 设定适当的自由度

根据任务的脆弱性和可变性匹配具体程度：

| 自由度 | 形式 | 适用场景 |
|--------|------|----------|
| **高自由度** | 文本指令 | 多种方法有效、决策依赖上下文、启发式方法指导 |
| **中自由度** | 伪代码或带参数的脚本 | 存在首选模式、可接受一定变化、配置影响行为 |
| **低自由度** | 特定脚本、参数少 | 操作脆弱易错、一致性关键、必须遵循特定顺序 |

把 AI 想象成在探索一条路径：狭窄的桥需要护栏（低自由度），而开阔的田野允许多条路线（高自由度）。

---

## Skill 的结构

每个 Skill 由必需的 `SKILL.md` 文件和可选的打包资源组成：

```
skill-name/
├── SKILL.md (必需)
│   ├── YAML frontmatter 元数据 (必需)
│   │   ├── name: (必需)
│   │   └── description: (必需)
│   └── Markdown 指令 (必需)
│
└── 打包资源 (可选)
    ├── scripts/       - 可执行代码 (Python/Bash 等)
    ├── references/   - 按需加载的参考资料
    └── assets/       - 输出中使用的文件
```

### SKILL.md（必需）

每个 SKILL.md 包含：

- **Frontmatter**（YAML）：包含 `name` 和 `description` 字段。AI 通过这两个字段判断何时使用该 Skill，所以清晰全面地描述 Skill 是什么、以及何时使用非常重要。
- **Body**（Markdown）：使用 Skill 的指令和指南。只在 Skill 触发后加载（如果需要的话）。

### 打包资源（可选）

#### Scripts (`scripts/`)

用于需要确定性可靠性或重复执行的任务的可执行代码。

- **何时包含**：相同的代码被反复重写，或需要确定性可靠性时
- **示例**：`scripts/rotate_pdf.py` - PDF 旋转任务
- **优势**：Token 高效、确定性、可不加载到上下文执行
- **注意**：代码可能仍需 AI 阅读以进行修补或环境调整

#### References (`references/`)

按需加载的文档和参考资料，帮助 AI 工作时参考。

- **何时包含**：AI 应该参考的文档
- **示例**：
  - `references/finance.md` - 财务模式
  - `references/policies.md` - 公司政策
  - `references/api_docs.md` - API 规格说明
- **使用场景**：数据库模式、API 文档、领域知识、公司政策、详细工作流指南
- **优势**：保持 SKILL.md 精简，只在 AI 判断需要时加载
- **最佳实践**：文件大（>10k 字）时，在 SKILL.md 中包含 grep 搜索模式
- **避免重复**：信息只放在 SKILL.md 或 references 文件之一，不要重复。详细资料优先放 references，保持 SKILL.md 精简核心流程

#### Assets (`assets/`)

不打算加载到上下文的文件，而是用在 AI 生成的输出中。

- **何时包含**：Skill 需要在最终输出中使用的文件
- **示例**：
  - `assets/logo.png` - 品牌标识
  - `assets/slides.pptx` - PPT 模板
  - `assets/font.ttf` - 字体
- **使用场景**：模板、图片、图标、样板代码、字体、被复制或修改的示例文档
- **优势**：将输出资源与文档分离，使 AI 无需加载到上下文即可使用文件

---

## description 编写指南

`description` 是 AI 判断何时触发 Skill 的关键。需要清晰、具体、有吸引力。

### 好的 description

```yaml
description: |
  Search for music tracks using the Spotify API. Use when the user asks to 
  "find songs", "search music", "look up artists", or "play something by [artist]".
  Handles playback queue management and playlist creation.
```

### 不好的 description

```yaml
description: |
  This skill helps with music related tasks.
```

### 编写技巧

1. **包含触发词**：列出用户可能说的关键短语
2. **明确边界**：说明该 Skill 能做什么、不能做什么
3. **保持简洁**：description 不是详细文档，只是触发条件

---

## 最佳实践总结

| 原则 | 做法 |
|------|------|
| **简洁** | 只添加 AI 真的不知道的内容 |
| **触发明确** | description 要具体，列出触发词 |
| **文件组织** | 大文件放 references，核心放 SKILL.md |
| **自由度匹配** | 脆弱任务用低自由度，灵活任务用高自由度 |
| **避免重复** | 信息只放一处 |

---

*原文来自 Claude Code skill-creator skill，翻译整理自 https://github.com/anthropics/claude-code/tree/main/plugins/plugin-dev*
