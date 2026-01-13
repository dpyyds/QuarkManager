# QuarkManager 夸克管家

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows-blue?style=flat-square" alt="Platform">
  <img src="https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat-square&logo=go" alt="Go">
  <img src="https://img.shields.io/badge/Vue-3.x-4FC08D?style=flat-square&logo=vue.js" alt="Vue">
  <img src="https://img.shields.io/badge/Wails-2.x-red?style=flat-square" alt="Wails">
  <img src="https://img.shields.io/github/license/dpyyds/QuarkManager?style=flat-square" alt="License">
</p>

<p align="center">
  <b>🚀 一款现代化的夸克网盘第三方桌面客户端</b>
</p>

<p align="center">
  基于 Wails + Vue3 + Element Plus 打造，提供简洁优雅的用户界面和强大的功能
</p>

## ⚠️ 免责声明

- 本软件为**第三方开发工具**，与夸克网盘官方无任何关联
- **仅供个人学习、研究和技术交流使用**，请勿用于任何商业用途
- 使用本软件可能存在账号被封禁等风险，由此产生的一切后果由用户自行承担
- 如本软件侵犯了您的权益，请联系开发者，我们将及时处理
- 请遵守当地法律法规，不得利用本软件从事任何违法活动

## ✨ 功能特性

### 📁 文件管理
- 文件/文件夹浏览、搜索
- 新建文件夹
- 文件重命名、删除、移动
- 文件上传（支持原生文件选择对话框）
- 获取文件下载链接

### 🔗 分享功能
- 创建分享链接（支持文件和文件夹）
- 自定义分享密码
- 设置分享有效期（1天/7天/30天/永久）
- 查看我的分享列表
- 取消分享

### 💾 转存功能
- 转存他人分享链接
- 支持带密码的分享链接
- 自动解析分享链接
- 选择转存目标文件夹

### 👥 多账户管理
- 支持多账户登录
- 账户快速切换
- 账户过期检测
- Cookie 自动保存与恢复

### 🌐 API 服务
- 内置 HTTP API 服务（端口 8080）
- Swagger API 文档
- 支持外部程序调用
- API 服务开关控制

### 📧 邮件通知
- Cookie 过期邮件提醒
- 自定义 SMTP 配置
- 支持 SSL/TLS 加密

## 🖼️ 界面预览

软件采用现代化 UI 设计，简洁优雅的浅色主题：

- 顶部导航栏：快速切换各功能模块
- 文件管理：类似文件管理器的操作体验
- 分享管理：一键创建和管理分享
- 设置中心：账户、API、邮件等配置

## 🚀 快速开始

### 下载安装

从 [Releases](https://github.com/dpyyds/QuarkManager/releases) 页面下载最新版本的 `quarkpan.exe`，双击运行即可。

### 登录账号

1. 启动软件后，点击右上角「登录」按钮
2. 使用夸克 APP 扫描二维码
3. 扫码成功后自动登录

### 基本使用

1. **浏览文件**：在「文件」页面浏览网盘文件
2. **上传文件**：点击上传按钮选择本地文件
3. **创建分享**：选中文件后点击分享按钮
4. **转存文件**：在「转存」页面粘贴分享链接

## 🔧 进阶玩法

### 1. API 服务调用

开启 API 服务后，可通过 HTTP 接口操作网盘：

```bash
# 获取文件列表
curl http://localhost:8080/api/files?folder_id=0

# 创建分享
curl -X POST http://localhost:8080/api/share \
  -H "Content-Type: application/json" \
  -d '{"file_ids": ["xxx"], "title": "分享标题"}'

# 转存分享
curl -X POST http://localhost:8080/api/save \
  -H "Content-Type: application/json" \
  -d '{"share_url": "https://pan.quark.cn/s/xxx"}'
```

访问 `http://localhost:8080/swagger/` 查看完整 API 文档。

### 2. 多账户管理

在「设置」→「账户管理」中：

- **添加账户**：点击添加按钮扫码登录新账户
- **切换账户**：点击账户旁的「切换」按钮
- **删除账户**：点击「删除」移除不需要的账户
- **检查过期**：定期检查账户 Cookie 是否过期

### 3. 邮件通知配置

配置邮件通知，在 Cookie 即将过期时收到提醒：

1. 进入「设置」→「邮件通知」
2. 开启邮件通知开关
3. 填写 SMTP 服务器信息：
   - QQ 邮箱：`smtp.qq.com`，端口 `465`
   - 163 邮箱：`smtp.163.com`，端口 `465`
4. 填写发件人/收件人邮箱
5. 点击「发送测试邮件」验证配置

### 4. 批量操作

支持批量文件操作：

- **批量删除**：选中多个文件后删除
- **批量移动**：选中多个文件后移动到目标文件夹
- **批量分享**：选中多个文件创建分享
- **批量转存**：支持多个分享链接转存

## 🛠️ 开发构建

### 环境要求

- Go 1.21+
- Node.js 18+
- Wails CLI 2.x

### 安装 Wails

```bash
go install github.com/wailsapp/wails/v2/cmd/wails@latest
```

### 构建项目

```bash
cd quarkpan-wails

# 安装前端依赖
cd frontend && npm install && cd ..

# 开发模式
wails dev

# 构建发布版本（64位）
$env:GOARCH="amd64"; wails build
```

### 项目结构

```
quarkpan-wails/
├── frontend/              # Vue3 前端
│   ├── src/
│   │   ├── api/          # API 封装
│   │   ├── views/        # 页面组件
│   │   └── App.vue       # 主组件
│   └── package.json
├── internal/
│   ├── app/              # 应用主逻辑
│   └── quark/            # 夸克 API 封装
│       ├── auth.go       # 认证服务
│       ├── files.go      # 文件服务
│       ├── share.go      # 分享服务
│       ├── upload.go     # 上传服务
│       └── account.go    # 账户管理
├── main.go               # 入口文件
└── wails.json            # Wails 配置
```

## 📝 更新日志

### v1.0.0
- 🎉 首次发布
- ✅ 文件浏览、上传、下载
- ✅ 分享创建与管理
- ✅ 转存功能
- ✅ 多账户管理
- ✅ API 服务
- ✅ 邮件通知

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 开源协议

本项目采用 [MIT License](LICENSE) 开源协议。

## 👨‍💻 作者

**dpyyds**

- GitHub: [@dpyyds](https://github.com/dpyyds)
- 项目地址: [QuarkManager](https://github.com/dpyyds/QuarkManager)

---

<p align="center">
  如果这个项目对你有帮助，欢迎 ⭐ Star 支持一下！
</p>
