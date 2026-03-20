# 🤖 WhatsApp AI 自动回复机器人

> 基于 VPS 自建的 WhatsApp AI 客服机器人，支持知识库问答、人工/AI 无缝切换，无需订阅任何第三方服务。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Docker](https://img.shields.io/badge/Docker-ready-blue.svg)](./docker-compose.yml)
[![Platform](https://img.shields.io/badge/Platform-Ubuntu%2023.04-orange.svg)]()

---

## ✨ 功能特性

- 📚 **知识库问答** — 上传 PDF / TXT / MD 文档，AI 自动基于文档内容回答
- 🔀 **人工/AI 切换** — 消息末尾加 `.` 切人工，加 `,` 切 AI，随时接管
- 🌍 **多语言支持** — 自动识别对方语言，动态切换回复语种
- 🐳 **Docker 一键部署** — 单条命令完成全部环境配置
- 💰 **极低成本** — API 费用约 $2/月，完全自己掌控数据

---

## 🗂️ 项目结构

```
whatsapp-ai-bot/
├── docker-compose.yml     # Docker 服务编排配置
├── .env.example           # 环境变量模板（复制为 .env 后填写）
├── README.md              # 项目说明文档
├── LICENSE                # 开源协议
└── docs/
    └── setup-guide.md     # 详细图文部署教程
```

---

## 🚀 快速开始

### 前置要求

| 依赖 | 版本要求 |
|------|----------|
| Ubuntu | 23.04 64bit |
| Docker | 最新版 |
| Docker Compose | 最新版 |
| OpenAI API Key | 有余额即可 |

### 一键部署

```bash
sudo apt update && sudo apt install git && sudo apt install -y docker.io && sudo curl -L \
"https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" \
-o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose && \
systemctl start docker && docker network create yansir-network && \
git clone https://github.com/yansircc/whatsapp-docker-compose-file.git && \
cd whatsapp-docker-compose-file && \
docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && \
docker-compose up -d && docker logout
```

部署完成后，访问管理后台：

```
http://你的服务器IP:3000
```

---

## 📖 完整部署教程

详见 [docs/setup-guide.md](./docs/setup-guide.md)，包含：

- VPS 购买与配置
- SSH 连接方法
- API Key 获取
- 知识库创建与文档上传
- 机器人配置与提示词编写
- WhatsApp 绑定扫码

---

## ⚙️ 环境变量说明

复制模板文件并填写配置：

```bash
cp .env.example .env
```

| 变量名 | 说明 | 示例 |
|--------|------|------|
| `OPENAI_API_KEY` | OpenAI API Key | `sk-xxxx` |
| `OPENAI_BASE_URL` | API 接口地址 | `https://api.openai.com/v1` |
| `BOT_MODEL` | 使用的模型 | `gpt-4-turbo` |
| `BOT_NAME` | 机器人名称 | `Kevin` |
| `ADMIN_PASSWORD` | 管理后台密码 | 自定义，务必记住 |

---

## 💬 使用说明

### 人工 / AI 模式切换

| 操作 | 效果 |
|------|------|
| 消息末尾加 `.`（英文句号） | 进入**人工介入**模式，AI 停止回复 |
| 消息末尾加 `,`（英文逗号） | 恢复 **AI 接管**模式 |

### 知识库文件格式

支持 `.pdf`、`.txt`、`.md` 格式，上传后点击「消化」完成索引。

---

## 💰 费用参考

| 项目 | 费用 |
|------|------|
| VPS（KVM 4，月付） | ~$10.49/月 |
| VPS（KVM 4，24个月付） | ~$7.49/月 |
| API 使用费（正常用量） | ~$2/月 |
| **合计** | **约 $9~12/月** |

---

## ❓ 常见问题

**Q：忘记管理后台密码怎么办？**

```bash
cd whatsapp-docker-compose-file
docker-compose down && docker-compose up -d
```

> ⚠️ 此操作会清空所有会话、机器人和知识库数据，请提前备份。

**Q：如何更新到最新版本？**

```bash
cd whatsapp-docker-compose-file
git pull && \
docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && \
docker-compose pull && docker-compose up -d && docker logout
```

**Q：如何彻底卸载？**

```bash
docker system prune -a --volumes -f
rm -rf whatsapp-docker-compose-file
```

---

## 🔗 相关资源

- [VPS 购买（Hostinger）](https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056)
- [API Key 获取（WildCard）](https://bewildcard.com/i/YANSIR)
- [Docker Compose 源文件](https://github.com/yansircc/whatsapp-docker-compose-file)

---

## 📄 License

本项目基于 [MIT License](./LICENSE) 开源。
