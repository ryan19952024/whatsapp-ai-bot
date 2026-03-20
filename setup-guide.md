# 详细部署教程

本文档是 PDF 原版教程的完整文字版，适合跟着一步步操作。

---

## 第一部分：购买 VPS

### 步骤 1：进入官网

在 Chrome 浏览器打开：

```
https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056
```

### 步骤 2：选择套餐

| 套餐 | CPU | 内存 | 硬盘 | 价格 | 建议 |
|------|-----|------|------|------|------|
| KVM 1 | 1核 | 4GB | 50GB | $4.49/月 | 仅测试用 |
| KVM 2 | 2核 | 8GB | 100GB | $6.99/月 | 用户量少时可用 |
| KVM 4 | 4核 | 16GB | 200GB | $10.49/月 | ✅ 推荐 |
| KVM 8 | 8核 | 32GB | 400GB | $19.99/月 | 高并发场景 |

> 知识库文档上限受 VPS 内存影响，建议选 KVM 4 及以上。

### 步骤 3：注册账号

填写邮箱密码，或使用 Google / Facebook 快速登录。

### 步骤 4：付款

支持支付宝、PayPal、信用卡。国内用户推荐支付宝扫码付款。

> 💡 优惠码：`vps101`，在结算页 `Have a coupon code?` 处填入，点 Apply 生效。

---

## 第二部分：配置 VPS

### 步骤 1：点击 Start Now

### 步骤 2：选择服务器地区

选 **India（印度）** 或 **United States（美国）**，哪个延迟低选哪个。

### 步骤 3：选择操作系统

选 **Ubuntu 23.04 64bit**。

### 步骤 4：安装杀毒软件

勾选 Monarx（免费），点 Continue。

### 步骤 5：设置 Root 密码

> ⚠️ 此密码非常重要，请记录到安全的地方！

### 步骤 6：点击 Finish Setup

### 步骤 7：等待部署完成

约需 3 分钟，状态变为 `Running`（绿色）后再等 2 分钟。

---

## 第三部分：SSH 连接服务器

### Windows 用户

1. 按 `Win + S` 搜索「命令提示符」，打开
2. 在 VPS 管理后台 → SSH access 标签页，复制 Terminal 命令
3. 粘贴到命令提示符，回车

### Mac 用户

1. 按 `Cmd + Space` 搜索「终端」，打开
2. 粘贴 SSH 命令，回车

### 连接流程

```bash
# 1. 输入命令
ssh root@你的服务器IP

# 2. 首次连接，手动输入 yes
Are you sure you want to continue connecting? yes

# 3. 输入密码（不显示字符，正常现象）
root@xxx's password: ****

# 4. 看到 # 开头说明连接成功
root@srv501513:~#
```

---

## 第四部分：获取 API Key

### 步骤 1：注册 WildCard

```
https://bewildcard.com/i/YANSIR
```

### 步骤 2：充值

点击「API 随心用」→「立即开始」，充值 $5（支付宝扫码）。

### 步骤 3：创建并复制 API Key

点击「创建」→ 输入名字 → 确定 → 点复制图标获取 Key（`sk-` 开头）。

---

## 第五部分：一键部署

确保终端显示 `#` 提示符后，运行以下命令：

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

> 如出现 `Continue [y/N]` 提示，输入 `y` 回车。

---

## 第六部分：管理后台操作

### 登录

浏览器打开 `http://你的IP:3000`，首次登录设置密码。

### 创建知识库

1. 左侧点知识库图标 → `+` 新建 → 输入名字
2. 点「查看文档」→ 拖拽上传文件（支持 .pdf / .txt / .md）
3. 点「消化」→ 等绿点亮起

### 创建机器人

1. 左侧点机器人图标 → `+` 新建
2. 填写：名称、类型（通用）、模型（gpt-4-turbo）、API Key、关联知识库、提示词
3. 点 Submit → 可点「测试」验证

### 提示词参考

```
你是一名叫 Kevin 的客服，代表 [你的公司名] 在 WhatsApp 上与客户沟通。
回复要简短（70词以内）、口语化、不用 emoji。
根据知识库内容回答问题，没有相关信息时如实说明，不要编造。
默认用英文，根据对方语言自动切换。
```

### 创建会话并绑定 WhatsApp

1. 左侧点会话图标 → `+` 新建 → 输入名字
2. 点「配置」→ 选择机器人 → 确认
3. 页面弹出二维码
4. 手机打开 WhatsApp → 设置 → 已关联设备 → 关联设备 → 扫码
5. 刷新页面，状态变绿即成功

---

## 第七部分：日常维护

### 更新版本

```bash
cd whatsapp-docker-compose-file
git pull && \
docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && \
docker-compose pull && docker-compose up -d && docker logout
```

### 重启服务

```bash
cd whatsapp-docker-compose-file
docker-compose restart
```

### 查看日志

```bash
cd whatsapp-docker-compose-file
docker-compose logs -f
```

### 彻底重置（慎用，数据清空）

```bash
docker system prune -a --volumes -f
rm -rf whatsapp-docker-compose-file
```
