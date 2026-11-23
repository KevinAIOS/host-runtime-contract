# Reality 本地配套（4，拟冻结形状）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。只冻 Host 集成用的本地入口形状（loopback + bearer），不钉必须与今天同一进程或同一实现。与观测、订阅不是同一进程。

- 指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/reality-runtime/reality-system/server.mjs` 的 `createServer`

| 项 | 指针 |
|---|---|
| `GET /status` | `server.mjs` 中 `url.pathname === '/status'` |
| `PUT /subscriptions/{id}` | `server.mjs` 中 `PUT` 且路径以 `/subscriptions/` 开头 |
| `DELETE /subscriptions/{id}` | `server.mjs` 中 `DELETE` 且路径以 `/subscriptions/` 开头 |
| `WS /video` | `server.mjs` 中 `upgrade` 校验 `req.url === '/video'` |

路径按该文件中的本地服务根来理解，不是 Hub 上的 `/api/v1/reality`。
