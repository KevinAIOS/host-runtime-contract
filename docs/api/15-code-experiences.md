# 代码型 Experience（HTTP 32 + Deno 52 + 处理槽 12，形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

本类计入形状保留不冻 147（从而计入 238）的是：**HTTP 32 + Hub 侧 Deno 平台方法 52 + 处理槽 12**。本类是 32 条 HTTP，不是锁前旧约数 4。动态 `code.*` 工具不计固定总数。

手机侧代码宿主在冻结点上点到的 35 个 session API 名只作为本页附录，**不与 52+12 合并，也不另加入 238**。尚未做逐项对照表，本页**不编造**对照表。

## HTTP（32）

源：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/code_experiences/api.py`。宿主桥前缀 `B = /api/v1/phone/perception/experiences/{slug}/code`。

| 项 | 指针 |
|---|---|
| `POST {B}/lifecycle/ack` | `code_experiences/api.py:205` |
| `POST {B}/tool-results` | `code_experiences/api.py:209` |
| `POST {B}/outputs` | `code_experiences/api.py:218` |
| `POST {B}/outputs/{output_ref}/receipt` | `code_experiences/api.py:235` |
| `POST {B}/preparations/{preparation_ref}/receipt` | `code_experiences/api.py:250` |
| `GET {B}/assets/{key}` | `code_experiences/api.py:258` |
| `PUT {B}/assets/{key}` | `code_experiences/api.py:263` |
| `POST {B}/images` | `code_experiences/api.py:269` |
| `GET {B}/images/{image_ref}` | `code_experiences/api.py:283` |
| `GET {B}/store/{key:path}` | `code_experiences/api.py:287` |
| `POST {B}/store/{key:path}/cas` | `code_experiences/api.py:291` |
| `GET {B}/store` | `code_experiences/api.py:296` |
| `PUT {B}/timers/{timer_id:path}` | `code_experiences/api.py:301` |
| `GET {B}/timers` | `code_experiences/api.py:306` |
| `POST {B}/timers/{timer_id:path}/pause` | `code_experiences/api.py:310` |
| `POST {B}/timers/{timer_id:path}/resume` | `code_experiences/api.py:314` |
| `POST {B}/timers/{timer_id:path}/fire` | `code_experiences/api.py:318` |
| `DELETE {B}/timers/{timer_id:path}` | `code_experiences/api.py:328` |
| `GET {B}/schedules` | `code_experiences/api.py:332` |
| `PUT {B}/schedules/{schedule_id}` | `code_experiences/api.py:336` |
| `POST {B}/net/fetch` | `code_experiences/api.py:341` |
| `POST {B}/agent/ask` | `code_experiences/api.py:346` |
| `POST {B}/agent/start` | `code_experiences/api.py:351` |
| `POST {B}/agent/send` | `code_experiences/api.py:355` |
| `POST {B}/agent/stop` | `code_experiences/api.py:359` |
| `POST {B}/peer` | `code_experiences/api.py:363` |
| `POST {B}/logs` | `code_experiences/api.py:367` |
| `POST {B}/health` | `code_experiences/api.py:377` |
| `GET /api/v1/phone/code/outbox` | `code_experiences/api.py:385` |
| `POST /api/v1/phone/code/outbox/{item_id}/receipt` | `code_experiences/api.py:391` |
| `GET /api/v1/developer/experiences/{slug}/code/logs` | `code_experiences/api.py:414` |
| `GET /api/v1/code/files/{token}` | `code_experiences/api.py:427` |

## Hub 侧 Deno 平台方法（52）与处理槽（12）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/code_experiences/deno_host.js` 的 `makeSession` 与 `HANDLERS`。这是服务端宿主注入给代码型 Experience 的平台面。标「server 上拒绝」的，在此宿主里是 `notOnServer` 桩，形状记下，不假装在 server 上已经能用。

这些处理槽与体验编写面里代码型处理槽名字相近，仍是**运行时宿主槽**，不得与已冻编写面词表合并或重冻。

在此宿主上可记下形状、且未标为 server 拒绝的方法：

- `now`
- `store.get`
- `store.cas`
- `store.list`
- `timers.schedule`
- `timers.cancel`
- `timers.pause`
- `timers.resume`
- `timers.get`
- `timers.list`
- `schedules.list`
- `schedules.set`
- `output.speak`
- `output.notify`
- `outputs.read`
- `outputs.write`
- `outputs.update`
- `materials.add`
- `materials.query`
- `materials.get`
- `materials.delete`
- `materials.keepEvidence`
- `images.get`
- `images.upload`
- `net.fetch`
- `agent.ask`
- `agent.start`
- `agent.send`
- `agent.stop`
- `peer.send`
- `files.write`
- `files.append`
- `files.list`
- `files.delete`
- `log.debug`
- `log.info`
- `log.warn`
- `log.error`
- `perception.frames`
- `perception.audio`

server 上拒绝（形状仍记下）：

- `camera.capture`
- `camera.status`
- `camera.cancel`
- `perception.subscribe`
- `perception.pause`
- `perception.resume`
- `perception.unsubscribe`
- `perception.list`
- `local.get`
- `local.set`
- `local.delete`
- `local.list`

处理槽 12 个（`HANDLERS` 键）：

- `onInstall`
- `onUpgrade`
- `onUninstall`
- `onMount`
- `onUnmount`
- `onSignal`
- `onSegment`
- `onUtterance`
- `onButton`
- `onTimer`
- `onSchedule`
- `onPeer`

以上 52 + 12 **计入 147**。

## 附录：手机侧 session API（35 个名字，不计 238）

指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`mobile/src/glass-host/code/code-api.ts` 的 `CodeApi` / `CAPABILITY`（以及同目录 `code-host.ts`、`types.ts`）。`aios/reality-runtime/reality-system/mobile-receipt/` 是收据／集成证据目录，不是另一份与 `code-api.ts` 并列的平台方法表。树中若有 Hub 侧 `deno_host.js` 的覆盖副本，不替代上面已锁定的 Hub 冻结点计数。

下列名字来自手机 `CAPABILITY` 表，共 35 个。只作形状说明，**不承诺行为**，不与 Hub 侧 52+12 相加，不改 238。本页不做逐项对照。

| 名字 | 备注 |
|---|---|
| `memory.remember`、`memory.search`、`memory.forget` | 留云调用类型（Memory），不是离线替代 |
| `store.get`、`store.cas`、`store.list` |  |
| `timers.schedule`、`timers.cancel`、`timers.pause`、`timers.resume`、`timers.get`、`timers.list` |  |
| `schedules.list`、`schedules.set` |  |
| `output.speak`、`output.notify` |  |
| `outputs.read`、`outputs.write` |  |
| `materials.add`、`materials.query`、`materials.get`、`materials.delete`、`materials.keepEvidence` |  |
| `images.upload`、`images.get` |  |
| `camera.capture`、`camera.status`、`camera.cancel` | 手机上有对应 `CodeCameraPort`，不是 Hub 侧那种拒绝桩 |
| `net.fetch` |  |
| `agent.ask`、`agent.start`、`agent.send`、`agent.stop` |  |
| `peer.send` |  |
| `log.write` |  |

先前说明曾举例的 `perception.subscribe`：**未**出现在上述手机 `CAPABILITY` 表里。它在 Hub 侧 `deno_host.js` 仍按已锁定叙述处理（server 上拒绝桩）。
