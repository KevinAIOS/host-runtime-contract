# 输入预备（5，拟冻结；与会话 HTTP 去重）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类必须出席，但这 5 条与 [05-agent-runtime-http.md](05-agent-runtime-http.md) 中的会话 `input-preparations`／activity messages 是同一能力的 Glass 认证入口。形状一并冻结，**主合计只计会话那一组，本页不把 5 再加进 91**。

- 路由器前缀：`/api/v1/glass`
- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/input_preparation.py`

| 项 | 指针 |
|---|---|
| `GET /api/v1/glass/input-preparations/capabilities` | `api/input_preparation.py`，`@router.get("/input-preparations/capabilities")` |
| `POST /api/v1/glass/sessions/{session_id}/input-preparations` | 同文件，`@router.post("/sessions/{session_id}/input-preparations")` |
| `DELETE /api/v1/glass/sessions/{session_id}/input-preparations/{candidate_id}` | 同文件，`@router.delete` 该路径 |
| `POST /api/v1/glass/sessions/{session_id}/input-preparations/{candidate_id}/confirm` | 同文件，`@router.post` 该路径 |
| `POST /api/v1/glass/sessions/{session_id}/activities/{activity_id}/messages` | 同文件，activity messages 入口 |

协议客户端的 `RuntimeInputCandidateTransport`（`loadCapabilities`、`whenPreparationIdle`、`prepare`、`cancel`、`confirm`）封装会话侧入口，拟冻结，不与 238 或 29 相加，见 [17-runtime-client.md](17-runtime-client.md)。
