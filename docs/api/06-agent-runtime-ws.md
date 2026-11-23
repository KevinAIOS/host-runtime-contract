# Agent Runtime 会话套接字（2，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。计入的是 **2 个端点**。流上每种 `event_type` **不按接口另计**，也不得写成一个已冻整数或「共 N 种事件」。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py`
- 行号相对该提交的该文件原文

| 项 | 指针 |
|---|---|
| `WS /api/v1/sessions/{session_id}/stream` | `AIOS2.0/backend/src/aios2/api/app.py:1298` |
| `WS /api/v1/sessions/{session_id}/activities/{activity_id}/voice` | `AIOS2.0/backend/src/aios2/api/app.py:1238` |

## 已点到的 `event_type` 字面量（不是完整目录）

客户端里 `event_type` 是字符串，不是封闭枚举。公开事件按 `visibility == "public"` 转发。对照冻结点源文件后，只列出已经见到的字面量；**完整目录仍是缺口**。

在冻结点上确认的**事件类型**字面量（`event.event_type`）：

- 转发里直接比较：`user.message`、`assistant.user_output`、`assistant.user_output.completed`
- 转发里按前缀：以 `tool.approval.` 开头的类型（不是一张封闭清单）
- 客户端正式输出处理（契约已列出，本目录复核仍在这些字面量上）：`assistant.final`、`assistant.user_output`，以及 `assistant.user_output.` 之后的 `started`、`delta`、`completed`、`cancelled`、`failed`

指针：Hub `AIOS2.0/backend/src/aios2/api/app.py` 的会话流 `forward_live` @ `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；Host `@aios/runtime-client` 的 `src/events.ts`、`src/types.ts`、`src/stream.ts` @ `d5a93a371b3d825b87771ab517c435551948a547`（`toFormalOutput` 等）。

见到、但**不宜一律当成 `event_type` 目录**的套接字消息或命令字面量：`tool.approval.snapshot`、`tool.approval.decide`、`tool.approval.decision.accepted`，以及 `app.py` 中出现的若干 `session.*` / `run.*` / `agent.activity.*` 命令或回执名。它们可以按「命令／回执」另述，不并进事件种类总数——本批也**不发明**这样一个总数。
