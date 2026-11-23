# 产出与材料 HTTP（18，形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

本类计入形状保留不冻 147（从而计入 238）。18 条为 artifacts 13 + task_assets 5。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/artifacts.py` 与 `AIOS2.0/backend/src/aios2/api/task_assets.py`

| 项 | 指针 |
|---|---|
| `GET /api/v1/phone/assets` | `api/artifacts.py` |
| `GET /api/v1/phone/assets/{output_id}` | 同上 |
| `DELETE /api/v1/phone/assets/{output_id}` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials/query` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials/keep-evidence` | 同上 |
| `GET /api/v1/artifacts/{experience}/materials/{entry_id}` | 同上 |
| `DELETE /api/v1/artifacts/{experience}/materials/{entry_id}` | 同上 |
| `POST /api/v1/artifacts/{experience}/outputs` | 同上 |
| `DELETE /api/v1/artifacts/{experience}/sharing` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/outputs` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/materials` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/materials/query` | 同上 |
| `GET /api/v1/phone/tasks` | `api/task_assets.py`，`@router.get("/api/v1/phone/tasks")` |
| `GET /api/v1/phone/tasks/deliveries` | `api/task_assets.py` |
| `GET /api/v1/phone/tasks/{task_id}` | `api/task_assets.py` |
| `GET /api/v1/phone/task-files/{item_id}` | `api/task_assets.py` |
| `DELETE /api/v1/phone/tasks/{task_id}` | `api/task_assets.py` |

与产出相关的固定工具（`submit_output`、`write_note` 等）见 [14-tool-registry.md](14-tool-registry.md)，那些余名不重复加进 238。
