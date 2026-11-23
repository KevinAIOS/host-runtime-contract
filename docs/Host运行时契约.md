# Host↔运行时契约

契约版本：**v0.1.0**（本契约自己的版本号，不是仓库标签，也不是 npm 包版本，也不是已公开的设备契约或体验编写面契约的 `v0.1.0`）。
日期：2026-11-23，America/New_York（ET，UTC-5）。

这份文档是 Host 与运行时之间的契约，已定稿并作为文档发布在本仓库 https://github.com/KevinAIOS/host-runtime-contract 。本仓库只公开契约文档，不开放运行时或 Host 实现，也不发布 `@aios/runtime-client` 包。许可为 [Apache-2.0](../LICENSE)。

冻结集：16 类去重主合计 **238**（拟冻结 **91** + 形状保留不冻 **147**）。另 **7** 个 Host↔运行时能力名拟冻结，不与 238 相加。`@aios/runtime-client` 只计类；`RuntimeClient` 公开方法 **29**（不是旧登记 30），方法不与 Hub HTTP/WebSocket 或 238 相加。

冻结点（源码仍在私有仓；本仓只公开契约文档，不改变那两座仓的许可或可见性）：
- 私有 `KevinAIOS/AIOSGlass` 分支 `codex/kele-20261103`，提交 `d5a93a371b3d825b87771ab517c435551948a547`（协议客户端、Reality 本地配套、Host 侧载源码）。
- 私有 `KevinAIOS/AIOS-new-` 分支 `codex/ruanruan-20261024`，提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`（Hub 路由与工具）。该工作分支尖端与此提交相同；默认分支 `main` 更旧，冻结点未改。

下文指针写「仓 / 提交 / 路径 / 符号」。Hub 路径相对 `AIOS2.0/backend/src/aios2/`。两条 Experience 编写路径称为「会话处理」和「代码型 Experience」。若对照公开／留云分层，用语是「始终留云 / 首版可开 / 后续可开代码 / 整仓不开放」。

不把体验编写面已冻结的 401 项写入本稳定面。第一切版已对照冻结点完成分类盘点，每一拟冻项都有源码或类型指针，并用协议客户端类型做过真实类型检查。尚未做真机验证，未连接生产或测试 Hub，未做系统级端到端（Host 启动 Experience 并收到订阅叫醒），未编 Native，未发 npm。不得把类型检查或纸面说明写成已跑通端到端。

## 1. 这份契约钉什么

本契约钉的是 Host 和运行时怎么配合，保住「前端现实、后端订阅」：Host 持有现实世界的信号与轨迹，运行时订阅并被叫醒，而不是由运行时自己占有传感器。出现在稳定面里，只保证**交互形状**被冻结，不保证今天必须是某两套运行时实现，也不钉内部模块表、目录名或进程切分。Reality 本地配套与 Hub 不是同一进程，不得读成「日用 Hub 上又开一套」。

本契约不是设备契约（Host↔眼镜），不是体验编写面契约（开发者怎么写会话处理或代码型 Experience），也不是把约 16 类第二批 API 的细则一次全部定死。第二批中未进稳定面的类，只保留形状、本份不承诺行为。对外第二批 API 文档、开放运行时／HAL／Host 代码，均须另行授权。本仓库只公开契约文档。

出现在稳定面里，不保证每一台 Host、每一套运行时部署都已经实现全部细节，也不保证云侧服务已经开通。能力名出现在这里，冻的是 Host 向运行时声明与要求的标识符，不冻「已经授权」或「该部署已实现」。

## 2. 版本约定

| 名称 | 本契约 v0.1.0 对应的值 | 说明 |
|---|---|---|
| 本契约版本 | v0.1.0 | 独立版本号。破坏性改动（删改已冻名字、路径形状或语义）必须升本契约版本，不得在 v0.1.0 名下偷改。 |
| Hub 冻结点 | `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615` | 本契约对照的运行时 HTTP／WebSocket／工具注册点。 |
| Host／协议客户端冻结点 | `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547` | 本契约对照的 `@aios/runtime-client`、本地配套与 Host 侧源码。 |
| `@aios/runtime-client` 包版本 | `0.1.0-d21.1`（该提交 `package.json`） | 这是协议客户端包版本，不是本契约版本，也不是 `@aios-glass/*` 的包版本。 |
| 协议 `contract_version` | `d21.v1`（schema `aios2.capabilities/v1`） | Host↔运行时能力发现用的协议版本名，与本契约 v0.1.0 分开记。 |
| 已公开设备契约 | https://github.com/KevinAIOS/glass-contract ，公开标签 `v0.1.0` | **不是**本契约。本契约不重冻那一份。 |
| 已公开体验编写面 | https://github.com/KevinAIOS/glass-sdk 的 `docs/体验编写面契约.md`，提交 `4cfb583`；仓库标签 `v0.1.0` 是 SDK 快照标签 | 体验编写面契约自己的版本也是 v0.1.0，与本契约只是号相同，不是同一份。不要把那 401 项写进本稳定面。 |
| `@aios-glass/*` 或现用 `@aios/glass`、`@aios/glass-cli` 包版本 | 与本契约无对应关系 | 那是编写面 SDK／CLI 的包版本（如 0.5.0 / 0.2.0）。本切版不发 npm，也不用本契约去改那些包版本。 |
| 本仓库与 git 标签 | 本仓库 https://github.com/KevinAIOS/host-runtime-contract ；若打标签，使用 `contract-v0.1.0`，不要只用 `v0.1.0` | 本契约版本仍是 v0.1.0。标签 `contract-v0.1.0` 只是本仓库对本契约版本的标注，与 [glass-contract](https://github.com/KevinAIOS/glass-contract) / [glass-sdk](https://github.com/KevinAIOS/glass-sdk) 的标签或契约 `v0.1.0`、以及 `@aios/glass` 0.5.0 / `@aios/glass-cli` 0.2.0 都不是同一份。不要只用 `v0.1.0` 当本仓标签。 |

## 3. 与已公开契约的边界，以及四套词表

- https://github.com/KevinAIOS/glass-contract 钉的是 Host 和眼镜怎么说话（75 个操作：50 条命令 + 25 个事件，另有设备侧 CapabilityId 17、PermissionId 12、ErrorCode 17）。本契约不重冻、不改写那一份。
- https://github.com/KevinAIOS/glass-sdk 的体验编写面契约钉的是开发者怎么写 Experience（会话处理与代码型 Experience）。本契约不重冻、不把那 401 项再列进来。
- 私有 `KevinAIOS/AIOSGlass` 与 `KevinAIOS/AIOS-new-` 仍是真源；生产网关 `aios/gateway/` 属整仓不开放。本仓库的公开不改变其许可或可见性。
- 不把执行脑、两个大脑、Harness 做成与本契约并列的公开标准。Harness 无对外接口，不算一类可公布 API。

### 四套词表，不要合并

名字相像也不得当成同一个标识符。本份契约只冻第四套。

| 词表 | 归属 | 本契约处置 | 例子 |
|---|---|---|---|
| 设备契约 `CapabilityId` / `PermissionId` | 已公开 glass-contract | 明确不进，不重冻 | 设备侧有自己的能力与权限枚举 |
| 体验编写面 `APP_CAPABILITIES` / `APP_PERMISSIONS` | 已公开体验契约（`aios.json`） | 明确不进，不重冻 | 应用清单声明 |
| 代码型 `Capability` | 已公开体验契约 | 明确不进，不重冻 | 如代码型 `store`、`perception.frames` |
| Host↔运行时能力声明 | 本契约 | 7 个名字拟冻结，不与 238 相加 | `requireCapability('glass_live')` 与上面三套不是同一个标识符 |

## 4. 稳定面（拟冻结 91）

下列 91 项是已锁定的拟冻结集，属于 16 类去重主合计中的拟冻结部分。每一项都给出源码或类型指针。完整名单即下面拟冻结 91 项。

另外 7 个能力名、输入预备的 Glass 认证入口（与第 4.5 节去重）、以及协议客户端上的拟冻结封装，写在第 4.9–4.11 节和第 8 节，**不另加进 91**。会话流上的 `event_type` 不按接口另计，见第 4.6 节与第 9 节。

冻的是交互形状。细则对外公布、第二批 API 文档，须另行授权。

### 4.1 Reality 观测（8）

前缀 `/api/v1/reality`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/reality/api.py`。
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

### 4.2 订阅（10）

同一文件、同一前缀。旧说明里的「status」即按 id 读取的那一条，没有额外的 `GET .../status`。

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

### 4.3 观察器／Glass 信号摄入（24）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/glass_signals.py`。含盘点时补计的 10 条按体验挂载路由。冻的是边界形状，细则可后段再写。

| 项 | 指针 |
|---|---|
| `POST /api/v1/glass/signals/sources` | `api/glass_signals.py:223`，`@router.post` |
| `POST /api/v1/glass/signals` | `api/glass_signals.py:230` |
| `DELETE /api/v1/glass/signals/sources/{lease_id}` | `api/glass_signals.py:237` |
| `GET /api/v1/phone/perception/source` | `api/glass_signals.py:245` |
| `GET /api/v1/phone/perception/events` | `api/glass_signals.py:375` |
| `GET /api/v1/phone/perception/layer2` | `api/glass_signals.py:418` |
| `POST /api/v1/phone/perception/layer2/submit` | `api/glass_signals.py:425` |
| `POST /api/v1/phone/perception/camera` | `api/glass_signals.py:505` |
| `POST /api/v1/phone/perception/start` | `api/glass_signals.py:515` |
| `GET /api/v1/phone/addressing/names` | `api/glass_signals.py:446` |
| `POST /api/v1/phone/utterances` | `api/glass_signals.py:450` |
| `POST /api/v1/phone/transcripts` | `api/glass_signals.py:455` |
| `POST /api/v1/phone/addressing/outputs` | `api/glass_signals.py:490` |
| `PUT /api/v1/phone/addressing/assistant` | `api/glass_signals.py:498` |
| `PUT /api/v1/phone/perception/experiences/{slug}/mount` | `api/glass_signals.py:252`（`base + "/mount"`） |
| `DELETE /api/v1/phone/perception/experiences/{slug}/mount` | `api/glass_signals.py:291` |
| `POST /api/v1/phone/perception/experiences/{slug}/runs` | `api/glass_signals.py:308` |
| `DELETE /api/v1/phone/perception/experiences/{slug}/runs/{run_id}` | `api/glass_signals.py:319` |
| `POST /api/v1/phone/perception/experiences/{slug}/subscriptions` | `api/glass_signals.py:328` |
| `GET /api/v1/phone/perception/experiences/{slug}/subscriptions` | `api/glass_signals.py:345` |
| `GET /api/v1/phone/perception/experiences/{slug}/subscriptions/{subscription_id}` | `api/glass_signals.py:351` |
| `POST /api/v1/phone/perception/experiences/{slug}/subscriptions/{subscription_id}/pause` | `api/glass_signals.py:357` |
| `POST /api/v1/phone/perception/experiences/{slug}/subscriptions/{subscription_id}/resume` | `api/glass_signals.py:363` |
| `DELETE /api/v1/phone/perception/experiences/{slug}/subscriptions/{subscription_id}` | `api/glass_signals.py:369` |

行号相对该提交的 `api/glass_signals.py` 原文。

### 4.4 Reality 本地配套（4）

指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/reality-runtime/reality-system/server.mjs` 的 `createServer`。只冻 Host 集成用的本地入口形状（loopback + bearer），不钉必须与今天同一进程或同一实现。与第 4.1–4.2 节不是同一进程。

| 项 | 指针 |
|---|---|
| `GET /status` | `server.mjs` 中 `url.pathname === '/status'` |
| `PUT /subscriptions/{id}` | `server.mjs` 中 `PUT` 且路径以 `/subscriptions/` 开头 |
| `DELETE /subscriptions/{id}` | `server.mjs` 中 `DELETE` 且路径以 `/subscriptions/` 开头 |
| `WS /video` | `server.mjs` 中 `upgrade` 校验 `req.url === '/video'` |

### 4.5 Agent Runtime HTTP（拟冻结 24；本类共 27，另 3 条见第 5.2 节）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py` 直接注册的装饰器。本类总共 27 条（不是旧约数 29）；计入 91 的是下面 24 条。

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

行号相对该提交的 `api/app.py` 原文。其中 messages 与 input-preparations 四条，与第 4.9 节是同一能力的两种认证入口，主合计只计本表一次。

### 4.6 Agent Runtime WebSocket（2）

| 项 | 指针 |
|---|---|
| `WS /api/v1/sessions/{session_id}/stream` | `AIOS2.0/backend/src/aios2/api/app.py:1298` |
| `WS /api/v1/sessions/{session_id}/activities/{activity_id}/voice` | `AIOS2.0/backend/src/aios2/api/app.py:1238` |

流上每种 `event_type` **不按接口另计**，也不得写成一个已冻整数。完整目录尚未点完，见第 9 节。

本契约对已经点到的正式输出形状作形状说明（不另计接口）：`assistant.final`、`assistant.user_output`、`assistant.user_output.started`、`.delta`、`.completed`、`.cancelled`、`.failed`。指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client/src/events.ts` 的 `toFormalOutput`。流转发里还出现 `user.message`、`tool.approval.*` 与 `tool.approval.snapshot`（`api/app.py` 会话流转发），不足以为完整清单。

### 4.7 Experience 安装启停（12）

市场安装（平台 `/products/{id}/install` 等）属始终留云，不在这 12 条里，见第 7 节。

Glass 入口，前缀 `/api/v1/glass`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/glass.py`。

| 项 | 指针 |
|---|---|
| `POST /api/v1/glass/calls/validate` | `api/glass.py:207` |
| `GET /api/v1/glass/experiences` | `api/glass.py:241` |
| `POST /api/v1/glass/experiences/query` | `api/glass.py:245` |
| `PUT /api/v1/glass/experiences/{product_id}/delegation` | `api/glass.py:252` |
| `GET /api/v1/glass/operations/{request_id}` | `api/glass.py:276` |
| `POST /api/v1/glass/experiences/start` | `api/glass.py:284` |

手机 experiences，前缀 `/api/v1/phone`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/phone/router.py`。

| 项 | 指针 |
|---|---|
| `GET /api/v1/phone/experiences` | `phone/router.py:297` |
| `GET /api/v1/phone/experiences/{slug}` | `phone/router.py:302` |
| `POST /api/v1/phone/experiences/{slug}/output-fallback` | `phone/router.py:358` |
| `POST /api/v1/phone/experiences/{slug}/enabled` | `phone/router.py:396` |
| `POST /api/v1/phone/experiences/{slug}/stop` | `phone/router.py:423` |
| `POST /api/v1/phone/experiences/{slug}/uninstall` | `phone/router.py:447` |

### 4.8 Attention（7）

前缀 `/api/v1/attention`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/attention/gate/routes.py`。冻的是打断形状。

| 项 | 指针 |
|---|---|
| `GET /api/v1/attention/held` | `attention/gate/routes.py`，`@router.get("/held")` |
| `GET /api/v1/attention/results/{output_ref}` | 同文件，`@router.get("/results/{output_ref}")` |
| `POST /api/v1/attention/feedback` | 同文件，`@router.post("/feedback")` |
| `POST /api/v1/attention/check` | 同文件，`@router.post("/check")` |
| `GET /api/v1/attention/settings` | 同文件，`@router.get("/settings")` |
| `PUT /api/v1/attention/settings` | 同文件，`@router.put("/settings")` |
| `PUT /api/v1/attention/signals` | 同文件，`@router.put("/signals")` |

### 4.9 输入预备的 Glass 认证入口（5，与第 4.5 节去重，不另计 91）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/input_preparation.py`，路由器前缀 `/api/v1/glass`。这是与第 4.5 节会话 `input-preparations`／activity messages 同一能力的 Glass 认证入口。形状一并冻结，主合计只计第 4.5 节那一组。

| 项 | 指针 |
|---|---|
| `GET /api/v1/glass/input-preparations/capabilities` | `api/input_preparation.py`，`@router.get("/input-preparations/capabilities")` |
| `POST /api/v1/glass/sessions/{session_id}/input-preparations` | 同文件，`@router.post("/sessions/{session_id}/input-preparations")` |
| `DELETE /api/v1/glass/sessions/{session_id}/input-preparations/{candidate_id}` | 同文件，`@router.delete` 该路径 |
| `POST /api/v1/glass/sessions/{session_id}/input-preparations/{candidate_id}/confirm` | 同文件，`@router.post` 该路径 |
| `POST /api/v1/glass/sessions/{session_id}/activities/{activity_id}/messages` | 同文件，activity messages 入口 |

### 4.10 Host↔运行时能力名（7，拟冻结标识符，不与 91 或 238 相加）

指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client/src/client.ts`（及类型导出 `aios/packages/runtime-client/src/types.ts`）中的能力名表。协议 `contract_version` 为 `d21.v1`，schema 为 `aios2.capabilities/v1`。发现入口是第 4.5 节的 `GET /api/v1/capabilities` 与协议客户端的 `capabilities` / `requireCapability`。

| 项 | 指针 |
|---|---|
| `glass_live` | `aios/packages/runtime-client/src/client.ts` 的能力名表 |
| `experience_delegation` | 同上 |
| `trusted_mcp_metadata` | 同上 |
| `idempotent_activity_start` | 同上 |
| `typed_mcp_images` | 同上 |
| `user_output_classification` | 同上 |
| `agent_model_concurrency` | 同上 |

这 7 个名字不得与设备契约 CapabilityId、应用清单 `APP_CAPABILITIES` 或代码型 `Capability` 合并。

### 4.11 稳定面小结

计入 91 的构成：观测 8 + 订阅 10 + 观察器 24 + 本地配套 4 + Agent Runtime HTTP 24 + WebSocket 2 + Experience 安装启停 12 + Attention 7 = **91**。与已锁定盘点表第 2.1 节一致。

## 5. 形状保留但不承诺行为（147）

下列 147 项已锁定为「形状保留不冻」：形状先记下，本份契约不承诺行为，也不在 v0.1.0 稳定面里保证。第二批 API 文档若要对外公布，须另行授权。完整名单即下面形状保留不冻 147 项。

### 5.1 感知系统工具（5）

仅系统感知 Agent 可调。不把「感知管线可被单独替换」写成第三份契约（那是总计划第 6 步，现不定、不开）。这 5 个也出现在 ToolRegistry 装配里，主合计只在本类计一次。

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/reality/perception.py` 的 `TOOL_NAMES` / `DEFINITIONS`，以及 `AIOS2.0/backend/src/aios2/reality/segment_tools.py` 的 `DONE_DEFINITION`。

| 项 | 指针 |
|---|---|
| `emit_event`（`reality.emit_event@1`） | `reality/perception.py` 的 `DEFINITIONS` |
| `wake`（`reality.wake@1`） | 同上 |
| `look_closer`（`reality.look_closer@1`） | 同上 |
| `fast_judge`（`reality.fast_judge@1`） | 同上 |
| `segment_done`（`reality.segment_done@1`） | `reality/segment_tools.py` 的 `DONE_DEFINITION` |

### 5.2 Agent Runtime HTTP 中不进稳定面的 3 条

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py`。

| 项 | 指针 |
|---|---|
| `GET /api/v1/payload` | `api/app.py:1221` |
| `GET /api/v1/invocations/{invocation_id}/audit` | `api/app.py:1202` |
| `GET /api/v1/provider-profiles` | `api/app.py:588` |

### 5.3 Skills（8）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py`。

| 项 | 指针 |
|---|---|
| `GET /api/v1/skills` | `api/app.py:597` |
| `POST /api/v1/skills/install` | `api/app.py:601` |
| `POST /api/v1/skills/search` | `api/app.py:612` |
| `POST /api/v1/skills/inspect` | `api/app.py:625` |
| `POST /api/v1/skills/{name}/check-updates` | `api/app.py:639` |
| `POST /api/v1/skills/{name}/update` | `api/app.py:648` |
| `POST /api/v1/skills/{name}/enabled` | `api/app.py:657` |
| `DELETE /api/v1/skills/{name}` | `api/app.py:666` |

### 5.4 MCP 管理 HTTP（12）与元工具（5）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py` 与 `AIOS2.0/backend/src/aios2/tools/mcp_platform.py`。生产网关实现不在本类计入，见第 6、9 节。

| 项 | 指针 |
|---|---|
| `GET /api/v1/mcp` | `api/app.py:676` |
| `POST /api/v1/mcp/servers` | `api/app.py:680` |
| `POST /api/v1/mcp/servers/{server_id}/confirm` | `api/app.py:687` |
| `POST /api/v1/mcp/servers/{server_id}/sync` | `api/app.py:698` |
| `POST /api/v1/mcp/servers/{server_id}/enabled` | `api/app.py:709` |
| `POST /api/v1/mcp/servers/{server_id}/tools/{tool_name}/policy` | `api/app.py:718` |
| `DELETE /api/v1/mcp/servers/{server_id}` | `api/app.py:727` |
| `GET /api/v1/mcp/input-requests` | `api/app.py:735` |
| `POST /api/v1/mcp/resources/read` | `api/app.py:744` |
| `POST /api/v1/mcp/prompts/render` | `api/app.py:758` |
| `POST /api/v1/mcp/prompts/apply` | `api/app.py:772` |
| `POST /api/v1/mcp/input-requests/{request_id}/respond` | `api/app.py:786` |
| `search_tools`（`mcp.search_tools@1`） | `tools/mcp_platform.py` 的 `ToolDefinition` |
| `search_resources`（`mcp.search_resources@1`） | 同上 |
| `read_resource`（`mcp.read_resource@1`） | 同上 |
| `search_prompts`（`mcp.search_prompts@1`） | 同上 |
| `use_prompt`（`mcp.use_prompt@1`） | 同上 |

外部 `mcp__{server}__{name}` 数量随配置变化，不计固定总数，也不在这 147 里。

### 5.5 `code_experiences` HTTP（32）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/code_experiences/api.py`。`B = /api/v1/phone/perception/experiences/{slug}/code`。本类 HTTP 是 32 条，不是旧登记的「HTTP 4」。`code.*` 工具动态，不计固定总数。

宿主桥 28 条：

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

外围 4 条：

| 项 | 指针 |
|---|---|
| `GET /api/v1/phone/code/outbox` | `code_experiences/api.py:385` |
| `POST /api/v1/phone/code/outbox/{item_id}/receipt` | `code_experiences/api.py:391` |
| `GET /api/v1/developer/experiences/{slug}/code/logs` | `code_experiences/api.py:414` |
| `GET /api/v1/code/files/{token}` | `code_experiences/api.py:427` |

### 5.6 Deno 宿主平台方法（52）与处理槽（12）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/code_experiences/deno_host.js` 的 `makeSession` 与 `HANDLERS`。这是 Hub 侧服务端宿主注入给代码型 Experience 的平台面。标「server 上拒绝」的，在此宿主里是 `notOnServer` 桩，形状记下，不假装在 server 上已经能用。手机或其他本地宿主若另有一份实现，尚未对照，见第 9 节。

这些处理槽与体验编写面里代码型处理槽名字相近，仍是运行时宿主槽，不得与已冻编写面词表合并或重冻。

平台方法 52 个：`now`；`store.get` / `cas` / `list`；`timers.schedule` / `cancel` / `pause` / `resume` / `get` / `list`；`schedules.list` / `set`；`output.speak` / `notify`；`outputs.read` / `write` / `update`；`materials.add` / `query` / `get` / `delete` / `keepEvidence`；`images.get` / `upload`；`net.fetch`；`agent.ask` / `start` / `send` / `stop`；`peer.send`；`files.write` / `append` / `list` / `delete`；`log.debug` / `info` / `warn` / `error`；`camera.capture` / `status` / `cancel`（server 上拒绝）；`perception.frames` / `audio`；`perception.subscribe` / `pause` / `resume` / `unsubscribe` / `list`（server 上拒绝）；`local.get` / `set` / `delete` / `list`（server 上拒绝）。

处理槽 12 个（`HANDLERS` 键）：`onInstall`、`onUpgrade`、`onUninstall`、`onMount`、`onUnmount`、`onSignal`、`onSegment`、`onUtterance`、`onButton`、`onTimer`、`onSchedule`、`onPeer`。

### 5.7 产出与材料（18）

指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/artifacts.py` 与 `AIOS2.0/backend/src/aios2/api/task_assets.py`。

| 项 | 指针 |
|---|---|
| `GET /api/v1/phone/assets` | `api/artifacts.py` |
| `GET /api/v1/phone/assets/{output_id}` | 同上 |
| `DELETE /api/v1/phone/assets/{output_id}` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials/query` | 同上 |
| `POST /api/v1/artifacts/{experience}/materials/keep-evidence` | 同上 |
| `GET /api/v1/artifacts/{experience}/materials/{entry_id}` | 同上 |
| `DELETE /api/v1/artifacts/{experience}/materials/{entry_id}` | 同上 |
| `POST /api/v1/artifacts/{experience}/outputs` | 同上 |
| `DELETE /api/v1/artifacts/{experience}/sharing` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/outputs` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/materials` | 同上 |
| `POST /api/v1/developer/experiences/{experience}/materials/query` | 同上 |
| `GET /api/v1/phone/tasks` | `api/task_assets.py`，`@router.get("/api/v1/phone/tasks")` |
| `GET /api/v1/phone/tasks/deliveries` | `api/task_assets.py` |
| `GET /api/v1/phone/tasks/{task_id}` | `api/task_assets.py` |
| `GET /api/v1/phone/task-files/{item_id}` | `api/task_assets.py` |
| `DELETE /api/v1/phone/tasks/{task_id}` | `api/task_assets.py` |

### 5.8 ToolRegistry 其余固定工具（形状保留；不另加进 147）

已锁定口径：ToolRegistry 的 147 贡献只来自已点名并计入其他类的项（感知 5 + MCP 元工具 5，已在第 5.1、5.4 节）。装配指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/composition.py` 的 `register_port` 列表（`tools`、`background_job_tools`、`document_workspace`、`mcp_manager`、`skill_tools`、`skill_source_tools`、`web_search_tools`、`reality_tools`、`segment_tools`、`output_tools`、`conversation_tools`）。

其余固定工具名本轮未全点，**不以旧「47」为已复核总数**，故不另加项进 147。触及 Memory 的 documents 调用类型见第 7 节。动态 `mcp__*` 与 `code.*` 不计固定总数。

### 5.9 形状保留小结

3 + 5 + 8 + 12 + 5 + 32 + 52 + 12 + 18 = **147**。与上文 16 类去重主合计中的 147 一致。

## 6. 明确不进本契约

下列对象不进本份契约的稳定面，也不在 v0.1.0 里承诺。这里按已锁定分类列出，不另发明一个计入 238 的整数。

- 已公开的设备契约（CapabilityId / PermissionId、75 个操作、ErrorCode）与体验编写面（含会话处理、代码型 Experience、CLI `sideload`、代码型处理槽与 Capability）。不重冻，不把那 401 项写入本稳定面。
- Host 侧载：调试侧载不是商店发布，不在本份重冻。已读指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`mobile/src/glass-host/sideload.ts` 的 `sideloadToken`、`assertSideloadToken`、`finishSideload`。同目录 `sideload-native.ts` 在盘点时未打开，见第 9 节。
- Harness：无对外 HTTP / SDK 接口，不算一类可公布 API，也不做成并列公开标准。
- 内部回环后台助手（`api/background.py`）：仅 loopback，不是公网 API。盘点未重数条数，不得把旧约数写成已复核新结论。
- 生产网关实现与网关自有 HTTP/WS 面：`aios/gateway/` 整仓不开放。调用约定原则见第 9 节，不把网关实现带进公开范围。
- 可单独替换的感知管线契约：总计划第 6 步，现不定、不开。第 5.1 节 5 个工具只保留形状。
- 执行脑、两个大脑不作为与本契约并列的公开标准。
- 总计划第 5 步的 Console／Studio／虚拟眼镜、账号鉴权、Memory 服务本身、手机页面／收件箱／权限。本轮碰到但不纳入 238 的手机页：`GET /api/v1/phone/home`、`GET /api/v1/phone/privacy`、`GET /api/v1/phone/privacy/summary`（`phone/router.py`）。`app.py` 上的 `GET /health`、`GET /product-icons/{name}`、`GET /market-covers/{name}` 也不进本契约。
- 未核实、不纳入本契约的 Mentra `cloud-v2`（本契约不是 Mentra 或其 SDK 的派生文档；提及仅用于标明排除项，不授予商标使用权）。

手机侧打断页 `GET /api/v1/phone/interrupt/held`、`POST /api/v1/phone/interrupt/feedback` 已锁定为形状保留不冻，但不属于 16 类主合计 147；本契约同样不把它们算进 147 或 91。

## 7. 留云调用类型

始终留云的服务，本契约只标明调用类型，不写可离线替代实现，也不把服务与数据搬离云。

- **市场安装**：平台 `/products/{id}/install` 等属第 18 类，不在第 4.7 节 12 条里。协议客户端打到 `/api/v1/platform/*` 的 7 个方法是留云调用类型，见第 8.1 节：`experiences.catalog`、`installed`、`config`、`install`、`setEnabled`、`checkUpdate`、`uninstall`。
- **手机市场消费页**（不加入 238）：`GET /api/v1/phone/market`、`GET /api/v1/phone/market/{slug}`、`GET /api/v1/phone/market/stories/{story_id}`、`GET /api/v1/phone/developers/{developer_id}`。指针：`phone/router.py`。
- **Memory 服务与数据**：无独立 HTTP。documents 工具若触及 Memory，为留云调用类型；工具名未在锁定表里逐条复核，本契约不补虚构整数。
- **账号与密钥**：始终留云。本契约不把账号路由写入稳定面。

16 类主合计里，留云具名项为 0，与上文 16 类去重主合计口径一致；上述项不改 238。

## 8. `@aios/runtime-client`（只计类，方法不与 238 相加）

指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client/`。这是 Host 连接运行时的协议客户端，不是给开发者写 Experience 的 SDK。包版本见第 2 节。`index.ts` 导出 `RuntimeClient`、`DelegatedExperience`、`RuntimeSessionStream`、`RuntimeClientError`、`UnsupportedCapabilityError`、`isRuntimeEvent`、`toFormalOutput`，以及 `input-overlap`、`stable-prefix`、`RuntimeInputCandidateTransport` 和 `types.ts`。

### 8.1 `RuntimeClient` 公开方法 29（不是 30）

源：`aios/packages/runtime-client/src/client.ts`。分组：sessions 8、runs 4、activities 1、experiences 10、providers 1、approvals 2，加上 `capabilities`、`requireCapability`、`connect`。没有第 30 个方法。

| 分组 | 方法 | 桶 | 说明 |
|---|---|---|---|
| sessions（8） | `list`、`create`、`get`、`history`、`events`、`update`、`delete`、`workingState` | 拟冻结 | 封装第 4.5 节会话面，不重复计入 238 |
| runs（4） | `submit`、`get`、`cancel`、`events` | 拟冻结 | 同上 |
| activities（1） | `get` | 拟冻结 | 同上 |
| experiences（7） | `catalog`、`installed`、`config`、`install`、`setEnabled`、`checkUpdate`、`uninstall` | 留云调用类型 | 打到 `/api/v1/platform/*` |
| experiences（3） | `delegation`、`setDelegation`、`operation` | 拟冻结 | 打到 `/api/v1/glass/*`，对应第 4.7 节委托／操作 |
| providers（1） | `list` | 形状保留不冻 | 对应 `/provider-profiles` |
| approvals（2） | `mcpInputs`、`respondMcpInput` | 形状保留不冻 | 对应 MCP input-requests |
| 根方法（3） | `capabilities`、`requireCapability`、`connect` | 拟冻结 | 能力发现与会话流连接 |

小计：拟冻结 19，形状保留不冻 3，留云调用类型 7。合计 29。不与 238 相加。

### 8.2 `RuntimeSessionStream` 与输入预备传输

指针：`aios/packages/runtime-client/src/stream.ts`、`aios/packages/runtime-client/src/input-preparation.ts`。

`RuntimeSessionStream`（拟冻结，不与 238 或 29 相加）：`afterSequence`、`isClosed`、`ready`、`close`、`resume`、`snapshot`、`putImage`、`startActivity`、`messageActivity`、`reattachActivity`、`putVisual`、`putAudio`、`decideApproval`、`stopActivity`、`endSource`（13 个方法加 2 个取值器）。

`RuntimeInputCandidateTransport`（5，拟冻结，不与 238 或 29 相加）：`loadCapabilities`、`whenPreparationIdle`、`prepare`、`cancel`、`confirm`。请求打到第 4.5 节的 input-preparations 入口。

### 8.3 事件与输入辅助（不与 238 或 29 相加）

- 拟冻结的已点形状：`isRuntimeEvent`、`toFormalOutput`（`aios/packages/runtime-client/src/events.ts`）；正式输出形状见第 4.6 节。`toOutputInterrupt` 随 Attention 打断形状，拟冻结。
- 形状保留不冻（Host 客户端辅助，不是第三条 Hub 线协议）：`inputFingerprint`；`InputOverlapCoordinator` 的 `begin`、`setCapabilities`、`snapshot`、`partial`、`endpoint`、`anticipation`、`offerHypothesis`、`final`、`cancel`（`aios/packages/runtime-client/src/input-overlap.ts`）；`StablePrefixTracker` 的 `begin`、`observe`、`final`、`cancel`（`aios/packages/runtime-client/src/stable-prefix.ts`）。以及这两个模块导出的阈值常量和类型。

## 9. 未核对项与完整性限制

下列项在定稿时仍未能核对，不得补虚构整数。它们不阻止本契约公开，但限制行为保证的完整性。

1. **会话流 `event_type` 完整目录。** 来源：Hub `api/app.py` 的 stream 转发、`aios/packages/runtime-client/src/events.ts` / `types.ts`（客户端里 `event_type` 是字符串，不是封闭枚举）。本契约只记载第 4.6 节已点到的形状。
2. **ToolRegistry 固定工具的逐名全表与是否仍为 47。** 来源：`composition.py` 装配已读；各 Port 源文件未全部点名。旧算术 47 不得当作已复核新结论。
3. **`inbox/tools.py` 的 `ask`。** 旧表曾算进 47；装配块未见 `register_port`。未打开该工具文件本身，不知道是否改由别处挂上。
4. **生产网关 Glass MCP 4 个工具与 4 个协议方法。** 来源仅为盘点前的登记，未重读 `aios/gateway/mcp.ts`。原则保留：可以后段登记调用约定，网关实现明确不进。这 8 个名字不计入 238。
5. **手机／本地代码宿主的平台 API。** 只逐条点了 Hub 侧 `deno_host.js`。`camera.*`、`perception.subscribe` 等在 server 上是拒绝桩。
6. **`sideload-native.ts`。** 树中存在，盘点时未打开。`sideload.ts` 已读，明确不进。
7. **内部回环后台、Harness 源文件、Marketplace 安装 HTTP 全表、账号路由。** 原则已定，条数未重数。

## 10. 对照核查与第一切版核验

本契约第 4–5 节计入 91 与 147 的名单和计数，已对照上述冻结点的源码核查；7 个能力名与 `RuntimeClient` 29 个方法的分桶一并核对。第 4 节每一个计入 91 的拟冻项，以及第 4.9–4.10 节的去重入口与能力名，都有源码或类型指针。没有发现需要改冻结集的差异。

第一切版还用冻结点上的 `@aios/runtime-client`（`0.1.0-d21.1`）类型做过真实类型检查，并通过。这只证明稳定面的类型形状对得上，**不是**真机验证，也**不是**系统级端到端。未连接生产或测试 Hub，未使用设备令牌，未编 Native，未发 npm。不得把类型检查或纸面说明写成已跑通端到端。

## 11. 本仓库公开的范围，以及尚未做的事项

本仓库只公开这份契约文档。`@aios/runtime-client` 实现、Hub、Reality Runtime、Agent Runtime、完整 HAL／Host 代码均未在本仓开放。两座私有工程仓的许可与可见性不变。

尚未公布第二批约 16 类 API 的对外文档。尚未开放 Reality Runtime、Agent Runtime 或完整 HAL／Host 实现。本切版不发 npm，也不把市场安装或 Memory 写成可离线替代。

本契约不是 Mentra 或其 SDK 的派生文档。

章节到此结束。稳定面、不承诺行为、不进本契约、留云调用类型、版本约定、与两份已公开契约的边界和四套词表、未核对项均已写明，没有未声明的剩余章节。
