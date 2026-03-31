# Changelog

本文件记录本仓库对外可见的变更。

## Unreleased

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

### Changed

- 修正 `README.md`、教程文档和模板文档中的目录结构、复制路径和相对链接
- 统一 `find-skill` 相关说明，明确本仓库提供的是引导文档，实际搜索可使用 Skills CLI 或先安装独立 `find-skills` 项目
- 明确 `.env.example` 是环境变量模板，和 `assets/` 中的配置模板分开维护
- 将单个 Skill 内的协作文档改为根目录扁平组织，参照 `legal-skills` 项目结构
- 扩充术语表，补充 Git / GitHub / 协作相关术语
- 更新 Claude 官方参考链接，统一到当前官方文档 / 博客地址，并重写 `CLAUDE.md` 最佳实践页
- 将 `04-参考资料/` 中未编号或全局累加编号的文件重命名为一致的本地顺序，并同步修正内部链接
- 调整 `GitHub 入门` 与 `Vibe Coding` 等入口文档的学习路径，强调 Git 提交流程与上下文工程，而不展开 GitHub Actions
- 重新编排学习目录：`02-工具指南/` 聚焦 Git / GitHub / SSH / commit，`03-AI协作与上下文/` 承接 Vibe Coding 与上下文工程，原 `03-创建Skill/`、`04-参考资料/` 顺延为 `04`、`05`
