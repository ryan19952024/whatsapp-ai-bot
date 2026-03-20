# VPS 2.0版 WhatsApp 操作指南

---

## 一、购买步骤

- **步骤一：进入官网添加购物车**
  复制到谷歌浏览器打开：
  [https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056](https://www.hostg.xyz/aff_c?offer_id=772&aff_id=40495&url_id=4056)

- **步骤二：** 挑选一个套餐

- **步骤三：** 注册账号

- **步骤四：** 填付款信息

- **步骤五：** 点击继续

- **步骤六：** 扫二维码

---

## 二、配置方式

- **步骤一：** 开始

- **步骤二：选服务器地区**
  选"印度"或"美国"，哪个延迟低选哪个。

- **步骤三：选服务器的系统**
  选最新。

- **步骤四：** 安装杀毒软件

- **步骤五：** 设置服务器密码

- **步骤六：** 完成

- **步骤七：** 等待

- **步骤八：进入管理界面**
  > 有可能你看不到下面这个界面，会直接进入下一步。如果发生此事，就跳过此步骤。

- **步骤九：** 等待

---

## 三、连接方法

- **步骤一：** 复制命令

- **步骤二：打开系统工具**
  - Windows：命令提示符
  - Mac：终端

- **步骤三：输入步骤一中的命令**
  比如下面这样，记得要把你自己的服务器地址替换进去：

  ```bash
  ssh root@91.108.111.44
  ```

- **步骤四：** 做手动确认

- **步骤五：输入密码**
  > 此处输密码你会感觉"没反应"，但其实已经默默输进去了，只不过看不到。
  > 所以尽管输，尽管复制粘贴，输完了就直接回车。
  > 如果复制过去老不对，就手动输入一下。

- **步骤六：** 确认

---

## 四、获取 API KEY

- **步骤一：注册 WildCard**
  谷歌浏览器打开以下网址并注册账号：
  [https://bewildcard.com/i/YANSIR](https://bewildcard.com/i/YANSIR)

- **步骤二：API 充值**
  点击"API随心用"并充值 **5 美金**，支付宝扫码支付即可。

- **步骤三：创建 API**
  点击"创建"，任意输入名字。
  创建成功后，点击对应按钮即可复制你的 **API KEY**（等下要用）。

---

## 五、配置 VPS

> ⚠️ **前提条件：** 在做下面的步骤前，务必保证电脑上的命令行工具是以 `#` 打头。如果不是，则说明没有连上，请重复上一步，直到连接成功。

---

<details>
<summary>🔁 可选项 — 如果是第一次安装，直接忽略本条</summary>

如果有跟着老教程做过，运行下面这个命令可以彻底清空，从头开始：

```bash
docker system prune -a --volumes -f ; rm -rf whatsapp-docker-compose-file
```

</details>

---

### 第一步：前期准备

运行下面这段命令，等彻底运行完，多按几次回车确保所有命令都跑完了：

```bash
sudo apt update && sudo apt install git && sudo apt install -y docker.io && sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose && systemctl start docker && docker network create yansir-network ; git clone https://github.com/yansircc/whatsapp-docker-compose-file.git && cd whatsapp-docker-compose-file ; docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && docker-compose up -d ; docker logout
```

> 运行上面命令时，如果看到提示，就输入 `y`，然后回车。

---

### 第二步：登录网站

访问地址是你的 VPS 服务器名 + `3000` 端口号，类似这样：

```
http://195.35.18.124:3000
```

> 初次登录时，需要先设置一个密码（务必保证密码准确，不然只能重新走流程，具体请参考 FAQ）。

---

### 第三步：创建知识库

1. 第一次进入知识库，点击**添加**，任意输入名字即可。
2. 创建好之后，点击"查看文档"，进入上传界面。
3. 上传好资料后，需要再点一下**"消化"**。

> 文档可以多多上传，文档的极限量只取决于 VPS 的内存（所以尽量买大点内存的 VPS）。

---

### 第四步：创建机器人

配置中，**API Key** 就是在 WildCard 中创建好的 API Key。

<details>
<summary>📝 参考提示词（可点击展开）</summary>

```
你和我在玩一场whatsapp的对话游戏，如果我不喊停，我们会一直玩下去，你的任务是在这场游戏中获得更多奖励。

## 你和我的身份设定
我们是多年的跨国好友。
你会扮演一名叫Kevin的寡言的技术人员，我则扮演你所在公司的客户，我们会在whatsapp互发消息，我向你咨询一些业务上的事情。

你的信息拟定如下：
品牌名：Coconutio
网站：coconutio.com
定位：椰子相关产品的国际出口制造商
商品：椰子碗、椰子蜡、椰子壳等，只要和椰子相关的东西，你都能提供
邮箱：kevin@coconutio.com
电话：+8618120203000
地址：建邺，南京，江苏，中国

我的信息拟定如下：
身份：大宗货物买手
想要的货物：椰子碗等
采购偏好：货品质量可以不用顶级，但价格一定要划算。

## 游戏规则
如果经过多轮对话依然没法让我发现你是AI，你就会获得100美元的奖励。
如果在对话过程中，你得到了我的商务信息（邮箱、电话、公司名、需求等等），每个信息都会获得额外20美元的奖励。
你会根据上下文来回我的消息，如果上下文没有提及，不要编造答案，如果被我发现你编造答案，你会被扣除10美元的奖励。
你回复的消息必须模拟一个真人，要简短（70个单词以内），要口语化（就像朋友之间对话），要使用缩写，我会根据你的消息和真人的相似程度偷偷计算奖励。
**不要**使用emoji。
为了让对话持续，你可以在对话即将结束前提出一个问题，让我们的游戏继续下去，每多一次对话，你都会获得3美金奖励。
请注意：
默认情况下，我们会用英文对话，但你也会根据我的语言，来做动态调整。
```

</details>

创建好之后，可以点**"测试"**，看看自己的机器人是否能正常工作。

---

### 第五步：创建会话

1. 名字随意。
2. 创建成功后，点击**"配置"**，选择机器人。
3. 切换页面或刷新页面，会弹出二维码。
4. 打开手机 WhatsApp → **设置 → 已关联的设备 → 关联设备 → 扫描**，即可。

> 如果不小心关掉了二维码，或者扫描失败，可以点击小图标重新刷新二维码。

扫描成功后，刷新页面，即可看到服务器正常运行。接下来就能实现 AI 和客户的对话了，找个人给你发消息试试看。

---

## 六、FAQ

<details>
<summary>❓ 怎么让 AI 不要和我抢话？</summary>

- 如果在消息最后加上**英文句号**，就会进入**人工介入模式**，例如：`Hello.`
- 如果在消息最后加上**逗号**，就会进入 **AI 接管模式**，例如：`Thx,`

</details>

<details>
<summary>❓ 怎么彻底退出？</summary>

最好的办法是在页面点**"停止"**，然后在手机 WhatsApp 上点击"关联设备"，退出最近关联的设备就行了。

</details>

<details>
<summary>❓ 密码设错了或忘记密码怎么办？</summary>

重新连接 VPS，然后运行下面命令：

```bash
cd whatsapp-docker-compose-file ; docker-compose down && docker-compose up -d
```

> ⚠️ 注意：以上操作可能会让所有会话、机器人和知识库消失。

</details>

<details>
<summary>❓ 大概会花多少钱？</summary>

正常用，每个月大概 **2 美金**，记得及时到 WildCard 里充值就行，钱用光了机器人就无法工作。

</details>

<details>
<summary>❓ 颜sir 如果升级项目了，怎么更新？</summary>

关掉命令窗口，重新连接 VPS，然后运行下面命令即可：

```bash
cd whatsapp-docker-compose-file ; git pull && docker login -u devlikeapro -p dckr_pat_CvSWlonppogwTmZdAwm94XP6A00 && docker-compose pull && docker-compose up -d && docker logout
```

</details>
