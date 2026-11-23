# Host↔运行时能力名（7，拟冻结标识符）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

这 7 个名字是标识符，**不与 91、147 或 238 相加**，也不与协议客户端的 29 个方法相加。发现入口是 `GET /api/v1/capabilities`（见 [05-agent-runtime-http.md](05-agent-runtime-http.md)）以及协议客户端的 `capabilities` / `requireCapability`。

- 指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client/src/client.ts`（及类型导出 `aios/packages/runtime-client/src/types.ts`）中的能力名表
- 协议 `contract_version`：`d21.v1`；schema：`aios2.capabilities/v1`

| 项 | 指针 |
|---|---|
| `glass_live` | `aios/packages/runtime-client/src/client.ts` 的能力名表 |
| `experience_delegation` | 同上 |
| `trusted_mcp_metadata` | 同上 |
| `idempotent_activity_start` | 同上 |
| `typed_mcp_images` | 同上 |
| `user_output_classification` | 同上 |
| `agent_model_concurrency` | 同上 |

这 7 个名字不得与下列词表合并或重冻：设备契约的 CapabilityId、应用清单 `aios.json` 的 `APP_CAPABILITIES`、代码型 Experience 的 Capability。
