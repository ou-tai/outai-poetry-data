# outai-poetry-data

OUTAI 诗词数据仓库：上游开源项目 [chinese-poetry](https://github.com/chinese-poetry/chinese-poetry) 数据的独立副本，供诗词阅读网站 https://s.outaidage.xyz 运行时读取。

- 上游仓库：https://github.com/chinese-poetry/chinese-poetry
- 上游分支：`master`
- 许可：MIT License，Copyright (c) 2016 JackeyGao，见 [LICENSE](LICENSE)
- 原始诗词内容不做修改，仅做同步；网站的搜索索引与派生数据在网站仓库 `ou-tai/outai-poetry` 中生成。

## 自动同步

`.github/workflows/sync.yml` 每天 02:00 UTC 自动检查上游更新：

- 有更新：同步数据目录与 LICENSE，更新 `SYNC_STATUS.md`，产生一次提交。
- 无更新：不产生提交。
- 同步失败：保留上一份可用数据，不覆盖。
- 支持在 GitHub Actions 页面手动触发（Run workflow）。
- 同步只覆盖下列数据目录与 LICENSE，不覆盖本仓库的 README、工作流与 `SYNC_STATUS.md`：全唐诗、宋词、诗经、楚辞、元曲、五代诗词、纳兰性德、论语、四书五经、蒙学、幽梦影、曹操诗集、御定全唐詩、水墨唐诗。

最近同步状态见 [SYNC_STATUS.md](SYNC_STATUS.md)。

## 网站如何读取

网站运行时从本仓库读取原始 JSON 分片，不直接请求上游仓库：

- CDN（优先）：`https://cdn.jsdelivr.net/gh/ou-tai/outai-poetry-data@main/<路径>`
- 回退：`https://raw.githubusercontent.com/ou-tai/outai-poetry-data/main/<路径>`

例如唐诗首个分片：`全唐诗/poet.tang.0.json`。
