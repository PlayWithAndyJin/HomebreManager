# HBM — Homebrew Manager 🍺

<p align="center">
  <a href="README.en.md">English</a>&nbsp;&nbsp;·&nbsp;&nbsp;<a href="README.md">中文版</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AI_Generated-8A2BE2?style=flat-square" alt="AI Generated"/>&nbsp;&nbsp;&nbsp;&nbsp;
  <img src="https://img.shields.io/badge/Idea-AndyJin-f59e0b?style=flat-square" alt="Idea: AndyJin"/>
</p>

**HBM** 是一款基于 [Wails](https://wails.io) 构建的 Homebrew 可视化管理工具，覆盖 Homebrew 命令行全部核心功能，并提供镜像源管理、一键安装/卸载等增强体验。

## 特性

| 功能 | 说明 |
|------|------|
| 📊 **仪表盘** | 系统概览、包统计、快捷操作（brew doctor / update / cleanup） |
| 📦 **包管理** | 浏览已安装的 Formulae 和 Casks，过滤、查看详情、卸载、升级 |
| 🔍 **搜索** | 搜索 Homebrew 全部包，一键安装 |
| 🔌 **Tap 管理** | 添加/移除 Homebrew Taps |
| ⚙️ **服务管理** | 启动/停止/重启 brew services |
| 🛠️ **工具** | brew doctor、update、cleanup、upgrade 全部 |
| 🪞 **镜像源管理** | 一键切换官方/中科大/清华/阿里云镜像源，检测当前配置状态 |
| 🚀 **安装向导** | 未检测到 brew 时自动引导一键安装（支持官方/中科大/清华源） |
| 📟 **实时控制台** | 所有操作实时流式输出 |

## 截图

<table>
  <tr>
    <td><img src="Samples/Dashboard.png" alt="仪表盘" width="400"/></td>
    <td><img src="Samples/Packages.png" alt="包管理" width="400"/></td>
  </tr>
  <tr>
    <td align="center">📊 仪表盘</td>
    <td align="center">📦 包管理</td>
  </tr>
  <tr>
    <td><img src="Samples/Search.png" alt="搜索" width="400"/></td>
    <td><img src="Samples/Mirrors.png" alt="镜像源" width="400"/></td>
  </tr>
  <tr>
    <td align="center">🔍 搜索</td>
    <td align="center">🪞 镜像源管理</td>
  </tr>
  <tr>
    <td><img src="Samples/Tap.png" alt="Tap管理" width="400"/></td>
    <td><img src="Samples/Services.png" alt="服务管理" width="400"/></td>
  </tr>
  <tr>
    <td align="center">🔌 Tap 管理</td>
    <td align="center">⚙️ 服务管理</td>
  </tr>
  <tr>
    <td><img src="Samples/Tools.png" alt="工具" width="400"/></td>
    <td></td>
  </tr>
  <tr>
    <td align="center">🛠️ 工具</td>
    <td></td>
  </tr>
</table>



## 快速开始

### 前置要求

- macOS (Apple Silicon / Intel) 或 Linux
- Go 1.23+
- Node.js 18+

### 开发模式

```bash
# 克隆项目
git clone <repo-url> && cd BrewManager

# 开发运行（自动热重载）
wails dev
```

### 生产构建

```bash
# 构建为 .app 应用
wails build

# 运行
open build/bin/HBM.app
```

## 项目结构

```
BrewManager/
├── main.go                 # Wails 应用入口
├── app.go                  # Go ↔ JS 绑定层
├── wails.json              # Wails 构建配置
├── backend/
│   ├── models/types.go     # 共享数据类型
│   └── brew/
│       ├── executor.go     # brew 命令执行器（缓存 + 流式输出）
│       ├── packages.go     # 包管理（list/search/info/install/uninstall/upgrade）
│       ├── taps.go         # Tap 管理
│       ├── services.go     # 服务管理
│       ├── system.go       # 系统工具（doctor/cleanup/update/stats/install/uninstall）
│       └── mirrors.go      # 镜像源管理
└── frontend/
    └── src/
        ├── main.ts         # Vue 入口
        ├── App.vue         # 主布局
        ├── style.css       # 全局样式（暗色主题）
        ├── router/         # 路由配置
        ├── stores/         # Pinia 状态管理
        ├── types/          # TypeScript 类型
        ├── components/     # 通用组件
        │   ├── Sidebar.vue
        │   ├── Console.vue
        │   ├── StatsCard.vue
        │   ├── PackageDetail.vue
        │   └── ConfirmDialog.vue
        └── views/          # 页面
            ├── Dashboard.vue
            ├── Packages.vue
            ├── Search.vue
            ├── Taps.vue
            ├── Services.vue
            ├── Tools.vue
            └── Mirrors.vue
```

## 技术栈

| 层 | 技术 |
|----|------|
| **桌面框架** | [Wails v2](https://wails.io) |
| **后端** | Go 1.23 |
| **前端** | Vue 3 + TypeScript |
| **构建** | Vite |
| **状态管理** | Pinia |
| **路由** | Vue Router 4 |
| **图标** | FontAwesome 7 (Free) |
| **样式** | CSS Variables (暗色主题) |

## 镜像源支持

HBM 支持一键切换以下镜像源，解决国内 Homebrew 下载慢的问题：

| 镜像源 | Brew 本体 | API 源 | Bottles |
|--------|-----------|--------|---------|
| 官方 (GitHub) | `github.com/Homebrew/brew.git` | `formulae.brew.sh` | GitHub |
| 中科大 USTC | `mirrors.ustc.edu.cn/brew.git` | `mirrors.ustc.edu.cn/.../api` | `mirrors.ustc.edu.cn/.../bottles` |
| 清华 TUNA | `mirrors.tuna.tsinghua.edu.cn/.../brew.git` | `mirrors.tuna.tsinghua.edu.cn/.../api` | `mirrors.tuna.tsinghua.edu.cn/.../bottles` |
| 阿里云 | `mirrors.aliyun.com/homebrew/brew.git` | `mirrors.aliyun.com/.../api` | `mirrors.aliyun.com/.../bottles` |

## 构建说明

```bash
# 安装 Wails CLI
go install github.com/wailsapp/wails/v2/cmd/wails@latest

# 开发模式（热重载）
wails dev

# 生产构建
wails build

# 仅构建前端（快速调试）
cd frontend && npm run build
```

## 注意事项

- **Homebrew 5.0+**: Core/Cask 已内置为 JSON API，无需独立配置镜像
- **Dock 图标**: 首次打开 Finder 图标可能需刷新（`killall Finder`）
- **环境变量**: 镜像源的 API 和 Bottles 配置需写入 `~/.zshrc` 持久化

## License

MIT
