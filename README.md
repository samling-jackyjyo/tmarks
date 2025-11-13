<div align="center">

# 🔖 TMarks

**AI 驱动的智能书签管理系统**

[![TypeScript](https://img.shields.io/badge/TypeScript-5.6-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18.3%20%7C%2019-61dafb.svg)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-6.0%20%7C%207-646cff.svg)](https://vitejs.dev/)
[![Cloudflare](https://img.shields.io/badge/Cloudflare-Workers-f38020.svg)](https://workers.cloudflare.com/)
[![许可证](https://img.shields.io/badge/许可证-MIT-green.svg)](LICENSE)

简体中文

[在线演示](https://tmarks.669696.xyz) | [问题反馈](https://github.com/ai-tmarks/tmakrs/issues)

</div>

---

## ✨ 项目简介

TMarks 是一个现代化的智能书签管理系统，结合 AI 技术自动生成标签，让书签管理变得简单高效。

### 核心特性

- 📚 **智能书签管理** - AI自动标签、多维筛选、批量操作、拖拽排序
- 🗂️ **标签页组管理** - 一键收纳标签页、智能分组、快速恢复
- 🌐 **公开分享** - 创建个性化书签展示页、KV缓存加速
- 🔌 **浏览器扩展** - 快速保存、AI推荐、离线支持、自动同步
- 🔐 **安全可靠** - JWT认证、API Key管理、数据加密

### 技术栈

- **前端**: React 18/19 + TypeScript + Vite + TailwindCSS 4
- **后端**: Cloudflare Workers + Pages Functions
- **数据库**: Cloudflare D1 (SQLite)
- **缓存**: Cloudflare KV
- **AI集成**: 支持 OpenAI、Anthropic、DeepSeek、智谱等8+提供商

---

## 🚀 快速开始

### 本地开发

```bash
# 1. 克隆项目
git clone https://github.com/ai-tmarks/tmakrs.git
cd tmarks

# 2. 安装依赖
cd tmarks
pnpm install

# 3. 创建数据库并迁移
wrangler d1 create tmarks-prod-db --local
pnpm db:migrate:local

# 4. 启动开发服务器
pnpm dev
# 访问 http://localhost:5173
```

### 浏览器扩展开发

```bash
# 1. 安装依赖
cd tab
pnpm install

# 2. 启动开发模式
pnpm dev

# 3. 加载扩展
# Chrome: chrome://extensions/ → 开发者模式 → 加载已解压的扩展程序 → 选择 tab/dist
# Firefox: about:debugging → 临时载入附加组件 → 选择 tab/dist/manifest.json
```

---

## 🚀 部署

### 快速部署

**前置要求:**
- Cloudflare 账号
- GitHub 账号

**部署步骤:**

1. **Fork 仓库**
   - Fork 本仓库到你的 GitHub

2. **创建资源并配置**
   
   **a. 在 Cloudflare Dashboard 创建资源：**
   - 创建D1数据库：`tmarks-prod-db`，记录 ID
   - 创建KV空间：`RATE_LIMIT_KV`，记录 ID
   - 创建KV空间：`PUBLIC_SHARE_KV`，记录 ID
   
   **b. 在你的 Fork 仓库中配置 wrangler.toml：**
   - 将 `tmarks/wrangler.toml.example` 重命名为 `tmarks/wrangler.toml`
   - 编辑文件，将上面记录的资源 ID 填入对应位置
   - 提交更改

3. **配置环境变量**
   
   继续在 Cloudflare Dashboard 操作：
   - Workers & Pages → 你的项目 → 设置 → 环境变量 → 生产环境
   - 添加以下变量（生成随机密钥）：
     - `JWT_SECRET`: 生成一个 48 位随机字符串
     - `ENCRYPTION_KEY`: 生成一个 48 位随机字符串

4. **初始化数据库**
   - Workers & Pages → D1 → 打开 `tmarks-prod-db`
   - 打开 `tmarks/migrations/d1_console_pure.sql` 文件
   - 复制 SQL 内容并在控制台执行

5. **连接仓库并部署**
   - Workers & Pages → 创建 → 连接到 Git → 选择你的仓库
   - 配置构建设置：
     - 根目录: `tmarks`
     - 构建命令: `pnpm install && pnpm build:deploy`
     - 构建输出目录: `.deploy`
   - 保存并部署，等待构建完成

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源协议。
