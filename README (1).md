# VPS2.0 版 WhatsApp AI 机器人操作指南

> 基于 VPS 自建的 WhatsApp AI 自动回复机器人，支持知识库问答、人工/AI 切换。

---

## 目录

- [购买 VPS](#一购买-vps)
- [配置 VPS](#二配置-vps)
- [SSH 连接服务器](#三ssh-连接服务器)
- [获取 API KEY](#四获取-api-key)
- [部署服务](#五部署服务)
- [使用管理后台](#六使用管理后台)
- [绑定 WhatsApp](#七绑定-whatsapp)
- [FAQ](#faq)

---

## 一、购买 VPS

### 步骤 1：进入官网

在 Chrome 浏览器中打开以下链接：

```
https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056
```

### 步骤 2：选择套餐

推荐选择 **KVM 4**（$10.49/月），稳定性更好。KVM 2 也可，适合用户量较少的场景。

| 套餐 | CPU | 内存 | 硬盘 | 带宽 | 价格 |
|------|-----|------|------|------|------|
| KVM 1 | 1核 | 4GB | 50GB | 4TB | $4.49/月 |
| KVM 2 | 2核 | 8GB | 100GB | 8TB | $6.99/月 |
| KVM 4 | 4核 | 16GB | 200GB | 16TB | $10.49/月 ✅ 推荐 |
| KVM 8 | 8核 | 32GB | 400GB | 32TB | $19.99/月 |

> 💡 知识库文档上传量受 VPS 内存限制，建议尽量购买内存大的套餐。

### 步骤 3：注册账号

填写邮箱和密码，或直接用 Google / Facebook 账号登录。

### 步骤 4：填写付款信息

支持以下支付方式：

- 信用卡（Visa / Mastercard 等）
- PayPal
- Google Pay
- **支付宝（AliPay）**✅ 推荐国内用户使用
- Coingate（加密货币）

> 💡 有优惠码的话，在 `Have a coupon code?` 处填入 `vps101` 并点击 Apply 确认。

### 步骤 5：点击继续完成支付

支付宝支付时，扫描页面二维码即可完成付款。

---

## 二、配置 VPS

### 步骤 1：点击 Start Now 开始

### 步骤 2：选择服务器地区

推荐选择 **印度** 或 **美国**，选延迟低的那个。

### 步骤 3：选择操作系统

选择 **Ubuntu 23.04 64bit**（选最新版本）。

### 步骤 4：安装杀毒软件

勾选 **Monarx malware scanner**（免费），点击 Continue。

### 步骤 5：设置服务器密码

在 `Create root password` 处设置登录密码。

> ⚠️ **务必记录下这个密码**，后续 SSH 连接时需要用到！

### 步骤 6：点击 Finish Setup 完成

### 步骤 7：等待部署

页面会显示进度条，部署约需 3 分钟，完成后会发送邮件通知。

### 步骤 8：进入管理界面

部署完成后，点击 **VPS dashboard → Manage** 进入管理后台。  
等待服务器状态变为 `Running`（绿色），再等约 2 分钟即可操作。

> 💡 建议将管理后台链接保存到书签，格式类似：
> `https://hpanel.hostinger.com/server/XXXXX/overview`

---

## 三、SSH 连接服务器

### 步骤 1：复制 SSH 命令

在 VPS 管理后台 → **SSH access** 标签页，复制 Terminal 栏的命令，格式如下：

```bash
ssh root@你的服务器IP
```

### 步骤 2：打开终端工具

- **Windows**：搜索并打开「命令提示符」
- **Mac**：搜索并打开「终端」

### 步骤 3：粘贴并执行命令

将复制的命令粘贴进终端，按回车。

### 步骤 4：首次连接确认

看到如下提示时，手动输入 `yes` 并回车：

```
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

### 步骤 5：输入密码

输入密码时，**终端不会显示任何字符**，这是正常现象。直接输入或粘贴密码后按回车即可。

### 步骤 6：确认连接成功

看到如下提示，说明连接成功：

```
root@srv501513:~#
```

---

## 四、获取 API KEY

### 步骤 1：注册 WildCard

在 Chrome 中打开并注册账号：

```
https://bewildcard.com/i/YANSIR
```

### 步骤 2：API 充值

点击左侧菜单「API 随心用」→「立即开始」，充值 **$5 美金**（支付宝扫码支付）。

### 步骤 3：创建 API Key

点击「创建」按钮，任意输入名字后确定。创建成功后，点击复制图标即可获取你的 API Key（格式类似 `sk-...`）。

> ⚠️ API Key 请妥善保管，后续配置机器人时需要用到。

---

## 五、部署服务

确保终端已连接到 VPS（提示符为 `#` 开头），然后执行以下步骤。

### 可选：清空旧数据（仅限已跑过旧版本的用户）

> 第一次安装请跳过此步骤！

```bash
docker system prune -a --volumes -f ; rm -rf whatsapp-docker-compose-file
```

### 第一步：前期准备

复制并运行以下命令（一次性粘贴，等待完全执行完毕，多按几次回车确认）：

```bash
sudo apt update && sudo apt install git && sudo apt install -y docker.io && sudo curl -L \
"https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" \
-o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose && \
systemctl start docker && docker network create yansir-network ; \
git clone https://github.com/yansircc/whatsapp-docker-compose-file.git && \
cd whatsapp-docker-compose-file ; \
docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && \
docker-compose up -d ; docker logout
```

> 💡 执行过程中如果看到 `Continue [y/N]` 提示，输入 `y` 并回车。

---

## 六、使用管理后台

### 第二步：登录管理网站

在浏览器中输入以下地址（替换为你自己的 VPS IP）：

```
http://你的VPS的IP:3000
```

例如：`http://195.35.18.124:3000`

首次登录时需要设置密码，**务必记准**，忘记密码只能重置（见 FAQ）。

### 第三步：创建知识库

1. 点击左侧知识库图标
2. 点击右上角 `+` 新建知识库，输入任意名字
3. 点击「查看文档」，上传 `.pdf`、`.txt`、`.md` 格式文件
4. 上传完成后，点击「消化」按钮，等待处理完成（绿点亮起即成功）

### 第四步：创建机器人

1. 点击左侧机器人图标
2. 点击 `+` 新建，参考以下配置：

| 字段 | 填写内容 |
|------|----------|
| 机器人名称 | 任意 |
| 类型 | 通用 |
| 模型 | gpt-4-turbo（默认） |
| API Key | 填入 WildCard 中创建的 Key |
| 远端地址 | `https://api.openai.com/v1`（默认） |
| 关联知识库 | 选择已创建的知识库（可多选） |
| 提示词 | 见下方示例 |

#### 提示词示例

```
你和我在玩一场 whatsapp 的对话游戏，如果我不喊停，我们会一直玩下去，你的任务是在这场游戏中获得更多奖励。

## 你和我的身份设定
我们是多年的跨国好友。你会扮演一名叫 Kevin 的寡言的技术人员，我则扮演你所在公司的客户，我们会在 whatsapp 互发消息，我向你咨询一些业务上的事情。

你的信息拟定如下：
- 品牌名：Coconutio
- 网站：coconutio.com
- 定位：椰子相关产品的国际出口制造商
- 商品：椰子碗、椰子蜡、椰子壳等
- 邮箱：kevin@coconutio.com
- 电话：+8618120203000
- 地址：建邺，南京，江苏，中国

## 游戏规则
- 你会根据上下文来回复消息，如果上下文没有提及，不要编造答案
- 回复必须模拟真人，简短（70个单词以内），口语化，使用缩写
- 不要使用 emoji
- 为了让对话持续，可以在对话即将结束前提出一个问题
- 默认用英文对话，但会根据对方语言动态调整
```

3. 点击 Submit 保存
4. 可点击「测试」验证机器人是否正常工作

### 第五步：创建会话并绑定 WhatsApp

1. 点击左侧会话图标，点击 `+` 新建会话，名字任意
2. 创建成功后点击「配置」，选择对应的机器人，点确认
3. 页面会弹出二维码
4. 打开手机 WhatsApp → 设置 → 已关联的设备 → 关联设备 → 扫描二维码
5. 扫描成功后刷新页面，会话状态变为绿色即表示运行正常

> 💡 如果二维码消失或扫描失败，点击会话旁的二维码小图标可重新刷新。

---

## 七、绑定 WhatsApp

完成以上步骤后，AI 机器人即可自动回复 WhatsApp 消息。找人发一条消息测试效果。

---

## FAQ

### Q：怎么让 AI 不要和我抢话？

在消息末尾加英文标点来切换模式：

- 末尾加 `.`（英文句号）→ 进入**人工介入**模式，例如：`Hello.`
- 末尾加 `,`（英文逗号）→ 进入 **AI 接管**模式，例如：`Thx,`

---

### Q：怎么彻底退出？

1. 在管理后台点击会话的「停止」
2. 手机 WhatsApp → 已关联的设备 → 退出最近关联的设备

---

### Q：密码设错了或忘记密码怎么办？

重新连接 VPS，运行以下命令（注意：**会清空所有会话、机器人和知识库数据**）：

```bash
cd whatsapp-docker-compose-file ; docker-compose down && docker-compose up -d
```

---

### Q：大概每月花多少钱？

API 费用正常使用约 **$2/月**。记得定期在 WildCard 中充值，余额不足时机器人将无法工作。

---

### Q：如何更新到最新版本？

关闭命令窗口，重新连接 VPS，运行：

```bash
cd whatsapp-docker-compose-file ; git pull && \
docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && \
docker-compose pull && docker-compose up -d && docker logout
```

---

## 费用总结

| 项目 | 费用 |
|------|------|
| VPS（KVM 4，24个月） | ~$10.49/月 |
| API 使用费（WildCard） | ~$2/月 |
| **合计** | **约 $12/月** |

---

## 相关链接

- VPS 购买：[Hostinger](https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056)
- API Key：[WildCard](https://bewildcard.com/i/YANSIR)
- Docker Compose 文件：[GitHub](https://github.com/yansircc/whatsapp-docker-compose-file)
