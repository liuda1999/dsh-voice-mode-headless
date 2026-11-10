# Turn an Idle Machine Into a Voice-Only Agent Box

> No screen. No keyboard. Just power, network, a microphone — and your voice.

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE) [![Release: v1.0.0](https://img.shields.io/badge/release-v1.0.0-blue.svg)](https://github.com/liuda1999/dsh-voice-mode-headless/releases/tag/v1.0.0) [![DSH: dsh-plugin](https://img.shields.io/badge/DSH-dsh--plugin-181717.svg)](https://github.com/topics/dsh-plugin)

[简体中文](README.md) · **English** · [语言切换 / Switch](README.bilingual.md)

⭐ **Before you read another line, please star the upstream project:** [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode). Without it, not a single line of this repository would exist. There is a proper tribute at the end — and it is heartfelt, not boilerplate.

---

## What It Is, In One Breath

An old Mac or a small box gathering dust becomes a headless agent once you give it network and a microphone.

Say "肥鱼, check last night's logs for errors" and it goes looking, then reads the answer back: "One timeout at 3pm, everything else is fine." Need the details? Open the web UI on your phone or another computer and scroll the transcript. Asking it to pull a file from another machine on the LAN and report back is one sentence too.

**Silent while you're quiet, working the moment you speak.** No monitor, no mouse, no keyboard, no logging in and re-authorizing the mic on every boot. That is what this repository installs.

---

## One Thing People Get Wrong

This is not a tool you open when you need it, and not a skill you invoke on every turn.

**It is a capability you install once and keep.** After that, it starts on boot, gets relaunched if it crashes, and needs no manual login or re-consent after a reboot. Your only job is to speak; everything else runs in the background.

So what lives here is a complete "how to install it, how to live with it" guide, plus a WorkBuddy SKILL package. Think of it as a construction manual for giving a machine ears and a mouth — not a shortcut you trigger once per chat.

---

## What You Actually Need

| You need | You do not need |
|---|---|
| Power | A monitor |
| Network | A mouse or keyboard |
| One working microphone | A browser UI |
| Your voice | Logging in and re-authorizing after every reboot |

Mic permission is a **one-time manual click** during setup. A background process cannot show that dialog itself. After that, automatic login brings up two small services and the whole chain is alive.

---

## What You Can Ask It To Do

- Look something up, run the tools itself, and read back only the conclusion;
- Watch another machine and speak up when something looks wrong;
- Reach into the LAN to fetch a file, move it, or bring results back;
- Sort through material, do the arithmetic, write something — then read it aloud;
- Check what it actually did from another device over remote / Web UI;
- Handle a thought at 2am without turning on a light or finding a keyboard.

The point is not "voice chat" — plenty of things do that. The point is that **the machine has no screen and you are not sitting in front of it**, yet it still takes action and hands you the result.

One more detail that matters: replies are forced into **short spoken sentences** inside a dedicated voice workspace. No markdown, no tables, no code blocks, no reading commands aloud. Nobody is looking at a screen; that stuff would be torture to listen to.

---

## How It Differs From a Voice Assistant

| | Typical assistant | This box |
|---|---|---|
| Needs a screen | Usually | Never |
| How you get the answer | Displayed, or one spoken line | Read aloud sentence by sentence, long answers included |
| Can you interrupt it | Usually you wait | The wake word stops playback instantly; echo and coughs do not |
| Will it operate other machines | Depends on the ecosystem | Yes — tools, commands and network live in its workspace |
| Where's the record | Mostly gone after reading | Sessions are kept; browse them in the web UI |
| Extra API key for listening | Often | On-device ASR, no extra key |

---

## How It Works Under the Hood

A pipeline, nothing more:

```
You speak
  │
  ▼
A tiny capture app (its only job is listening)
  │  16 kHz mono float32
  ▼
A FIFO pipe (think of it as a speaking tube)
  │
  ▼
bridge.mjs — the coordinator
  ├─ silence? do nothing, near-zero idle CPU
  ├─ streaming ASR while you talk
  ├─ second-pass ASR at end of segment (punctuation, corrections)
  ├─ wake-word match
  ├─ hand the instruction to a headless session
  ├─ synthesize the reply with a local voice, sentence by sentence
  └─ play it, with three short cue tones
  │
  ▼
Session file on disk, registered in the "语音对话" workspace
```

One caveat worth stating early: the upstream plugin records **inside the browser** (`getUserMedia`); the host side has no capture code at all. This machine does not even open a browser, so host-side capture and the bridge had to be built. Models, voice presets and the download script come from upstream; everything else here is our own wiring.

---

## How One Turn Is Decided

In plain terms: when are you speaking, and when are you done?

1. In silence the recognizer is off — idle CPU ≈ 0. Quiet sounds below RMS 0.006 and bursts under 300 ms are ignored.
2. Sound starts a segment with 300 ms of pre-roll; empty or punctuation-only results are dropped.
3. **2000 ms** of continuous silence ends the segment.
4. The wake word must be **at the start** of the sentence: second syllable exact, first may be a homophone — "飞鱼" wakes it, "买条鱼" does not.
5. **Wake word has top priority**: saying just the name stops playback instantly, replies "我在" (here), but **does not kill the running task**; the next 20 seconds need no wake word.
6. A short stop phrase right after it (stop / cancel / never mind…, ≤12 characters) terminates the task and replies "好的，停了".
7. Other instructions run immediately when idle, or queue until the current turn finishes.
8. During playback **only the wake word** can interrupt — echo, coughs and noise never cut a reply short.

---

## A Fresh Session Every Day

The baseline spec keeps one fixed session; this project adds a daily-rotation rule so context does not grow bloated:

**The first utterance of each day opens a new session for that day; everything else that day continues it; the first utterance after midnight opens another.** Yesterday's sessions stay available.

The host does this automatically. It will not announce "I created a new session" in a spoken reply — that would be noise. You can still start a fresh one manually, at the cost of current context.

---

## Before You Start

- A **macOS 12+** machine, Node 24 (nvm keeps it painless), a working `dsh` CLI, and an existing `web` profile;
- A microphone that actually picks up sound;
- **One-time** graphical login — purely to click "Allow" for mic access; a background process cannot trigger that prompt;
- Network: npm must be reachable; `huggingface.co` is often not, so keep `hf-mirror.com` as a fallback.

One warning: recompiling the capture app changes its code signature hash and invalidates mic permission. **Once it works, leave that binary alone.**

---

## Installing It

Nine steps. Full commands, config file contents and known traps are in **Section 10** of [`references/语音模式说明.md`](references/语音模式说明.md); this is just the map:

1. Add the voice plugin to the `web` profile (`dsh plugin --profile web add dsh-voice-mode`);
2. Download and verify models — **this one bites**: the download script fetches the default branch while runtime pins a fixed revision, so fetch the 4 files at that revision and confirm 32/32 checksums;
3. Create a dedicated voice workspace and write its `AGENTS.md` rules;
4. Compile and sign the capture app, click mic permission once;
5. Deploy the bridge, run one headless turn to obtain a session id;
6. Configure DSH: web-profile voice switches, headless default model, cloud credentials;
7. Install two user-level LaunchAgents (capture, bridge) with crash restarts;
8. Enable system auto-login so reboots need nobody at the keyboard;
9. Verify.

Two classic traps: **the workspace record needs all five fields** (`updatedAt` missing makes the whole sidebar blank), and **do not turn capture into a system LaunchDaemon** — mic TCC only works inside a login session, so you will just get `auth_status=2`.

Every path in the docs is a placeholder (`~`, `<VOICE_DIR>`, `<VOICE_WS>`, `<DSH_HOME>`, `<MODELS>`, `<UID>`). No machine-specific absolute path or account is baked in. Substitute your own values.

---

## How To Know It's Alive

1. Both the capture and bridge processes are running;
2. `frames` keeps climbing in the capture log and `peak` is not zero;
3. The bridge log prints a level line every 4 seconds;
4. Say "肥鱼" → hear "我在" → give a task → get a normal answer;
5. `session-id.txt` stays the same within a day, and changes on the first turn after midnight.

---

## Everyday Tweaks

| Want to change | Where |
|---|---|
| Wake word | `VOICE_WAKE` |
| It cuts you off too eagerly | Raise `VOICE_SILENCE_MS` (currently 2000) |
| Too quiet / noisy room triggers it | `VOICE_RMS` (currently 0.006) |
| Reads too fast | `VOICE_SPEED` (currently 0.9) |
| Different voice | Write a preset name into `voice.txt` and restart the bridge; choices: suyingxue / gunian / fushiyu / bingjiao / bazong |
| Answers too long | Edit the voice workspace's `AGENTS.md` |
| Cloud or local model | `agent-default-model` in the headless profile; takes effect next turn |
| Fresh session right now | `printf '' > <VOICE_DIR>/session-id.txt` |

Commands are in Section 7 of the reference doc; the parameter table is in 5.1.

---

## When Something Breaks

| Symptom | Likely cause | Fix |
|---|---|---|
| No response, no segments in the log | Capture stopped (device slept, audio route changed) | Capture app self-checks and binds the default input device; watchdog restarts after 3 s without audio, with a 10 s cooldown; kickstart manually if impatient |
| Peak level stuck near zero | Wrong input device or input volume at 0 | Check the system default input |
| Wake word ignored | Mis-recognition, not at the start, or outside the 20 s window | Second-pass ASR already corrects; say it at the start, or use a 3+ syllable wake word |
| Executed before you finished | Paused too long mid-sentence | Already relaxed to 2 s; raise `VOICE_SILENCE_MS` further |
| Log repeats `session locked, retry` | The session is open in the web UI and holds a write lock | Close that tab; the bridge retries every 5 s and does not switch sessions |
| New session missing from sidebar | The host loads its session list at startup | Refresh or restart the web service |
| Mumbled speech | Synthesis quality / rate | Rate is already 0.9; try another preset |

Full troubleshooting table: Section 8 of the reference doc.

---

## Known Limits (No Hiding)

- The web UI is not live; the session list needs a refresh or a service restart;
- Opening a voice session in the UI takes a write lock that conflicts with voice writes (it keeps retrying, never switches sessions);
- A single spoken turn is silently cut at 800 characters; the session record is unaffected;
- Interrupting playback requires the wake word; random speech, coughs or echo will not cut a reply short;
- Bluetooth headsets may lose the mic during playback, breaking barge-in;
- No runtime switch for the model — edit the profile;
- Cold start depends on system auto-login; changing the login password requires setting it up again;
- Leftovers from early experiments (isolated home dir, backup files, a retired viewer script) can be cleaned up.

---

## What's In This Repo

```
.
├── README.md                       ← Simplified Chinese (primary)
├── README.en.md                    ← This file
├── README.bilingual.md             ← Language switcher
├── SKILL.md                        ← WorkBuddy skill entry (triggers, navigation, hard rules)
├── references/
│   └── 语音模式说明.md              ← Full original spec: architecture, parameters, commands, deployment, troubleshooting, changelog
├── community/                      ← DSH community listing status and submission material
│   ├── README.md
│   └── dsh-plugin-radar.md
├── CONTRIBUTING.md / CODE_OF_CONDUCT.md / SECURITY.md
├── NOTICE.md                       ← Upstream attribution
├── LICENSE                         ← MIT
└── .github/                        ← Issue and PR templates
```

**As a WorkBuddy skill**: put `SKILL.md` and `references/` under `~/.workbuddy/skills/dsh-voice-mode-headless/`, or download the release archive and unzip it there. Then ask about turning an idle device into a voice box, deploying a headless voice chain, or "肥鱼 not responding" — the agent will look up the right section.

**As a human with a machine to set up**: read Section 10 of `references/语音模式说明.md`. It is a standalone build manual; no tooling required.

---

## Fully Open Source, And In The DSH Community

This repository is **fully public and fully open source**: public repo, [MIT](LICENSE), free to use, modify and redistribute, with no feature gates and no "open source, except..." clauses. Upstream attribution lives in [NOTICE.md](NOTICE.md).

The usual project hygiene is in place: [contribution guide](CONTRIBUTING.md), [code of conduct](CODE_OF_CONDUCT.md), [security notes](SECURITY.md), issue and PR templates. Issues are welcome.

**On the DSH community side:**

- The repo carries the ecosystem's official discovery topic [`dsh-plugin`](https://github.com/topics/dsh-plugin); directories such as dsh-plugin.org, dshmarketplace.dev and DSH Plugin Radar discover and list repos from it;
- An entry for the 🎓 Skills section of the [DSH Plugin Radar registry](https://github.com/AdamPlatin123/dsh-plugin-radar) has been prepared — progress and the one remaining manual step are in [`community/README.md`](community/README.md);
- Curated plugin directories require an installable plugin, real plugin code and a repo at least a day old. This is a documentation project, so by the rules we **do not present it as a plugin**; we take the skills / related-projects route instead.

---

## This Is Not an Installable DSH Plugin

Worth saying plainly, so nobody spends an afternoon on `dsh plugin add`:

- This repo is **documentation + a WorkBuddy skill** (`SKILL.md` + `references/语音模式说明.md`). There is no `package.json`, no `dsh.bundle`, no `apply(ctx)`, no `cordis.patch.yml`;
- The `dsh plugin --profile web add dsh-voice-mode` in step 1 above installs the [upstream plugin](https://github.com/qishuilalala/dsh-voice-mode) — a dependency of this deployment, not this repository;
- To use this repo, either drop `SKILL.md` and `references/` into your WorkBuddy skills directory or follow the README to build the setup yourself;
- In DSH community directories it belongs under skills / documentation / related projects, never "installable plugin". That is exactly how we registered it.

No affiliation with DeepSeek AI. This is not an official project.

---

## How This Relates To Upstream

Upstream [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) is a full-duplex voice plugin for DSH: streaming captions, sentence-by-sentence read-aloud with live subtitles, barge-in, optional wake word, on-device ASR with no extra API key. It was built for **the browser**.

This project targets a machine that **never opens a browser**. Therefore:

- From upstream: the `scripts/prefetch.mjs` downloader, ASR/TTS models, voice presets and settings page;
- Built here: host-side mic capture app, FIFO pipe, `bridge.mjs`, wake-word and session scheduling, LaunchAgent autostart, headless session wiring, daily session rotation.

Put simply: **upstream poured the foundation — models, recognition, synthesis, voices. We only ran one cable to it so a screenless machine could use it.** Sections 3 and 13 of the reference doc say the same thing.

---

## FAQ

**Q: Does it have to be a Mac?**
A: The current guide is written for macOS (LaunchAgents, auto-login, mic TCC, afplay). On Windows / Linux, read it for the idea; do not copy the commands.

**Q: Does it need the internet?**
A: ASR is local, but the reasoning model currently runs in the cloud with a key in `<DSH_HOME>/.credentials.yaml`. Switch the headless default model to a local provider for fully offline use — effective next turn.

**Q: Why is system auto-login mandatory?**
A: Mic permission only exists inside a user login session. Without auto-login, nobody logs in after a reboot and the two services never start. The cost: the login password is stored as system `kcpassword` and the login window is skipped; change the password and you must re-enable auto-login.

**Q: Can I install this repo with `dsh plugin add`?**
A: No. It is documentation and a WorkBuddy skill, not a DSH plugin. What you install is the upstream `dsh-voice-mode`; this repo is meant to be read or dropped into a skills directory.

**Q: Is this a rewrite of upstream?**
A: Not remotely, and we could not pull it off. Models, voices, ASR and TTS are all upstream's work; we only added the piece that listens and forwards when there is no browser.

---

## License

The documentation and skill description in this repo are **MIT** ([LICENSE](LICENSE)) — use, modify and redistribute freely. Upstream is MIT too; its code, models and voice assets remain the property of [@qishuilalala](https://github.com/qishuilalala) and their respective rights holders. We claim no rights over upstream code and copy none of its source; full attribution is in [NOTICE.md](NOTICE.md).

Contribution guide, code of conduct, security notes and issue/PR templates are in the repo. DSH community listing status: [`community/README.md`](community/README.md).

---

## 🙇 One Last Thing: A Proper Bow To Upstream

**Let's be unambiguous: almost everything of value here belongs to [qishuilalala/dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) and its author [@qishuilalala](https://github.com/qishuilalala). We stood on their shoulders and moved half a step forward.**

Getting streaming ASR, second-pass correction, sentence-level synthesis, barge-in, wake words, voice presets, model download and checksum verification right — then grinding through iteration after iteration until 250+ tests pass — that is **real craft**, earned the hard way. What we did, stripped of all drama, was write a small capture app, lay a pipe, and build a bridge to hand the words over. **Without that foundation, we could not have recognized a single sentence, and not one page of this documentation would exist.**

So:

- 🙏 **To [@qishuilalala](https://github.com/qishuilalala): our warmest, most sincere thanks and respect.** Thank you for open-sourcing this project, for filling in the potholes one by one, and for making it possible for others to build on top.
- ⭐ **If anything here is useful to you, star upstream first**: <https://github.com/qishuilalala/dsh-voice-mode>. They earned it.
- 📦 The [npm package](https://www.npmjs.com/package/dsh-voice-mode), [Releases](https://github.com/qishuilalala/dsh-voice-mode/releases) and [Issues](https://github.com/qishuilalala/dsh-voice-mode/issues) are the best places to support the author.
- 🫶 Our small addition **claims no credit and invites no comparison**. Where this works, upstream did the hard part; where it is clumsy, incomplete or wrong, that is our own doing and has nothing to do with them — please open an issue here.

Thank you again, sincerely, to the author and to this excellent project. Getting to extend it, even a little, is our good fortune. 🙏
