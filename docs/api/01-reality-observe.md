# Reality 观测 HTTP（8，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。这是「前端现实」一侧的观测入口：Host 或运行时向现实面提交或读取信号、同步与感知状态。与 [02-reality-subscribe.md](02-reality-subscribe.md) 同一前缀、同一源文件，但订阅是另一类。

- 前缀：`/api/v1/reality`
- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/reality/api.py`

| 项 | 指针 |
|---|---|
| `POST /api/v1/reality/signals` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.post("/signals")` |
| `GET /api/v1/reality/signals/{signal}` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.get("/signals/{signal}")` |
| `POST /api/v1/reality/translate` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.post("/translate")` |
| `POST /api/v1/reality/sync` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.post("/sync")` |
| `GET /api/v1/reality/stats` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.get("/stats")` |
| `GET /api/v1/reality/events` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.get("/events")` |
| `GET /api/v1/reality/perception` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.get("/perception")` |
| `POST /api/v1/reality/perception/start` | `AIOS2.0/backend/src/aios2/reality/api.py`：reality/api.py，`@router.post("/perception/start")` |

本页不钉内部模块表或进程切分。与 [04-local-perception.md](04-local-perception.md) 的本地配套不是同一进程，不得写成「日用 Hub 上又开一套」。
