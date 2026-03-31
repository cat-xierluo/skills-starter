# Claude Skill 最佳实践清单

> 这份清单基于 Claude 官方 Skills 文档、Best Practices 页面、官方博客和官方 PDF 指南整理，适合在真正动手写 Skill 前快速过一遍。
> 最后核对时间：2026-03-30

---

## 1. 先判断值不值得写成 Skill

官方反复强调，不要为了“感觉以后也许会用到”就先写 Skill。

更适合写成 Skill 的场景：

- 你已经重复做过几次
- 之后还会继续做很多次
- 任务有稳定流程、检查标准或模板
- 需要把团队经验沉淀成可复用做法

如果只是一次性问题，往往直接提示 Claude 更划算。

---

## 2. `description` 比正文更重要

Claude 是否能正确触发一个 Skill，首先看的是 `description`。

官方建议：

- 写清楚“什么时候用”
- 写出真实用户会说的话
- 说明边界，不要什么都包
- 避免过于宽泛的描述

坏例子：

```yaml
description: Helps with documents.
```

好例子应该更像：

```yaml
description: |
  Create, edit, and review legal or policy documents.
  Use when the user asks to draft agreements, redline clauses,
  summarize contract terms, or compare two document versions.
```

---

## 3. `SKILL.md` 要短，小而能用

官方 best practices 和博客都强调一件事：

> `SKILL.md` 不应该变成一本手册。

推荐做法：

- `SKILL.md` 只保留触发条件、主流程、限制、关键例子
- 大块说明移到 `references/`
- 可执行逻辑移到 `scripts/`
- 最终输出模板或素材放到 `assets/`

这和本仓库的模板设计是一致的。

---

## 4. 把文件夹拆对，比把字写多更重要

官方推荐的基本心智模型：

- `SKILL.md`：入口和操作说明
- `references/`：按需加载的资料
- `scripts/`：确定性执行逻辑
- `assets/`：输出要用但不必进入上下文的文件

一个常见错误是把所有内容都塞进 `SKILL.md`。这样会让上下文膨胀，触发后也更难让 Claude 抓到重点。

---

## 5. 给 Claude “足够具体”的例子

官方博客和 skill-creator 经验都说明：

- 只给高层目标，Claude 容易泛化得太宽
- 写死全部细节，又会让 Skill 太脆

更稳妥的方式是：

- 给 1 到 3 个代表性例子
- 给清晰的输入 / 输出预期
- 给“什么算完成”的标准
- 给关键限制和错误处理方式

---

## 6. 先做单一职责，再考虑组合

Skill 可组合，但不代表一个 Skill 应该什么都做。

更好的拆法是：

- 一个 Skill 聚焦一类任务
- 多步复杂工作流由多个 Skill 配合
- 共同规则写进项目级 `CLAUDE.md` 或 `AGENTS.md`

如果一个 Skill 同时承担“搜资料、做分析、写报告、发邮件、建任务”，通常已经太重了。

---

## 7. 评估和回归不是可选项

2026-03-03 的官方文章已经把重点放到：

- 写 evals
- 跑 benchmark
- 观察触发准确率
- 比较“有 Skill”和“没 Skill”的差异

这意味着 Skill 维护应该像维护代码一样：

- 改完要验证
- 模型升级后要回归
- `description` 要根据误触发 / 漏触发持续调整

---

## 8. 注意安全边界

官方 API 文档和产品文档都提醒过：

- Skill 可能触发工具调用
- Skill 可能运行脚本或代码
- 恶意 Skill 可能越权读取或执行不该做的事

所以：

- 只安装可信来源
- 在 `.claude/settings.json` 里限制敏感文件访问
- 不把密钥写进 `CLAUDE.md`、`SKILL.md` 或参考文档
- 对外部 Skill 做来源审查

---

## 9. 团队 Skill 要可维护，不只是能运行

对团队项目，官方资料和实践都指向同一个方向：

- 版本变更要可追踪
- 重要决策要可追溯
- 下一位协作者要能快速接手

因此在这个 starter 里，推荐默认保留：

- `CHANGELOG.md`
- `ROADMAP.md`
- `TASKS.md`
- `DECISIONS.md`

---

## 10. 一个实用的发布前检查表

在你准备把 Skill 交给别人用之前，至少检查：

- `name` 是否唯一且稳定
- `description` 是否具体
- `SKILL.md` 是否过长
- `references/` 是否只保留必要资料
- `scripts/` 是否可运行
- 相对路径是否有效
- 是否有最小验证步骤
- 是否记录了限制、依赖和安全注意事项

---

## 11. 推荐阅读顺序

1. [什么是 Skill？](../01-概念入门/01-什么是-Skill.md)
2. [Claude 官方 Skill 资料导航](./08-Claude-官方-Skill-资料导航.md)
3. [Skill 编写官方指南](./03-Skill-官方编写指南.md)
4. [Claude Code 上下文与记忆](./09-Claude-Code-上下文与记忆.md)
5. [SKILL-DEV-GUIDE.md](../SKILL-DEV-GUIDE.md)

---

## 一句话总结

官方最佳实践的核心不是“把 Skill 写得很长”，而是把触发条件写准、把内容拆对、把验证补齐、把维护当成长期工作来做。
