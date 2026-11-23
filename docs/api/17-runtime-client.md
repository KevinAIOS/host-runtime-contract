# `@aios/runtime-client`（只计作一类，方法不与 238 相加）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


这是 Host 连接运行时的协议客户端，不是给开发者写 Experience 的 SDK。本切版不开放该包源码、不发 npm。方法数**不与 238 相加**，也不是锁前旧约数 30。

- 包：`@aios/runtime-client` `0.1.0-d21.1`
- 源目录：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client`
- 主要源文件：`src/client.ts`、`src/stream.ts`、`src/input-preparation.ts`、`src/events.ts`、`src/types.ts`、`src/input-overlap.ts`、`src/stable-prefix.ts`

## `RuntimeClient` 公开方法 29

分组：sessions 8、runs 4、activities 1、experiences 10（其中 7 个留云、3 个拟冻结）、providers 1、approvals 2，加上根方法 `capabilities`、`requireCapability`、`connect`。没有第 30 个方法。

| 分组 | 方法 | 桶 | 说明 |
|---|---|---|---|
| sessions（8） | `list`、`create`、`get`、`history`、`events`、`update`、`delete`、`workingState` | 拟冻结 | 封装会话 HTTP，不重复计入 238 |
| runs（4） | `submit`、`get`、`cancel`、`events` | 拟冻结 | 同上 |
| activities（1） | `get` | 拟冻结 | 同上 |
| experiences（3） | `delegation`、`setDelegation`、`operation` | 拟冻结 | 打到 `/api/v1/glass/*`，对应 [07-experience-host.md](07-experience-host.md) |
| providers（1） | `list` | 形状保留不冻，**不承诺行为** | 对应 `/provider-profiles` |
| approvals（2） | `mcpInputs`、`respondMcpInput` | 形状保留不冻，**不承诺行为** | 对应 MCP input-requests |
| 根方法（3） | `capabilities`、`requireCapability`、`connect` | 拟冻结 | 能力发现与会话流连接 |

拟冻结 19 + 形状保留不冻 3 = 22 个可在本页公开方法表展开的项。另外 7 个市场方法是留云调用类型，**不列入公开 API**，只在 [18-cloud-only.md](18-cloud-only.md) 标明边界：`experiences.catalog`、`installed`、`config`、`install`、`setEnabled`、`checkUpdate`、`uninstall`（打到 `/api/v1/platform/*`）。合计 29。

## `RuntimeSessionStream`（拟冻结，不与 238 或 29 相加）

指针：`aios/packages/runtime-client/src/stream.ts` @ `d5a93a371b3d825b87771ab517c435551948a547`。

公开方法／取值：`afterSequence`、`isClosed`、`ready`、`close`、`resume`、`snapshot`、`putImage`、`startActivity`、`messageActivity`、`reattachActivity`、`putVisual`、`putAudio`、`decideApproval`、`stopActivity`、`endSource`（13 个方法加 2 个取值器）。

## `RuntimeInputCandidateTransport`（5，拟冻结，不与 238 或 29 相加）

指针：`aios/packages/runtime-client/src/input-preparation.ts` @ `d5a93a371b3d825b87771ab517c435551948a547`。

`loadCapabilities`、`whenPreparationIdle`、`prepare`、`cancel`、`confirm`。请求打到会话侧 input-preparations 入口，见 [05-agent-runtime-http.md](05-agent-runtime-http.md) 与 [09-input-prep.md](09-input-prep.md)。

## 事件与输入辅助（不与 238 或 29 相加）

- 拟冻结的已点形状：`isRuntimeEvent`、`toFormalOutput`（`src/events.ts`）；正式输出形状见 [06-agent-runtime-ws.md](06-agent-runtime-ws.md)。`toOutputInterrupt` 随 Attention 打断形状，拟冻结（注意：它不是包根上的导出，宿主若要使用需按该模块路径引用）。
- 形状保留不冻（Host 客户端辅助，不是第三条 Hub 线协议，**不承诺行为**）：`inputFingerprint`；`InputOverlapCoordinator` 的 `begin`、`setCapabilities`、`snapshot`、`partial`、`endpoint`、`anticipation`、`offerHypothesis`、`final`、`cancel`（`src/input-overlap.ts`）；`StablePrefixTracker` 的 `begin`、`observe`、`final`、`cancel`（`src/stable-prefix.ts`）。以及这两个模块导出的阈值常量和类型。
