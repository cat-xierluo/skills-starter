# Changelog

本文件记录本仓库对外可见的变更。
即使当前还没有正式对外发布，也按内部迭代版本记录，例如 `0.1.0`、`0.2.0`，而不是只维护一个 `Unreleased` 段落。

## 0.7.0 - 2026-03-31

### Changed

- 将 `SKILL-DEV-GUIDE.md` 与 `SKILL-ORCHESTRATION-GUIDE.md` 统一移入 `04-创建Skill/`，作为创建与规范文档的一部分
- 将 `.claude/skills` 调整为指向根目录 `skills/` 的符号链接，对齐 `legal-skills` 的单一来源结构
- 更新 README、AGENTS、创建流程、参考资料和模板中的路径说明，移除 `find-skill` 双副本叙事

## 0.6.0 - 2026-03-31

### Added

- 为许可证文档补充常见许可证对比表

### Changed

- 增补派生版本 / 衍生作品相关说明，明确 `SA`、`GPL`、`AGPL`、`ND`、`NC` 等条款在 Skill 场景下的区别
- 将许可证说明进一步对齐到“开源方式、商用边界、署名义务和后续授权策略”的决策维度

## 0.5.0 - 2026-03-31

### Changed

- 撤回对 `SKILL-DEV-GUIDE.md` 的本地改动，避免与后续从 `legal-skills` 同步的内容发生漂移
- 在 `AGENTS.md` 中新增上游同步文件约定，明确根目录 `SKILL-*-GUIDE.md` 默认不手动修改

## 0.4.0 - 2026-03-31

### Changed

- 重写许可证说明结构，不再主要按 Skill 类型分类，而改为围绕商用边界、署名义务、同协议共享和后续商业授权空间来解释
- 更新 `AGENTS.md`、`SKILL-DEV-GUIDE.md`、许可证概念文档和参考资料，使许可证选择逻辑更通用、更适合 starter

## 0.3.0 - 2026-03-31

### Added

- 参照 `legal-skills` 抽取并补充许可证管理规范，覆盖 `AGENTS.md`、开发指南与参考资料

### Changed

- 更新许可证概念文档，增加按 Skill 类型选择许可证的实战分类
- 更新许可证参考文档，补充 `legal-skills` 中值得继承的多 Skill 许可证展示与迁移规则
- 更新 `AGENTS.md` 与 `SKILL-DEV-GUIDE.md`，把许可证从“说明事项”提升为维护规范

## 0.2.0 - 2026-03-31

### Added

- 新增许可证基础说明文档：`01-概念入门/02-什么是-许可证.md`
- 新增许可证官方参考导航：`05-参考资料/12-许可证与开源授权参考.md`

### Changed

- 更新 `README.md` 资源导航和快速开始，明确 `LICENSE.txt` 也是创建 Skill 时应处理的关键文件
- 更新 `SKILL-DEV-GUIDE.md`、`04-创建Skill/03-基于模板创建.md` 和 `skills/skill-template/SKILL.md`，补充许可证选择、`license` 字段和 `LICENSE.txt` 的落地说明
- 更新 `04-创建Skill/02-搜索现成方案.md`，强调许可证不明确时不要直接复制第三方实现

## 0.1.0 - 2026-03-31

### Added

- 为 starter 仓库补充 `docs/`、`status/` 和 `CHANGELOG.md` 协作文档体系
- 为 `skills/skill-template/` 增加协作文档模板、配置模板和更实用的脚手架脚本
- 新增完整示例 Skill：`skills/weekly-weather-briefing/`
- 补强 `Vibe Coding`、`Git`、`GitHub`、`SSH` 基础教程，加入首次上手流程与常见问题说明
- 新增 Claude 官方 Skills 资料导航、上下文 / memory / settings 说明和 `AGENTS.md` / `CLAUDE.md` 入门文档
- 新增一份基于官方文档、博客和 PDF 的 Claude Skill 最佳实践清单
- 统一 `04-参考资料/` 的文件编号和命名规则，改为目录内独立从 `01` 开始排序
- 新增“提交到 GitHub 与 Commit 规范”“上下文工程入门”“Rules 编写指南”三篇基础工具教程
- 新增 `03-AI协作与上下文/` 目录，将 Vibe Coding、`AGENTS.md`、`CLAUDE.md`、上下文工程和 Rules 单独成组
- 新增项目内置 `.claude/skills/find-skill/`，让 `find-skill` 在仓库内开箱即用
- 新增 AI 需求分流与目录检索协议，明确 `AGENTS.md` 中的默认工作流和 project-local Skill 使用规则
- 新增 changelog 版本化约定，即使未正式发布也按 `0.x.0` 迭代记录

### Changed

- 调整 `README.md`，明确“先描述需求 -> 先检索现成 Skill -> 能复用不重造 -> 否则进入创建流程”的默认使用路径
- 修正 `README.md`、教程文档和模板文档中的目录结构、复制路径和相对链接
- 统一 `find-skill` 相关说明，明确本仓库提供的是引导文档，实际搜索可使用 Skills CLI 或先安装独立 `find-skills` 项目
- 明确 `.env.example` 是环境变量模板，和 `assets/` 中的配置模板分开维护
- 将单个 Skill 内的协作文档改为根目录扁平组织，参照 `legal-skills` 项目结构
- 扩充术语表，补充 Git / GitHub / 协作相关术语
- 更新 Claude 官方参考链接，统一到当前官方文档 / 博客地址，并重写 `CLAUDE.md` 最佳实践页
- 将 `04-参考资料/` 中未编号或全局累加编号的文件重命名为一致的本地顺序，并同步修正内部链接
- 调整 `GitHub 入门` 与 `Vibe Coding` 等入口文档的学习路径，强调 Git 提交流程与上下文工程，而不展开 GitHub Actions
- 重新编排学习目录：`02-工具指南/` 聚焦 Git / GitHub / SSH / commit，`03-AI协作与上下文/` 承接 Vibe Coding 与上下文工程，原 `03-创建Skill/`、`04-参考资料/` 顺延为 `04`、`05`
- 调整 `.gitignore`，不再整体忽略 `.claude/`，改为只忽略本地配置与仓库元数据
