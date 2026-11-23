# 注意力路由（7，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。冻的是打断形状。

- 前缀：`/api/v1/attention`
- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/attention/gate/routes.py`

| 项 | 指针 |
|---|---|
| `GET /api/v1/attention/held` | `attention/gate/routes.py`，`@router.get("/held")` |
| `GET /api/v1/attention/results/{output_ref}` | 同文件，`@router.get("/results/{output_ref}")` |
| `POST /api/v1/attention/feedback` | 同文件，`@router.post("/feedback")` |
| `POST /api/v1/attention/check` | 同文件，`@router.post("/check")` |
| `GET /api/v1/attention/settings` | 同文件，`@router.get("/settings")` |
| `PUT /api/v1/attention/settings` | 同文件，`@router.put("/settings")` |
| `PUT /api/v1/attention/signals` | 同文件，`@router.put("/signals")` |

协议客户端的 `toOutputInterrupt` 随本类打断形状，拟冻结，本身不计进 29 或 238，见 [17-runtime-client.md](17-runtime-client.md)。

手机侧另有 `GET /api/v1/phone/interrupt/held`、`POST /api/v1/phone/interrupt/feedback`，已锁定为形状保留不冻，但**不属于** 147，也不在本页清单里。见 [20-not-in-this-release.md](20-not-in-this-release.md)。
