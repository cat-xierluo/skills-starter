---
name: skill-template
description: "Skill 模板 - 用于快速创建新的 Skill"
metadata:
  openclaw:
    emoji: "📦"
    requires: []
    triggers: []
---

# Skill 模板

> 这是一个最小可用的 Skill 模板，用于快速开始新的 Skill 开发。

## 简介

在这里描述你的 Skill 是做什么的。

## 使用场景

- 场景1：xxx
- 场景2：xxx
- 场景3：xxx

## 前置要求

### 系统依赖

| 依赖 | 安装方式 |
|------|----------|
| xxx | `brew install xxx` |

### Python 包

| 包名 | 用途 | 安装命令 |
|------|------|----------|
| xxx | 用途说明 | `pip install xxx` |

## 快速开始

1. 安装依赖
2. 配置环境变量（如果需要）
3. 运行测试

## 目录结构

```
skill-template/
├── SKILL.md           # 本文件
├── references/        # 参考文档
│   └── README.md
├── scripts/          # 自动化脚本
│   └── main.py
└── assets/          # 静态资源
    └── requirements.txt
```

## 开发指南

### 添加新功能

1. 在 `scripts/` 目录下创建脚本
2. 在 `SKILL.md` 中添加使用说明
3. 更新 `references/` 中的相关文档

### 测试

```bash
# 运行测试
python scripts/main.py --test
```

## 相关链接

- [OpenClaw 官方文档](https://docs.openclaw.ai)
- [ClawHub](https://clawhub.com)
- [Skill Creator 官方指南](https://github.com/anthropics/claude-code/tree/main/plugins/plugin-dev)

---

**基于 Skill 模板创建 | 版本: 1.0.0**
