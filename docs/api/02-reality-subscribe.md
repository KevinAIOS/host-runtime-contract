# 订阅 HTTP（10，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。这是「后端订阅」一侧：按体验拥有者管理订阅、询问、片段结束与证据。与 [01-reality-observe.md](01-reality-observe.md) 同一源文件、同一前缀。

- 前缀：`/api/v1/reality`
- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/reality/api.py`

| 项 | 指针 |
|---|---|
| `GET /api/v1/reality/experiences/{owner}/subscriptions` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.get("/experiences/{owner}/subscriptions")` |
| `POST /api/v1/reality/experiences/{owner}/subscriptions` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post("/experiences/{owner}/subscriptions")` |
| `POST /api/v1/reality/experiences/{owner}/subscriptions/pause` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post(".../pause")` |
| `POST /api/v1/reality/experiences/{owner}/subscriptions/resume` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post(".../resume")` |
| `POST /api/v1/reality/experiences/{owner}/ask` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post("/experiences/{owner}/ask")` |
| `POST /api/v1/reality/experiences/{owner}/segments/done` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post(".../segments/done")` |
| `POST /api/v1/reality/experiences/{owner}/subscriptions/unsubscribe` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post(".../unsubscribe")` |
| `GET /api/v1/reality/experiences/{owner}/subscriptions/{subscription_id}` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.get(".../{subscription_id}")` |
| `POST /api/v1/reality/experiences/{owner}/evidence` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post(".../evidence")` |
| `POST /api/v1/reality/wake` | `AIOS2.0/backend/src/aios2/reality/api.py`：`@router.post("/wake")` |

旧说明里的「status」对应按 id 读取的那一条（表中 `GET .../subscriptions/{subscription_id}`），没有额外的 `GET .../status` 路由。
