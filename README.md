# MelodyHub

基于 lx-music-desktop 核心逻辑的 Web 版本音乐服务，支持多平台音乐搜索、下载和管理，提供 Docker 一键部署方案。

## ✨ 特性

- 🎵 **多音源支持**: 兼容 lx-music-desktop 自定义源，支持网易云、QQ音乐、酷我、酷狗等平台
- 🌐 **Web 访问**: 浏览器即可使用，支持多设备访问
- 📥 **服务器端下载**: 支持断点续传、队列管理、多任务并行
- 🔄 **实时推送**: WebSocket 实时推送下载进度
- 🛡️ **防盗链代理**: 自动处理音乐平台防盗链
- 💾 **数据持久化**: SQLite 数据库存储
- 🎨 **现代化 UI**: Vue 3 + Element Plus 构建
- 🎯 **歌曲管理**: 内置歌曲管理器，支持元数据编辑
- 🔍 **智能搜索**: 多平台聚合搜索

## 🚀 快速开始

### 方式一: Docker Compose（推荐）

```yaml
version: '3.8'

services:
  melodyhub:
    image: geelonn/melodyhub:latest
    container_name: melodyhub
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - melodyhub-data:/app/data
      - melodyhub-files:/app/music
    environment:
      - NODE_ENV=production
      - PORT=3000
      - DATA_DIR=/app/data
      - MUSIC_DIR=/app/music
      - JWT_SECRET=your-secure-secret-key
      - TZ=Asia/Shanghai

volumes:
  melodyhub-data:
  melodyhub-files:
```

启动服务：
```bash
docker-compose up -d
# 访问 http://localhost:3000
```

### 方式二: 直接运行容器

```bash
docker run -d \
  --name melodyhub \
  --restart unless-stopped \
  -p 3000:3000 \
  -v melodyhub-data:/app/data \
  -v melodyhub-files:/app/music \
  -e NODE_ENV=production \
  -e PORT=3000 \
  -e DATA_DIR=/app/data \
  -e MUSIC_DIR=/app/music \
  -e JWT_SECRET=your-secure-secret-key \
  -e TZ=Asia/Shanghai \
  geelonn/melodyhub:latest
```

## 🔧 环境变量

| 变量名 | 描述 | 默认值 |
|--------|------|--------|
| `PORT` | 服务器端口 | `3000` |
| `DATA_DIR` | 数据存储目录 | `/app/data` |
| `MUSIC_DIR` | 音乐存储目录 | `/app/music` |
| `NODE_ENV` | 运行环境 | `production` |
| `JWT_SECRET` | 安全密钥（必须修改） | `your-secure-secret-key` |
| `MAX_CONCURRENT_DOWNLOADS` | 最大并发下载数 | `3` |
| `DOWNLOAD_RETRY_LIMIT` | 下载失败重试次数 | `3` |
| `HTTP_PROXY` | HTTP 代理（可选） | - |
| `HTTPS_PROXY` | HTTPS 代理（可选） | - |
| `TZ` | 时区设置 | `Asia/Shanghai` |

## 📁 数据持久化

建议使用 Docker 卷或本地目录挂载来持久化数据：
- `/app/data`: 存储数据库和配置
- `/app/music`: 存储下载的音乐文件

## 🎯 使用指南

1. **访问 Web 界面**: 打开浏览器访问 `http://localhost:3000`
2. **上传自定义源**: 进入"系统设置" → "音源管理"上传源文件
3. **搜索音乐**: 在搜索框输入歌曲名，选择音源后搜索
4. **下载管理**: 进入"下载管理"查看和管理下载任务
5. **歌曲管理**: 进入"歌曲管理"编辑元数据和批量操作

## 🐛 故障排除

### 容器启动失败
```bash
# 查看日志
docker logs melodyhub

# 重新构建并启动
docker-compose up -d --build
```

### 音频无法播放
- 检查音源是否返回有效链接
- 查看浏览器控制台错误
- 确认服务器网络正常

### 下载失败
- 检查音乐目录权限
- 查看服务器日志
- 确认磁盘空间充足

## 📝 开发计划

- [x] 后端核心模块
- [x] 前端 Vue 3 界面
- [x] Docker 部署
- [ ] 用户认证系统
- [ ] 播放列表管理
- [ ] 移动端适配
- [ ] 多用户支持
- [ ] 音乐推荐功能

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

Apache License 2.0

## 🙏 致谢

本项目基于 [lx-music-desktop](https://github.com/lyswhut/lx-music-desktop) 的核心逻辑开发，感谢原项目的贡献者们。

---
