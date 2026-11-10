# 双语对照 · Bilingual README

# Turn an Idle Machine Into a Voice-Only Agent Box

> **中文**｜一台吃灰的旧设备，通上电、连上网、开个麦克风，就变成不用看屏幕的智能体。
> **EN**｜No screen. No keyboard. Just power, network, a microphone — and your voice.

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE) [![Release: v1.0.0](https://img.shields.io/badge/release-v1.0.0-blue.svg)](https://github.com/liuda1999/dsh-voice-mode-headless/releases/tag/v1.0.0) [![DSH: dsh-plugin](https://img.shields.io/badge/DSH-dsh--plugin-181717.svg)](https://github.com/topics/dsh-plugin)

[简体中文](README.md) · [English](README.en.md) · **中英双语 / Bilingual**

⭐ **CN**｜先别急着往下翻，麻烦先去给上游点个 Star：[qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode)。没有那个项目，这个仓库连一行字都写不出来。文末的致谢是真心话，不是客套。
⭐ **EN**｜Before another line, please star the upstream project. Without it, not a single line here would exist. The tribute at the end is heartfelt, not boilerplate.

📖 **CN**｜完全公开、MIT 许可，随便看、随便用、随便改；上游版权写在 [NOTICE.md](NOTICE.md)。
📖 **EN**｜Fully public, MIT licensed — read it, use it, fork it. Upstream attribution lives in [NOTICE.md](NOTICE.md).

---

## 01 · 一句话讲明白 / What It Is, In One Breath

**CN**｜一台吃灰的旧 Mac 或小主机，接上网、开个麦克风，就变成不用看屏幕的智能体。说一句「肥鱼，看看昨晚的日志有没有报错」，它自己去查，再用语音把结论念回来：「下午三点有一条超时，别的都正常。」想核对细节，在手机或另一台电脑上打开 Web 页面翻会话记录；让它去局域网另一台机器取个文件、发个汇报，也是一句话的事。**不说话时它安安静静，一开口就开始干活。** 没有显示器，没有鼠标键盘，也不用每次开机点一遍登录和授权 —— 这个仓库装的就是这套能力。

**EN**｜An old Mac or a small box gathering dust becomes a headless agent once you give it network and a microphone. Say "肥鱼, check last night's logs for errors" and it goes looking, then reads the answer back: "One timeout at 3pm, everything else is fine." Need the details? Open the web UI on your phone or another computer and scroll the transcript. Asking it to pull a file from another machine on the LAN and report back is one sentence too. **Silent while you're quiet, working the moment you speak.** No monitor, no mouse, no keyboard, no logging in and re-authorizing the mic on every boot.

---

## 02 · 先说个特别容易误会的事 / One Thing People Get Wrong

**CN**｜这不是一个「用的时候打开一下」的小工具，也不是每次都要重新调用一遍的技能。**它是装一次、就长期住在这台机器里的能力。** 装好之后开机自己起来，崩了被人拉起来，重启也不用重新登录、重新点授权。你要做的只有「说话」。所以这里放的是「怎么装上去、装完怎么管」的完整说明，外加一个 WorkBuddy SKILL 包 —— 是给设备装耳朵和嘴巴的施工手册，不是每轮对话触发一次的快捷指令。

**EN**｜This is not a tool you open when you need it, and not a skill you invoke on every turn. **It is a capability you install once and keep.** It starts on boot, gets relaunched if it crashes, and needs no manual login or re-consent after a reboot. Your only job is to speak. What lives here is a complete "how to install it, how to live with it" guide plus a WorkBuddy SKILL package — a construction manual for giving a machine ears and a mouth, not a per-chat shortcut.

---

## 03 · 装好之后，你手上只需要什么 / What You Actually Need

| 需要 / Need | 不需要 / Do not need |
|---|---|
| 电 · Power | 显示器 · A monitor |
| 网 · Network | 鼠标、键盘 · A mouse or keyboard |
| 一个能用的麦克风 · One working microphone | 浏览器界面 · A browser UI |
| 一张嘴 · Your voice | 每次开机手动登录、手动点授权 · Logging in and re-authorizing after every reboot |

**CN**｜麦克风授权只在第一次装的时候人工点一次「允许」，之后再也不用管。
**EN**｜Mic permission is a one-time manual click during setup; a background process cannot show that dialog itself.

---

## 04 · 它能帮你做什么 / What You Can Ask It To Do

**CN**｜问点什么、查点什么，让它自己调工具跑完，只念结论；盯着某台机器，有异常主动汇报；在局域网里跑去别的设备取文件、传文件、拿结果；整理资料、算数、写点东西，然后读给你听；在另一台设备上通过远程 / Web UI 翻会话记录，检查它干得对不对。关键不是「能语音聊天」，而是**这台机器没有屏幕、你也不用坐在它面前**，它还能真的动手干活、把结果交出来。回答会被强制压成口语短句 —— 不念 markdown、表格、代码块，也不念命令，因为用户根本看不见屏幕。

**EN**｜Look something up and hear only the conclusion; watch another machine and speak up when something looks wrong; reach into the LAN to fetch a file, move it, or bring results back; sort material, do the arithmetic, write something — then read it aloud; check what it actually did from another device over remote / Web UI. The point is not "voice chat" — it is that **the machine has no screen and you are not sitting in front of it**, yet it still takes action and hands you the result. Replies are forced into short spoken sentences: no markdown, tables, code blocks or commands read aloud.

---

## 05 · 跟手机上的语音助手有啥不一样 / How It Differs From a Voice Assistant

| | 常见语音助手 / Typical assistant | 这台盒子 / This box |
|---|---|---|
| 得有块屏幕吗 / Needs a screen | 基本得有 / Usually | 完全不用 / Never |
| 回答怎么给你 / How you get it | 显示 / 念一句 / Displayed or one line | 逐句念出来 / Read aloud sentence by sentence |
| 能插嘴吗 / Can you interrupt | 多数得等 / Usually you wait | 说一句完整的话立刻停 / A complete sentence stops it |
| 会操作别的机器吗 / Operate other machines | 看生态 / Depends | 会，工具与网络都在工作区里 / Yes, tools and network in its workspace |
| 干完的痕迹 / Where's the record | 多数看完就没了 / Mostly gone | 会话存着，Web UI 随时翻 / Kept, browsable in the web UI |
| 识别要额外 API Key 吗 / Extra ASR key | 常常要 / Often | 本地识别，不用 / On-device, no |

---

## 06 · 大概是怎么跑起来的 / How It Works Under the Hood

**CN**｜别被名词吓到，就是一条流水线：麦克风 → 采集 App → FIFO 管道 → `bridge.mjs`（判断有没有声音、边听边出字、段末定稿、唤醒词、headless 会话、逐句合成、播放 + 三声提示音）→ 会话存盘并登记到「语音对话」工作区。有个坑得说清楚：上游插件原本在浏览器里录音，宿主端没有采集代码；这台机器连浏览器都不开，所以采集与桥接只能自己补。模型、音色表、下载脚本来自上游。

**EN**｜A pipeline, nothing more: mic → capture app → FIFO → `bridge.mjs` (silence gate, streaming ASR, second-pass correction, wake word, headless session, sentence-level TTS, playback + cue tones) → session on disk, registered in the voice workspace. One caveat: upstream records inside the browser, so the host has no capture code; this machine never opens a browser, which is why capture and bridge had to be built. Models, voice presets and the download script come from upstream.

```
You speak → capture app (16 kHz mono float32) → FIFO → bridge.mjs
        → [VAD | streaming ASR | final ASR | wake word | headless session | VITS | afplay]
        → session file + "语音对话" workspace
```

---

## 07 · 一次对话是怎么判定的 / How One Turn Is Decided

**CN / EN**｜说白了就是「什么时候算说话、什么时候算说完」/ In plain terms: when are you speaking, and when are you done?

1. **CN** 安静时识别器不启动，CPU 几乎为 0 ｜ **EN** In silence the recognizer is off; idle CPU ≈ 0.
2. **CN** 一有声音就收，往前多留 300 毫秒，句首不丢 ｜ **EN** Sound starts a segment with 300 ms pre-roll.
3. **CN** 连续安静 **2 秒**算说完 ｜ **EN** **2000 ms** of silence ends the segment.
4. **CN** 开头喊「肥鱼」就剥掉名字，剩下的是指令 ｜ **EN** Strip the wake word; the rest is the instruction.
5. **CN** 只喊名字回「我在」，接下来 20 秒免唤醒 ｜ **EN** Just the name → "我在" (here) + a 20 s wake-free window.
6. **CN** 它念答案时你插一句完整的话，立刻停嘴 ｜ **EN** A complete sentence stops playback and takes over.
7. **CN** 忙的时候新指令排队，不丢 ｜ **EN** New instructions mid-task are queued, not dropped.

**CN**｜两字唤醒词容易识别跑偏，规矩是「末字精确、首字容许同音」；实在不行换三个字以上。
**EN**｜Two-syllable wake words are easy to mis-hear: last syllable exact, first may be a homophone. Use a longer one if needed.

---

## 08 · 每天一个新会话 / A Fresh Session Every Day

**CN**｜早期版本永远只用一个会话，上下文越攒越长。现在改成：**每天第一次开口新建一个当天会话，当天后续对话沿用，跨天首轮再换新的**，旧会话保留可查。这事由宿主侧自动完成，不会在回答里跟你汇报；想立刻清空上下文也可以手动开一段新的。
**EN**｜The early build kept one session forever and context grew bloated. Now **the first utterance of each day opens a new session for that day; everything else that day continues it; the first utterance after midnight opens another**. Yesterday's remain available. The host does this automatically and never announces it in a spoken reply; a manual reset is still possible.

---

## 09 · 装之前要准备啥 / Before You Start

- **CN** macOS 12+、Node 24（nvm 管比较省事）、`dsh` CLI 可用、已有 `web` profile ｜ **EN** macOS 12+, Node 24 (nvm keeps it painless), working `dsh` CLI, an existing `web` profile
- **CN** 一个能出声的麦克风 ｜ **EN** A microphone that actually picks up sound
- **CN** 一次性的图形登录能力，只为了点一次「允许使用麦克风」｜ **EN** One-time graphical login, purely to click "Allow" for mic access
- **CN** npm 可达；`huggingface.co` 常连不通，准备 `hf-mirror.com` 兜底 ｜ **EN** npm reachable; keep `hf-mirror.com` as fallback for Hugging Face

**CN**｜采集 App 重新编译会改签名哈希，麦克风授权要重新点 —— 装完就别再动那个二进制。
**EN**｜Recompiling the capture app changes its signature hash and invalidates mic permission. Once it works, leave that binary alone.

---

## 10 · 怎么装 / Installing It

**CN**｜九步，完整命令与踩坑见 [`references/语音模式说明.md`](references/语音模式说明.md) 第 10 节。
**EN**｜Nine steps; full commands and traps are in Section 10 of the reference doc.

1. 把语音插件装进 `web` profile / Add the voice plugin to the `web` profile — `dsh plugin --profile web add dsh-voice-mode`
2. 下载并校验模型（**有坑**：按固定 revision 补齐 4 个文件，32/32 全过）/ Download and verify models (**trap**: fetch 4 files at the pinned revision, confirm 32/32)
3. 建语音工作区，写好 `AGENTS.md` / Create the voice workspace and its `AGENTS.md` rules
4. 编译、签名采集 App，手动点一次麦克风授权 / Compile and sign the capture app, click mic permission once
5. 部署桥接，先跑一次 headless 拿会话 id / Deploy the bridge, run one headless turn for a session id
6. 配 DSH：语音开关、默认模型、云端密钥 / Configure DSH: voice switches, default model, cloud credentials
7. 装两个用户级 LaunchAgent（带崩溃拉起）/ Install two user-level LaunchAgents with crash restarts
8. 开系统自动登录 / Enable system auto-login
9. 验收 / Verify

**CN**｜两个经典坑：工作区记录五个字段必须写全（少 `updatedAt` 侧栏会空白）；别把采集改成系统级 LaunchDaemon，麦克风 TCC 只在登录会话里生效，硬改只会拿到 `auth_status=2`。
**EN**｜Two classic traps: the workspace record needs all five fields (`updatedAt` missing blanks the sidebar); never turn capture into a system LaunchDaemon — mic TCC only works in a login session, so you will just get `auth_status=2`.

---

## 11 · 装完怎么知道它真活了 / How To Know It's Alive

1. **CN** 采集与桥接两个进程都在 ｜ **EN** Both capture and bridge processes running
2. **CN** 采集日志 `frames` 一直涨、`peak` 不为 0 ｜ **EN** `frames` climbing, `peak` non-zero
3. **CN** 桥接日志每 4 秒一行电平 ｜ **EN** A bridge level line every 4 seconds
4. **CN** 喊「肥鱼」→「我在」→ 给任务 → 正常回答 ｜ **EN** "肥鱼" → "我在" → task → normal answer
5. **CN** 同一天 `session-id.txt` 不变，跨天首轮换新 ｜ **EN** `session-id.txt` stable within a day, new after midnight

---

## 12 · 日常想调点什么 / Everyday Tweaks

| 想改 / Want | 动哪儿 / Where |
|---|---|
| 唤醒词 / Wake word | `VOICE_WAKE` |
| 抢话、老打断 / Cuts you off | 调大 `VOICE_SILENCE_MS`（现在 2 秒）/ Raise it (currently 2000) |
| 声音太轻、太吵 / Too quiet or trigger-happy | `VOICE_RMS` |
| 念得太快 / Reads too fast | `VOICE_SPEED`（0.9） |
| 换音色 / Different voice | `voice.txt` + 重启桥接 / + restart bridge（suyingxue / gunian / fushiyu / bingjiao / bazong） |
| 答案太啰嗦 / Too long | 改工作区 `AGENTS.md` / Edit workspace `AGENTS.md` |
| 换模型 / Cloud or local | headless profile 的 / `agent-default-model`（下轮生效 / next turn） |
| 立刻开新会话 / Fresh session now | `printf '' > <VOICE_DIR>/session-id.txt` |

---

## 13 · 出问题了先看这儿 / When Something Breaks

| 现象 / Symptom | 八成是 / Likely | 怎么办 / Fix |
|---|---|---|
| 完全没反应 / Dead silent | 采集停了 / Capture stopped | 看门狗 12 秒自动拉起，或手动 kickstart / 12 s watchdog, or kickstart |
| 峰值恒定极低 / Peak near zero | 输入设备选错、音量为 0 / Wrong device or zero volume | 查系统默认输入 / Check default input |
| 喊名字没反应 / Wake word ignored | 识别跑偏 / 不在 20 秒窗口 / Mis-recognition or outside window | 已有定稿纠错；换 3 字以上唤醒词 / Second-pass ASR; longer wake word |
| 话没说完就执行 / Cut off mid-sentence | 停顿太久 / Paused too long | 调大 / Raise `VOICE_SILENCE_MS` |
| `session locked, retry` | Web 界面占着写锁 / UI holds the write lock | 关掉页面；每 5 秒重试 / Close the tab; retries every 5 s |
| 侧栏看不到新会话 / New session missing | 宿主启动时才载入列表 / Host loads list at startup | 刷新或重启 Web 服务 / Refresh or restart |
| 念得含糊 / Mumbled | 音质、语速 / Quality, rate | 换音色 / Try another preset |

---

## 14 · 目前还做不到的事 / Known Limits

**CN**｜界面不实时；在界面打开语音会话会加写锁；单轮朗读超 800 字静默截断；打断要等 2 秒静音；蓝牙耳机播放时麦克风可能被切走；换模型没有运行时开关；冷启动依赖系统自动登录；早期遗留的隔离目录、备份、查看页脚本可以清掉。
**EN**｜The UI is not live; opening a voice session in it takes a write lock; a spoken turn is cut at 800 characters; barge-in needs 2 s of silence; Bluetooth headsets may lose the mic during playback; no runtime model switch; cold start depends on auto-login; leftovers from early experiments can be cleaned up.

---

## 15 · 这个仓库里都有啥 / What's In This Repo

```
.
├── README.md                       ← 简体中文主版 / Chinese primary
├── README.en.md                    ← English edition
├── README.bilingual.md             ← 本文件 / This file
├── SKILL.md                        ← WorkBuddy 技能入口 / Skill entry
├── references/语音模式说明.md        ← 完整方案原文 / Full original spec
├── community/                      ← DSH 社区收录状态 / Community listing status
├── CONTRIBUTING.md / CODE_OF_CONDUCT.md / SECURITY.md
├── NOTICE.md                       ← 上游版权 / Upstream attribution
├── LICENSE                         ← MIT
└── .github/                        ← Issue / PR 模板 / templates
```

**CN**｜想当技能用：把 `SKILL.md` 和 `references/` 放进 `~/.workbuddy/skills/dsh-voice-mode-headless/`，或下载 Release 包解压。只想自己装：直接读参考文档第 10 节。
**EN**｜As a skill: put `SKILL.md` and `references/` under `~/.workbuddy/skills/dsh-voice-mode-headless/`, or unzip the release archive there. As a human with a machine: read Section 10 of the reference doc.

---

## 16 · 完全开源，也进了 DSH 社区 / Fully Open Source, And In The DSH Community

**CN**｜公开仓库、[MIT](LICENSE)，随便看、用、改、分发，没有功能阉割，也没有附加条款；上游版权单独写在 [NOTICE.md](NOTICE.md)。贡献指南、行为准则、安全说明、Issue / PR 模板齐全。**DSH 社区**：已加官方生态标签 [`dsh-plugin`](https://github.com/topics/dsh-plugin)，多个社区目录靠它自动发现；也按 [DSH Plugin Radar](https://github.com/AdamPlatin123/dsh-plugin-radar) 的 🎓 技能 分区备好登记条目，进度见 [`community/README.md`](community/README.md)。精选插件库要求可安装插件 + 真实代码 + 仓库满 1 天，本仓库是文档型项目，按规矩不冒充插件去投主目录。

**EN**｜Public repo, [MIT](LICENSE), free to use, modify and redistribute with no feature gates or extra clauses; upstream attribution in [NOTICE.md](NOTICE.md). Contribution guide, code of conduct, security notes and issue/PR templates are all present. **DSH community**: the repo carries the official [`dsh-plugin`](https://github.com/topics/dsh-plugin) discovery topic, which several community directories scan automatically; an entry for the 🎓 Skills section of [DSH Plugin Radar](https://github.com/AdamPlatin123/dsh-plugin-radar) is prepared, with progress in [`community/README.md`](community/README.md). Curated plugin directories require an installable plugin, real code and a repo at least a day old — this is a documentation project, so by the rules we do not present it as a plugin.

---

## 17 · 先说清楚：这不是一个 DSH 插件 / This Is Not an Installable DSH Plugin

**CN**｜这里是**文档 + WorkBuddy 技能**，没有 `package.json`、`dsh.bundle`、`apply(ctx)` 或 `cordis.patch.yml`，**不能**用 `dsh plugin add` 安装。上面第 1 步那条命令装的是[上游插件](https://github.com/qishuilalala/dsh-voice-mode)，是部署链路的依赖，不是本仓库。想用这个仓库，要么把 `SKILL.md` 和 `references/` 放进 WorkBuddy 技能目录，要么照 README 给设备装一套。社区目录里它该归到「技能 / 文档 / 相关项目」。与 DeepSeek AI 官方没有隶属关系。

**EN**｜This repo is **documentation + a WorkBuddy skill**: no `package.json`, no `dsh.bundle`, no `apply(ctx)`, no `cordis.patch.yml` — it **cannot** be installed with `dsh plugin add`. Step 1 above installs the [upstream plugin](https://github.com/qishuilalala/dsh-voice-mode), a dependency of the deployment, not this repository. Use this repo by dropping `SKILL.md` and `references/` into your WorkBuddy skills directory, or by following the README to build the setup. In community directories it belongs under skills / documentation / related projects. No affiliation with DeepSeek AI.

---

## 18 · 跟上游到底是什么关系 / How This Relates To Upstream

**CN**｜上游 [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) 是很完整的 DSH 全双工语音插件，原本给浏览器界面用。我们这套面向连浏览器都不开的无显示器设备：**用到上游的**是模型下载脚本、识别与合成模型、音色表、设置页；**自己补的**是宿主端采集 App、FIFO、`bridge.mjs`、唤醒词与会话调度、LaunchAgent 自启、headless 会话接入、按天轮转会话。**上游把最难的地基浇好了，我们只是在旁边接了一根线。**

**EN**｜Upstream is a full-duplex voice plugin built for the browser. This project targets a machine that never opens one. **From upstream**: the model downloader, ASR/TTS models, voice presets and settings page. **Built here**: host-side capture app, FIFO, `bridge.mjs`, wake-word and session scheduling, LaunchAgent autostart, headless wiring, daily session rotation. **Upstream poured the foundation; we only ran one cable to it.**

---

## 19 · 几个常被问到的问题 / FAQ

**Q（CN）一定要 Mac 吗？** 目前按 macOS 写的，Windows / Linux 看思路就好，命令别照抄。｜ **Q (EN) Does it have to be a Mac?** The guide targets macOS; on other systems, take the idea, not the commands.

**Q（CN）一定要联网吗？** 识别本地，推理目前走线上；想全本地就把 headless 默认模型换成本地 provider，下轮生效。｜ **Q (EN) Does it need the internet?** ASR is local; reasoning currently runs in the cloud. Switch the headless default model to a local provider for offline use.

**Q（CN）为什么非要自动登录？** 麦克风授权只在登录会话里有效；代价是登录密码以系统 `kcpassword` 保存、登录窗口被跳过，改密码要重设。｜ **Q (EN) Why auto-login?** Mic permission only exists inside a login session; the cost is `kcpassword` storage and a skipped login window.

**Q（CN）能用 `dsh plugin add` 装吗？** 不能，见第 17 节。｜ **Q (EN) Can I `dsh plugin add` this repo?** No — see section 17.

**Q（CN）算不算重写了上游？** 完全不算，也担不起；模型、音色、识别合成全靠上游。｜ **Q (EN) Is this a rewrite of upstream?** Not remotely; models, voices, ASR and TTS are all upstream's work.

---

## 20 · 许可 / License

**CN**｜文档与技能说明采用 **MIT**（[LICENSE](LICENSE)），可自由使用、修改、分发。上游同样是 MIT，其代码、模型与音色资源归 [@qishuilalala](https://github.com/qishuilalala) 及各自权利人所有；本仓库不主张上游代码的任何权利，也没有复制上游源码，完整归属见 [NOTICE.md](NOTICE.md)。
**EN**｜Documentation and skill description are **MIT** ([LICENSE](LICENSE)) — use, modify and redistribute freely. Upstream is MIT too; its code, models and voice assets remain the property of [@qishuilalala](https://github.com/qishuilalala) and their respective rights holders. We claim no rights over upstream code and copy none of its source; see [NOTICE.md](NOTICE.md).

---

## 21 · 🙇 写在最后：认认真真地，向上游鞠一躬 / A Proper Bow To Upstream

**CN**｜**先把话说得明明白白：这个仓库能存在，几乎全部功劳都属于 [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) 和它的作者 [@qishuilalala](https://github.com/qishuilalala)。我们真的只是站在人家肩膀上，往前挪了半步。** 把识别、定稿纠错、按句合成、打断、唤醒词、音色、模型下载与校验做扎实，还一轮轮修到两百多项测试全绿，那是真功夫；我们说破了天，也就是写了个采集小 App、架了根管道、把话递进去 —— 没有上游把地基浇好，这份文档一页都写不出来。🙏 **向作者致以最诚挚、最热烈的感谢和敬意！** 如果这个小仓库对您有一点用，请先把 Star 点给上游。我们这点补充不敢掠美，也不配比：凡是有价值的地方都是上游做得好，凡是不好用、不周到、写岔了的地方都是我们自己加的，跟上游一点关系都没有。能站在它的肩膀上做一点点延伸，是我们的运气。

**EN**｜**Let's be unambiguous: almost everything of value here belongs to [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) and its author [@qishuilalala](https://github.com/qishuilalala). We stood on their shoulders and moved half a step forward.** Getting streaming ASR, second-pass correction, sentence-level synthesis, barge-in, wake words, voice presets, model download and checksum verification right — then grinding through iteration after iteration until 250+ tests pass — is real craft, earned the hard way. What we did was write a small capture app, lay a pipe, and build a bridge to hand the words over. Without that foundation, not one page of this documentation would exist. 🙏 **To the author: our warmest, most sincere thanks and respect.** If anything here is useful to you, star upstream first. Our small addition claims no credit and invites no comparison: where this works, upstream did the hard part; where it is clumsy, incomplete or wrong, that is our own doing and has nothing to do with them. Getting to extend it, even a little, is our good fortune.
