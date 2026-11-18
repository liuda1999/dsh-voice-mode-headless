# 内置上游发布包 / Vendored upstream

这个目录放的是上游 [dsh-voice-mode](https://github.com/qishuilalala/dsh-voice-mode) 的**固定版本发布包**，原样复制自 npm tarball，用于版本锁定、代码审阅与校验。

| 项 | 值 |
|---|---|
| 包名 | `dsh-voice-mode` |
| 版本 | **0.7.39** |
| 来源 | `https://registry.npmjs.org/dsh-voice-mode/-/dsh-voice-mode-0.7.39.tgz` |
| sha512 | `sha512-NjF6SrWi3lX0dwO/4guX1Qy+VWo0q/mRgEEJQK2cE6FQ5hYLZhPZasP8HrX67drvmJMPNyriiEbgzJ5Sz0OQsA==` |
| sha1 | `992b940932c6d013d05c5c662a646d4522f23c24` |
| git commit | `b2fa61b22a7e1559ddb50fd0265c2049bcb2610a` |
| 许可 | MIT，版权归 [@qishuilalala](https://github.com/qishuilalala) 所有 |
| 文件数 / 解包大小 | 21 / 1,428,484 bytes |

## 为什么内置

- **固定版本**：文档里的安装命令、`cordis.patch.yml` 条目、音色预设、`prefetch.mjs` 的 32 个模型文件校验，都是按这一版核对的；
- **可核对**：拿到仓库就能直接对照代码，不用去猜 npm 最新版改了什么；
- **不修改**：这里的内容与发布包逐字节一致，本仓库不对上游代码做任何改动。

## 怎么核对

```bash
# 自行重新下载同版本 tarball 后，比对校验值
curl -sSL https://registry.npmjs.org/dsh-voice-mode/-/dsh-voice-mode-0.7.39.tgz -o pkg.tgz
openssl dgst -sha512 -binary pkg.tgz | openssl base64 -A
# 结果应等于 PROVENANCE.json 里 integrity 去掉 "sha512-" 前缀后的值
```

也可以直接比对 `package.json` 的 `version` 字段和 `PROVENANCE.json`。

## 怎么升级

1. 下载新的 npm tarball，解包替换 `upstream/dsh-voice-mode-<新版本>/` 目录；
2. 更新 `PROVENANCE.json`（版本、sha512、sha1、gitHead、日期）；
3. 重新核对参考文档第 10.2 节九步与第 5 节的参数、音色、模型清单；
4. 更新 `references/upstream-lock.md` 与三份 README 的版本说明。

> 上游若发布 0.8.x 或引入破坏性变更，本仓库不保证自动跟随。需要最新代码请直接访问 [上游仓库](https://github.com/qishuilalala/dsh-voice-mode)。
