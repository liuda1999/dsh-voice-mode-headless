# DSH 社区收录状态

这个项目怎么进 DSH 开源社区、走到哪一步了，都记在这儿。

## ✅ 已经做完的

- **完全开源**：公开仓库、[MIT 许可](../LICENSE)、可直接 fork / clone / 分发；上游版权单独写在 [NOTICE.md](../NOTICE.md)，不把别人的功劳算到自己头上。
- **已加入 DSH 生态发现体系**：仓库加上了官方标签 [`dsh-plugin`](https://github.com/topics/dsh-plugin)。dsh-plugin.org、dshmarketplace.dev、DSH Plugin Radar 等社区目录都靠这个标签做常规扫描，会自动发现并收录本仓库。
- **已备好登记表条目**：在 fork 分支 `add-dsh-voice-mode-headless` 里，把一行登记写进了 [DSH Plugin Radar 的 `PLUGINS.md`](https://github.com/AdamPlatin123/dsh-plugin-radar/blob/main/PLUGINS.md) 的 🎓 技能 分区，运行级按规矩填「待测」。原文见 [dsh-plugin-radar.md](dsh-plugin-radar.md)。

## ⏳ 还差一步（网页上点一下，只是加速）

**先说明白：不点也不影响被收录。** `PLUGINS.md` 开头写着「未登记的仓库只要打 `dsh-plugin` / `dsh-external` topic，会在每日 02:00 全量扫描时自动收录」——本仓库已经打了 `dsh-plugin`，会自动进入雷达的全量索引。下面这个 PR 只是让它更快出现在人工策展的登记表里，并明确归到 🎓 技能 分区。

当前使用的 GitHub 细粒度令牌只能操作本人仓库，没有「向第三方仓库创建 PR」的权限，所以登记 PR 需要手动确认：

1. 打开 [这个 compare 链接](https://github.com/AdamPlatin123/dsh-plugin-radar/compare/main...liuda1999:add-dsh-voice-mode-headless)；
2. 点 **Create pull request**；
3. 标题和正文直接用 [dsh-plugin-radar.md](dsh-plugin-radar.md) 里写好的那一版。

合并之后，登记表与自动快照取并集，条目会进入全量索引（登记表的设计是「登记即可见」）。

## 为什么不投「精选插件库」的主目录

| 社区目录 | 收录要求 | 本仓库情况 |
|---|---|---|
| [awesome-dsh-plugin/awesome-dsh-plugin](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin) 主目录 | `package.json` 声明 `dsh.bundle`、真实可用代码（纯 README 仓库不收）、仓库满 1 天、加 `dsh-plugin` topic | 文档 + WorkBuddy SKILL，没有 bundle 和插件代码，仓库也是新建的 → **不符合** |
| [cccakeee/awesome-dsh-plugins](https://github.com/cccakeee/awesome-dsh-plugins) 已核验目录 | 至少一个原生可装载证据：`dsh plugin` 安装命令、`dsh.bundle` / `cordis.patch.yml`、`apply` 入口 | 没有 → 只能进全量聚合目录 / 相关项目观察名单 |
| [AdamPlatin123/dsh-plugin-radar](https://github.com/AdamPlatin123/dsh-plugin-radar) 登记表 | 表格加一行，🎓 技能 分区收 SKILL.md 类项目，登记即可见 | ✅ 合适，已按这个走 |

**我们不会把文档型项目包装成「可安装插件」去投主目录。** 这既是社区规则，也是对维护者时间的尊重。等以后这个仓库真的长出了 `dsh.bundle` 和可安装代码，再按规则补投不迟。

## 当前标签（复查过）

`dsh-plugin` · `dsh` · `deepseek-harness` · `dsh-voice-mode` · `voice-agent` · `headless` · `speech-to-text` · `text-to-speech` · `wake-word` · `macos` · `workbuddy-skill` · `homelab`

其中 `dsh-plugin` 是生态发现的关键标签；去掉了与 `speech-to-text` 重复的 `speech-recognition`，补上了 `wake-word`（唤醒词）、`homelab`（闲置设备/家庭实验室场景）。
