# 安全说明

## 本仓库本身

仓库里没有可执行代码、没有安装脚本、不下载模型、不读取本地文件，只有 Markdown 文档和一个 WorkBuddy 技能说明（`SKILL.md`）。把它克隆下来不会运行任何东西。

## 照文档部署时会碰到的事

方案文档里描述的链路涉及一些需要你自己拿主意的操作，**这些操作由你在本机执行，与本仓库无关**：

| 事项 | 需要留意的 |
|---|---|
| 系统自动登录 | 登录凭据会以系统 `kcpassword` 形式保存，登录窗口被跳过；只在你能物理控制的设备上开启 |
| 麦克风 TCC 授权 | 一次性人工授权；按 App 的 cdhash 记忆，重新编译采集 App 会需要重新授权 |
| 云端模型密钥 | 放在 `<DSH_HOME>/.credentials.yaml`，别提交到任何仓库 |
| `allowLan: true` | 让局域网设备能调用语音接口，只在可信网络里开 |
| headless 会话 | 智能体会按语音工作区规则调用工具，等于把这台设备的操作能力交给了对话 |
| LaunchAgent / LaunchDaemon | 开机自启、崩溃拉起；确认自己知道怎么停用（`launchctl bootout`） |

## 报告问题

- **不要**在 issue、PR、讨论区里贴 API Key、密码、令牌、完整日志、真实绝对路径或会话内容，先脱敏；
- 如果发现文档里某条建议会带来安全风险，请开 issue 说明「哪一节、什么风险、建议怎么改」；
- 涉及不宜公开的细节，请通过 GitHub 私信维护者 [@liuda1999](https://github.com/liuda1999)。

上游项目的安全问题请到 https://github.com/qishuilalala/dsh-voice-mode/security 或它的 Issues 反馈，不要发到本仓库。
