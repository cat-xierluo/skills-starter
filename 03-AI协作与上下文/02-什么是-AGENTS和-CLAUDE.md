# 什么是 AGENTS.md 和 CLAUDE.md？

在 AI Coding 项目里，很多人会看到这些文件：

- `AGENTS.md`
- `CLAUDE.md`
- `.claude/settings.json`

它们都和“上下文”有关，但职责不一样。

## 先理解一句话

这些文件本质上是在回答：

**AI 进入这个项目后，应该知道什么、遵守什么、怎么工作。**

## `CLAUDE.md` 是什么

`CLAUDE.md` 是 Claude Code 官方支持的“项目记忆文件”。

根据 Claude Code 官方文档：

- `./CLAUDE.md` 或 `./.claude/CLAUDE.md` 可以作为项目级说明
- Claude 会在会话开始时自动读取这些说明
- 它适合写项目规则、常用命令、架构约定、命名习惯、工作流说明

你可以把它理解成：

> 给 Claude Code 的项目级入职说明。

### 适合写什么

- 怎么启动项目
- 怎么跑测试
- 代码风格
- 哪些目录重要
- 常见工作流
- 项目内必须遵守的规则

### 不适合写什么

- 临时性的个人偏好
- 密钥
- 大段重复文档

## `AGENTS.md` 是什么

`AGENTS.md` 不是 Claude Code 的唯一官方保留文件名，但在很多 AI Coding 项目里，它会被当作：

> 面向 AI 代理的协作协议文件。

在这个 starter 仓库里，`AGENTS.md` 的职责是：

- 规定文档怎么写
- 规定目录怎么命名
- 规定 Git 工作流
- 规定哪些文档必须同步更新

也就是说，它更偏：

- 仓库协作规则
- 代理行为规范
- 团队约定

### 你可以把它理解成

- `CLAUDE.md`：Claude Code 自动加载的项目记忆
- `AGENTS.md`：团队写给 AI 代理看的协作章程

## 它们有什么区别

| 文件 | 主要角色 | 更像什么 | 是否官方自动加载 |
|------|----------|----------|------------------|
| `CLAUDE.md` | Claude Code 项目记忆 | 项目说明书 | 是 |
| `AGENTS.md` | 代理协作协议 | 团队规则手册 | 不一定，取决于工具 |

## 在这个项目里为什么两个都有

看当前仓库的 [CLAUDE.md](../CLAUDE.md)，你会发现它几乎只是：

```md
@include ./AGENTS.md
```

这说明本项目采用的是：

1. 把主要协作规则写在 `AGENTS.md`
2. 再通过 `CLAUDE.md` 把这些规则喂给 Claude Code

这样做的好处是：

- 规则只有一份，不容易写两套
- 既能给人看，也能给 Claude 读
- 项目上下文更集中

## 还有哪些“上下文文件”

### `.claude/settings.json`

这是配置文件，不是说明文档。

它主要控制：

- 权限
- 工具行为
- 环境变量
- 本地或团队设置

例如官方文档里提到，可以用它禁止 Claude 读取 `.env` 等敏感文件。

### `SKILL.md`

这是 Skill 本身的定义文件。

它解决的是：

> 某个 Skill 什么时候触发、怎么工作、依赖什么资源。

### `CHANGELOG.md` / `ROADMAP.md` / `TASKS.md` / `DECISIONS.md`

这些不是 Claude 的底层配置文件，但会成为非常重要的项目上下文来源。

它们回答的是：

- 改过什么
- 计划做什么
- 当前要做什么
- 为什么这样做

## 新手最实用的理解方式

如果把一个 AI Coding 项目想成“让 AI 入职一个团队”，那么：

- `CLAUDE.md` = 入职须知
- `AGENTS.md` = 团队规章制度
- `.claude/settings.json` = 系统设置与权限
- `SKILL.md` = 某个岗位/能力包的说明书
- `TASKS.md` / `DECISIONS.md` = 项目进展与决策记录

## 推荐实践

### 对单个项目

至少保留：

- `CLAUDE.md`
- `AGENTS.md` 或等价协作协议
- `CHANGELOG.md`
- `TASKS.md`
- `DECISIONS.md`

### 对复杂团队项目

建议：

- `CLAUDE.md` 只放 Claude 真的需要的项目说明
- `AGENTS.md` 放完整协作协议
- 长文档不要全塞进 `CLAUDE.md`
- 敏感信息不要写进任何会被提交的记忆文件

## 继续阅读

- [上下文工程入门](./03-上下文工程入门.md)
- [Rules 编写指南](./04-Rules-编写指南.md)
- [CLAUDE.md 配置最佳实践](../05-参考资料/07-CLAUDE-md-配置最佳实践.md)
- [Claude 官方 Skill 资料导航](../05-参考资料/08-Claude-官方-Skill-资料导航.md)
- [Claude Code 上下文与记忆机制](../05-参考资料/09-Claude-Code-上下文与记忆.md)

## 一句话总结

`CLAUDE.md` 是 Claude Code 的官方项目记忆入口，`AGENTS.md` 是团队给 AI 代理的协作规则。两者配合得好，项目上下文才会稳定。
