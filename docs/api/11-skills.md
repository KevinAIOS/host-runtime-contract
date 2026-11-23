# Skills HTTP（8，形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

本类计入形状保留不冻 147（从而计入 238）。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py`

| 项 | 指针 |
|---|---|
| `GET /api/v1/skills` | `api/app.py:597` |
| `POST /api/v1/skills/install` | `api/app.py:601` |
| `POST /api/v1/skills/search` | `api/app.py:612` |
| `POST /api/v1/skills/inspect` | `api/app.py:625` |
| `POST /api/v1/skills/{name}/check-updates` | `api/app.py:639` |
| `POST /api/v1/skills/{name}/update` | `api/app.py:648` |
| `POST /api/v1/skills/{name}/enabled` | `api/app.py:657` |
| `DELETE /api/v1/skills/{name}` | `api/app.py:666` |

与 Skills 相关的固定工具（`load_skill`、`find_skills` 等）见 [14-tool-registry.md](14-tool-registry.md)，那些余名不重复加进 238。
