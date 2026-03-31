# Claude Code 上下文与记忆

> 这篇文档聚焦 Claude Code 里的“上下文是怎么来的”，以及 `CLAUDE.md`、`settings.json`、Skills、MCP 之间是什么关系。
> 最后核对时间：2026-03-30

---

## 1. Claude Code 里的上下文不只有聊天记录

根据 Claude Code 官方文档，Claude Code 会综合多种来源来形成当前会话的上下文。

官方 `settings` 文档里明确提到几类来源：

- `CLAUDE.md` 记忆文件
- `settings.json` 配置文件
- Skills
- MCP servers

所以你可以把“上下文”理解成：

> Claude 在当前项目里做决定时所依赖的全部信息来源。

---

## 2. `CLAUDE.md` 是最核心的项目上下文入口

官方 `memory` 文档说明：

- `./CLAUDE.md` 或 `./.claude/CLAUDE.md` 可以作为项目级说明
- `~/.claude/CLAUDE.md` 是用户级个人偏好
- 更高层级的 `CLAUDE.md` 会先加载
- 子目录中的 `CLAUDE.md` 会按需加载

这意味着 `CLAUDE.md` 不是“一个随便放的说明文件”，而是 Claude Code 的正式记忆机制。

### 适合写什么

- 项目架构
- 编码规范
- 命名规则
- 常用命令
- 测试方式
- 评审标准

### 不适合写什么

- API 密钥
- 长篇重复文档
- 纯个人偏好但要提交到仓库的内容

---

## 3. `settings.json` 管的是行为和权限，不是项目说明

官方 `settings` 文档里把它定义为配置系统。

它适合控制：

- 权限
- 环境变量
- 工具行为
- 用户设置、项目设置、组织设置的层级覆盖

例如官方明确提到，可以在 `.claude/settings.json` 中通过 `permissions.deny` 禁止读取：

- `.env`
- `.env.*`
- `secrets/**`
- 凭据文件

所以：

- `CLAUDE.md` = 告诉 Claude 怎么理解和工作
- `.claude/settings.json` = 告诉 Claude 能做什么、不能做什么

---

## 4. Skills 是按需加载的专用上下文

官方 `skills` 文档说明：

- Skills 用 `SKILL.md` 作为入口
- Claude 可以自动发现 Skills
- 也可以直接用 `/skill-name` 调用
- Skills 可以包含支持文件、脚本、模板、引用资料

和 `CLAUDE.md` 的区别是：

- `CLAUDE.md` 更像“项目通用规则”
- Skill 更像“某一类任务的专用操作手册”

## 一个简单类比

- `CLAUDE.md`：项目总说明
- `SKILL.md`：某个岗位或流程的 SOP

---

## 5. MCP 提供外部工具和数据源

官方文档中，MCP 被定义为连接外部数据源和工具的开放协议。

它解决的是：

- Claude 怎么接 Slack
- 怎么接 Jira
- 怎么接 Google Drive
- 怎么接你自定义的内部工具

所以它和 `CLAUDE.md`、Skills 的关系是：

- `CLAUDE.md` 提供规则
- Skill 提供专用流程
- MCP 提供外部能力入口

---

## 6. 官方给出的上下文层次，可以这样理解

你可以把 Claude Code 的上下文大致拆成 4 层：

### 第 1 层：会话上下文

- 当前对话
- 当前任务
- 当前工作目录

### 第 2 层：项目上下文

- `CLAUDE.md`
- 仓库文件
- 项目结构

### 第 3 层：专用能力上下文

- Skills
- 子代理
- 自定义命令

### 第 4 层：系统与权限上下文

- `.claude/settings.json`
- 企业策略
- 用户级配置
- MCP 配置

---

## 7. 在这个 starter 项目里应该怎么落地

推荐做法：

### 项目级

- `CLAUDE.md`：只保留 Claude Code 真正需要的项目级说明
- `AGENTS.md`：保留完整协作协议

### Skill 级

- `SKILL.md`：只写这个 Skill 的触发和流程
- `CHANGELOG.md / ROADMAP.md / TASKS.md / DECISIONS.md`：沉淀长期上下文

### 配置级

- `.claude/settings.json`：权限、敏感文件屏蔽、工具配置

---

## 8. 官方资料里最关键的几条

### 来自 `memory` 文档

- `CLAUDE.md` 会在会话开始时加载
- 项目级与用户级都有作用域
- 子目录可以按需加载

### 来自 `settings` 文档

- `CLAUDE.md` 属于 memory files
- `settings.json` 属于配置层
- 可以用 `permissions.deny` 屏蔽敏感文件

### 来自 `skills` 文档

- Skill 是可发现、可直接调用的专用能力包
- `SKILL.md` 是入口
- 支持附加文件、动态上下文、子代理执行

---

## 9. 新手最容易犯的错误

### 错误 1：把所有东西都塞进 `CLAUDE.md`

这样会让项目记忆膨胀，也不利于维护。

### 错误 2：把配置规则和协作规则混在一起

`settings.json` 和 `CLAUDE.md` 职责不同，不要混写。

### 错误 3：没有把长期上下文沉淀到文件

只靠聊天记录，下一次会话就会断掉。

### 错误 4：敏感信息直接交给 Claude 读

应优先通过设置限制读取，而不是事后补救。

---

## 10. 推荐阅读顺序

1. [什么是 AGENTS.md 和 CLAUDE.md？](../03-AI协作与上下文/02-什么是-AGENTS和-CLAUDE.md)
2. [CLAUDE.md 配置最佳实践](./07-CLAUDE-md-配置最佳实践.md)
3. [Claude 官方 Skill 资料导航](./08-Claude-官方-Skill-资料导航.md)

---

## 一句话总结

Claude Code 的上下文不是单一文件，而是一套机制：`CLAUDE.md` 管项目记忆，`settings.json` 管行为和权限，Skills 管任务专用能力，MCP 管外部工具接入。
