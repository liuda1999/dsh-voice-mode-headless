# 上游版本锁定 / Upstream Lock

本技能对应并**仅保证兼容** `dsh-voice-mode` **v0.7.39**。

## 锁定信息

| 项 | 值 |
|---|---|
| 版本 | **0.7.39** |
| 发布源 | `https://registry.npmjs.org/dsh-voice-mode/-/dsh-voice-mode-0.7.39.tgz` |
| sha512 integrity | `sha512-NjF6SrWi3lX0dwO/4guX1Qy+VWo0q/mRgEEJQK2cE6FQ5hYLZhPZasP8HrX67drvmJMPNyriiEbgzJ5Sz0OQsA==` |
| sha1 shasum | `992b940932c6d013d05c5c662a646d4522f23c24` |
| git commit | `b2fa61b22a7e1559ddb50fd0265c2049bcb2610a` |
| 许可 | MIT（上游作者 [@qishuilalala](https://github.com/qishuilalala)） |
| 声明兼容 | `node >=18.0.0`、`dsh >=0.1.1-rc.2 <0.3.0-0` |
| 仓库内置位置 | `upstream/dsh-voice-mode-0.7.39/`（原样副本 + `PROVENANCE.json`） |

## 按 v0.7.39 核对过的兼容点

| 方案文档依赖的接口 | v0.7.39 核对结果 |
|---|---|
| `dsh plugin --profile web add dsh-voice-mode` | 包名未变；建议锁定为 `dsh-voice-mode@0.7.39` |
| `cordis.patch.yml` 提供 `voice-mode` 条目 | 仍为 `- insert: - id: voice-mode / name: dsh-voice-mode` |
| `wakeWord` / `autoResume` / `allowLan` 配置项 | 均在 `lib/index.js`、`lib/client.js` 中存在 |
| 5 个本地 VITS 音色预设 | suyingxue / gunian / fushiyu / bingjiao / bazong 均存在 |
| `scripts/prefetch.mjs` 与模型 SHA256 校验 | 存在；6 个模型仓库共 **32** 个文件，逐个带 SHA256 |
| `GET /voice-mode/config` 配置接口 | 仍由 voice-mode 提供 |
| 部署第 10.2 节九步 | 安装、模型预取、patch 挂载、配置键均未变 |

## 离线安装（备份路径）

上游关库或无法访问 npm 时，用仓库内置包直接安装（在仓库根目录执行）：

```bash
dsh plugin --profile web add ./upstream/dsh-voice-mode-0.7.39.tgz
# 解包目录方式：dsh plugin --profile web add ./upstream/dsh-voice-mode-0.7.39
```

本地目录必须在**上一级父目录**执行，否则会多套一层路径。安装依赖与模型预取仍需网络。

## 兼容边界（写进说明文档的口径）

- **仅保证与 v0.7.39 一致**：命令、参数、音色、模型清单都以这一版为准。
- 上游发布 **0.8.x 或更高**、或引入破坏性更新（改配置键名、换模型仓库、改 `cordis.patch.yml` 条目、改安装入口、改目录结构）后，方案文档中的命令与参数可能失效，**本技能不保证继续可用**。
- 需要使用最新上游代码，请前往 <https://github.com/qishuilalala/dsh-voice-mode> 或 npm 页面自行获取；升级后按上游 README 重新核对本方案第 10.2 节。

## 升级检查清单

1. 下载新版本 npm tarball，核对 `dist.integrity`；
2. 替换 `upstream/dsh-voice-mode-<新版本>/`，更新 `PROVENANCE.json`；
3. 逐项复核上表 7 个接口，确认没有破坏性变更；
4. 更新 `references/语音模式说明.md` 第 5、10、13 节与本文档版本号；
5. 同步 `SKILL.md` 与中英 README 的版本说明，重新打包技能。
