# DSH Plugin Radar 登记材料

目标仓库：https://github.com/AdamPlatin123/dsh-plugin-radar
目标文件：`PLUGINS.md` → 🎓 技能 分区
分支：`liuda1999:add-dsh-voice-mode-headless`（已推送）

## 登记行（已写入分支）

```markdown
| dsh-voice-mode-headless | [liuda1999/dsh-voice-mode-headless](https://github.com/liuda1999/dsh-voice-mode-headless) | 无显示器设备的纯语音智能体部署方案与 WorkBuddy SKILL：麦克风采集 App → FIFO → bridge.mjs → headless 会话 → 本地 TTS，含九步部署、参数表、排障与按天轮转会话规则；入口为 SKILL.md 与 references/语音模式说明.md，非可安装 DSH 插件、不含 dsh.bundle；基于并致敬 qishuilalala/dsh-voice-mode | 待测 |
```

运行级按登记表约定填「待测」：没有在 DSH 官方运行环境里做过安装兼容性实测，不冒充 ✅。

## 一键创建 PR

https://github.com/AdamPlatin123/dsh-plugin-radar/compare/main...liuda1999:add-dsh-voice-mode-headless

## PR 标题

```
docs: 登记 liuda1999/dsh-voice-mode-headless（无显示器纯语音智能体部署方案 + SKILL）
```

## PR 正文

```markdown
### 登记条目

在 `PLUGINS.md` 的 🎓 技能 分区追加一行，运行级按规矩填「待测」。

- 仓库：https://github.com/liuda1999/dsh-voice-mode-headless
- 已添加 `dsh-plugin` topic。
- 性质说明：这是**文档 + WorkBuddy SKILL**，不是可安装的 DSH 原生插件，仓库内没有 `package.json` / `dsh.bundle` / `apply(ctx)`，不能 `dsh plugin add`。放在 🎓 技能 分区是因为它交付的是一份 SKILL.md 与完整部署说明。
- 内容：macOS 无显示器设备的纯语音链路（麦克风采集 App → FIFO → bridge.mjs → headless 会话 → 本地 TTS），含九步部署、参数表、排障表与按天轮转会话规则。
- 许可：MIT（LICENSE），上游版权见 NOTICE.md。
- 关系：复用上游 qishuilalala/dsh-voice-mode 的模型、音色表与下载脚本，宿主端采集与桥接为自建；README 末尾有致谢。

只改了登记表这一行，没有动其他条目。
```
