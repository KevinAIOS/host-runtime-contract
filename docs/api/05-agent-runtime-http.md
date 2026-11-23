# Agent Runtime HTTP（27：24 拟冻结 + 3 形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本类总共 **27** 条（不是锁前旧约数 29），全部计入 238：其中 24 条计入拟冻结 91，3 条计入形状保留不冻 147。下面先列稳定面 24 条；后段 3 条单独标明**不承诺行为**。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py` 直接注册的装饰器
- 行号相对该提交的该文件原文

## 拟冻结（24）

| 项 | 指针 |
|---|---|
| `POST /api/v1/sessions` | `api/app.py:817` |
| `GET /api/v1/sessions` | `api/app.py:854` |
| `PATCH /api/v1/sessions/{session_id}` | `api/app.py:863` |
| `DELETE /api/v1/sessions/{session_id}` | `api/app.py:947` |
| `GET /api/v1/sessions/{session_id}` | `api/app.py:961` |
| `GET /api/v1/sessions/{session_id}/history` | `api/app.py:973` |
| `GET /api/v1/sessions/{session_id}/events` | `api/app.py:985` |
| `GET /api/v1/sessions/{session_id}/trace` | `api/app.py:1003` |
| `GET /api/v1/sessions/{session_id}/working-state` | `api/app.py:1021` |
| `POST /api/v1/sessions/{session_id}/runs` | `api/app.py:1030` |
| `GET /api/v1/session-groups` | `api/app.py:896` |
| `POST /api/v1/session-groups` | `api/app.py:903` |
| `PATCH /api/v1/session-groups/{group_id}` | `api/app.py:918`（路径在下一行） |
| `DELETE /api/v1/session-groups/{group_id}` | `api/app.py:933` |
| `GET /api/v1/runs/{run_id}` | `api/app.py:1151` |
| `POST /api/v1/runs/{run_id}/cancel` | `api/app.py:1160` |
| `GET /api/v1/runs/{run_id}/events` | `api/app.py:1169` |
| `GET /api/v1/activities/{activity_id}` | `api/app.py:1183` |
| `POST /api/v1/sessions/{session_id}/activities/{activity_id}/messages` | `api/app.py:1128` |
| `GET /api/v1/input-preparations/capabilities` | `api/app.py:1056` |
| `POST /api/v1/sessions/{session_id}/input-preparations` | `api/app.py:1069` |
| `DELETE /api/v1/sessions/{session_id}/input-preparations/{candidate_id}` | `api/app.py:1092` |
| `POST /api/v1/sessions/{session_id}/input-preparations/{candidate_id}/confirm` | `api/app.py:1106` |
| `GET /api/v1/capabilities` | `api/app.py:499` |

其中 activity messages 与 input-preparations 四条，与 [09-input-prep.md](09-input-prep.md) 的 Glass 认证入口是同一能力的两种入口，主合计只计本表一次。

## 形状保留不冻（3，不承诺行为）

这 3 条计入 147，不进稳定面。

| 项 | 指针 |
|---|---|
| `GET /api/v1/payload` | `api/app.py:1221` |
| `GET /api/v1/invocations/{invocation_id}/audit` | `api/app.py:1202` |
| `GET /api/v1/provider-profiles` | `api/app.py:588` |

`GET /api/v1/capabilities` 在稳定面中，对应的 7 个能力名见 [10-capabilities.md](10-capabilities.md)，能力名本身不与 238 相加。`GET /api/v1/provider-profiles` 由协议客户端的 `providers.list` 封装，该方法是形状保留，见 [17-runtime-client.md](17-runtime-client.md)。
