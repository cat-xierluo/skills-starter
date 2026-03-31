# CLAUDE.md 配置最佳实践

> 本文基于 Claude Code 官方 `memory` 与 `settings` 文档整理，重点是把 `CLAUDE.md` 放回它真正的职责里：项目记忆，而不是“万能配置文件”。
> 最后核对时间：2026-03-30

---

## 1. 先搞清楚：`CLAUDE.md` 不是“技能注册表”

官方语境里，`CLAUDE.md` 属于 memory files。

它的职责是：

- 告诉 Claude 这个项目是什么
- 告诉 Claude 需要遵守哪些长期规则
- 提供常用命令、目录约定、验证方式
- 为当前仓库补充稳定上下文

它不适合承担的事情：

- 存密钥
- 写超长教程
- 充当技能市场目录
- 把所有团队文档原样塞进去

---

## 2. `CLAUDE.md`、`AGENTS.md`、`settings.json` 要分工

推荐这样理解：

| 文件 | 主要职责 | 更像什么 |
|------|----------|----------|
| `CLAUDE.md` | Claude Code 的项目记忆 | 项目级入职说明 |
| `AGENTS.md` | 团队写给代理的协作协议 | 协作章程 |
| `.claude/settings.json` | 权限、行为与工具配置 | 系统设置 |

在本项目里采用的是：

- 把完整协作规则写进 `AGENTS.md`
- 用根目录 `CLAUDE.md` 通过 `@include ./AGENTS.md` 引入

这样既保留了面向人类的协作文档，也兼容 Claude Code 的官方记忆机制。

---

## 3. 官方推荐写进 `CLAUDE.md` 的内容

更适合保留在 `CLAUDE.md` 里的信息：

- 项目目标和核心边界
- 关键目录说明
- 常用开发命令
- 测试和验证方式
- 代码风格或评审标准
- 敏感约束和不可越界规则

一个简单原则：

> 如果下一次会话一开始就应该知道它，那它可能适合写进 `CLAUDE.md`。

---

## 4. 不建议写进 `CLAUDE.md` 的内容

以下内容更适合拆到别处：

- 长篇背景知识：放 `references/`
- 某个任务专用流程：放 `SKILL.md`
- 临时任务安排：放 `TASKS.md`
- 决策原因和工作日志：放 `DECISIONS.md`
- 发布记录：放 `CHANGELOG.md`
- 权限和 deny 规则：放 `.claude/settings.json`

这样做的好处是上下文更稳，也更容易维护。

---

## 5. 推荐的最小结构

对多数项目，`CLAUDE.md` 不需要很长。一个够用的版本通常包含：

```md
# Project Memory

## 项目目标
- 这个仓库解决什么问题

## 关键目录
- `src/`
- `docs/`
- `tests/`

## 常用命令
- `pnpm test`
- `pnpm lint`

## 工作规则
- 先读后改
- 改完要验证
- 不提交密钥

## 参考文档
- `AGENTS.md`
- `docs/ARCHITECTURE.md`
- `status/TASKS.md`
```

如果你已经把规则沉淀在 `AGENTS.md`，那可以像当前仓库一样保持更简洁：

```md
@include ./AGENTS.md
```

---

## 6. `.claude/settings.json` 负责什么

很多人会把 `CLAUDE.md` 和 `settings.json` 混在一起，这是常见误区。

更准确的分工是：

- `CLAUDE.md`：给 Claude 读的长期项目说明
- `settings.json`：给 Claude Code 的行为与权限配置

`settings.json` 更适合处理：

- `permissions.deny`
- 环境变量
- 工具行为
- 项目级或用户级配置覆盖

如果你的重点是“不要读 `.env`”或“限制某些目录访问”，应该去改 `settings.json`，而不是往 `CLAUDE.md` 里堆规则。

---

## 7. 多层级记忆怎么理解

根据官方 memory 文档，可以把它理解成：

- 用户级 `~/.claude/CLAUDE.md`：个人长期偏好
- 项目级 `./CLAUDE.md` 或 `./.claude/CLAUDE.md`：仓库规则
- 更高层目录的 `CLAUDE.md`：上层约束
- 子目录中的 `CLAUDE.md`：进入子目录任务时按需加载

所以更好的写法不是“把所有东西都写在一个文件里”，而是按作用域拆开。

---

## 8. 新手最容易踩的坑

### 坑 1：把 `CLAUDE.md` 写成百科全书

结果是上下文冗长，真正关键的规则反而被淹没。

### 坑 2：把 Skill 说明塞进 `CLAUDE.md`

Skill 的触发逻辑和任务流程应保留在 `SKILL.md`。

### 坑 3：把权限配置写成自然语言规则

能用 `settings.json` 约束的，就不要只靠提示词约束。

### 坑 4：没有给下一位协作者留文档上下文

`CLAUDE.md` 解决的是“项目记忆”，不是“任务接力”。后者还需要：

- `CHANGELOG.md`
- `ROADMAP.md`
- `TASKS.md`
- `DECISIONS.md`

---

## 9. 在这个 starter 项目里的落地建议

推荐分工如下：

- `CLAUDE.md`：入口级项目记忆
- `AGENTS.md`：完整协作协议
- `SKILL.md`：具体 Skill 的触发与流程
- `CHANGELOG.md`：对外可见变更
- `ROADMAP.md`：中长期计划
- `TASKS.md`：当前任务状态
- `DECISIONS.md`：技术决策与工作日志

---

## 10. 推荐继续阅读

1. [什么是 AGENTS.md 和 CLAUDE.md？](../03-AI协作与上下文/02-什么是-AGENTS和-CLAUDE.md)
2. [Claude Code 上下文与记忆](./09-Claude-Code-上下文与记忆.md)
3. [Claude 官方 Skill 资料导航](./08-Claude-官方-Skill-资料导航.md)
4. [Claude Skill 最佳实践清单](./10-Claude-Skill-最佳实践清单.md)

---

## 一句话总结

`CLAUDE.md` 应该是精炼、稳定、长期有效的项目记忆文件；协作规则、权限配置、任务状态和 Skill 专用流程，都应该拆到各自更合适的位置。
