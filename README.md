# 智能镜像同步工具（GitHub Actions → 华为云 SWR）

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-自动同步-blue)](https://github.com/features/actions)
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

使用 GitHub Actions 将 `images.txt` 中的容器镜像自动同步到华为云容器镜像服务（SWR）。  
**智能判断**：仅在源镜像有**实质性内容更新**（包括 `latest` 这类 Tag 指向新版本）时才执行拉取和推送，否则自动跳过，节约时间与流量。

---

## ✨ 核心特性

| 功能 | 说明 |
| :--- | :--- |
| 🕒 **定时同步** | 每 3 天自动运行一次（北京时间上午 8:00），捕捉可变 Tag（如 `latest`）的内容更新 |
| 🔄 **变更触发** | 修改 `images.txt` 并推送到仓库后自动触发，实时同步新增或版本变更 |
| 🎯 **手动触发** | 支持在 GitHub Actions 页面一键运行，方便测试或紧急同步 |
| 🧠 **智能跳过** | 通过对比镜像摘要（Digest），内容未变时完全跳过拉取和推送，零冗余操作 |
| 🧩 **规范命名** | 自动将源镜像路径中的 `/` 替换为 `.`（如 `library/nginx` → `library.nginx`），既保留来源信息，又彻底杜绝命名冲突 |
| 🔐 **安全可靠** | 所有敏感凭证（登录指令、仓库地址）通过 GitHub Secrets 加密存储，绝不硬编码 |

---

## 📂 仓库目录结构

```bash
your-repo/
├── .github/
│   └── workflows/
│       └── sync-images.yml       # 工作流主文件
├── images.txt                     # 镜像列表（核心配置）
└── README.md                      # 本文档
