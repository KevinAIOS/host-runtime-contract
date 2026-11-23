# Host↔运行时第二批 API 文档

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本文档是已公开契约 v0.1.0 的厂商面 API 目录，位于本仓库 `docs/api/`。不另开新仓，不并进 `glass-sdk` 或 `glass-contract`。

已公开的契约正文是：[docs/Host运行时契约.md](../Host运行时契约.md)。本目录对照那份契约，**不改**契约里的分桶、计数或冻结点。本目录与契约 v0.1.0（仓库标签 `contract-v0.1.0`）配套，但不是那份契约本身。若将来为本目录打单独的 git 标签，应使用 `api-docs-v0.1.0`，不要使用光秃的 `v0.1.0`，也不要复用 `contract-v0.1.0`。它与设备契约仓、体验编写面仓各自的 `v0.1.0` 也不是同一份。

## 范围与计数（不得改锁）

16 类主合计 **238 = 拟冻结 91 + 形状保留不冻 147**。构成与已公开契约正文一致：

- 拟冻结 91 = Reality 观测 8 + 订阅 10 + 观察器 24 + 本地配套 4 + Agent Runtime HTTP 中拟冻结 24 + WebSocket 2 + Experience 安装启停 12 + Attention 7。输入预备 5 条与会话侧同能力入口去重，**不另加**。
- 形状保留不冻 147 = Agent Runtime HTTP 后段 3 + 感知系统工具 5 + Skills 8 + MCP 管理 HTTP 12 + MCP 元工具 5 + `code_experiences` HTTP 32 + Deno 平台方法 52 + 处理槽 12 + 产出与材料 18。

另外：7 个 Host↔运行时能力名拟冻结，但不与 238 相加；`@aios/runtime-client` 只计作一类，公开方法 29（不是旧约数 30）不与 238 相加。16 类内核具名的留云项与明确不进项为 0；那些对象在留云专节或不公布专节出现。

不要使用锁前的近似值（RuntimeClient 30、Agent Runtime HTTP 29、观察器 14、`code_experiences` HTTP 4、「已复核 47」）。

## 分桶读法

详见 [00-buckets.md](00-buckets.md)。简要：

- **拟冻结**：稳定面的交互形状。
- **形状保留不冻**：只记形状，不承诺行为。
- **留云**：可点调用类型，不是离线替代；市场 7 个 `experiences.*` **不列入公开 API**。
- **明确不进 / 不在本份公布**：目录出席或专节列出，不写调用手册。

## 四套词表，不要合并

Host↔运行时能力名、设备契约的 CapabilityId / PermissionId、应用清单 `aios.json` 的 `APP_CAPABILITIES`、代码型 Experience 的 Capability，是四套不同的词表。本批只写第一套（以及本批范围内的 HTTP、工具、宿主方法）。不要与另外三套合并或重冻。两条 Experience 编写路径是「会话处理」和「代码型 Experience」，那是体验编写面契约的事，本批读者不是那条线上的应用开发者。

## 本目录

| 文件 | 内容 |
|---|---|
| [00-buckets.md](00-buckets.md) | 分桶与计数规则 |
| [01-reality-observe.md](01-reality-observe.md) | 观测 HTTP 8，拟冻结 |
| [02-reality-subscribe.md](02-reality-subscribe.md) | 订阅 HTTP 10，拟冻结 |
| [03-observers.md](03-observers.md) | 观察器 24，拟冻结 |
| [04-local-perception.md](04-local-perception.md) | 本地感知 4，拟冻结 |
| [05-agent-runtime-http.md](05-agent-runtime-http.md) | Agent Runtime HTTP 27（24 拟冻结 + 3 形状保留） |
| [06-agent-runtime-ws.md](06-agent-runtime-ws.md) | 会话套接字 2，拟冻结；`event_type` 已点字面量与缺口 |
| [07-experience-host.md](07-experience-host.md) | 安装启停 12，拟冻结（不含市场） |
| [08-attention.md](08-attention.md) | 注意力 7，拟冻结 |
| [09-input-prep.md](09-input-prep.md) | 输入预备 5，拟冻结，去重不另加进 91 |
| [10-capabilities.md](10-capabilities.md) | 7 个能力名，拟冻结，不计 238 |
| [11-skills.md](11-skills.md) | Skills HTTP 8，形状保留不冻 |
| [12-perception-tools.md](12-perception-tools.md) | 感知工具 5，形状保留不冻 |
| [13-mcp.md](13-mcp.md) | MCP 17 + 网关 4+4 调用约定 |
| [14-tool-registry.md](14-tool-registry.md) | 已挂固定工具名与 `ask` 边界 |
| [15-code-experiences.md](15-code-experiences.md) | HTTP 32 + Deno 52+12（计入 147）+ 手机侧 35 名附录（不计 238） |
| [16-artifacts.md](16-artifacts.md) | 产出与材料 18，形状保留不冻 |
| [17-runtime-client.md](17-runtime-client.md) | 协议客户端一类；方法不计 238 |
| [18-cloud-only.md](18-cloud-only.md) | 留云专节（含市场 7 个方法） |
| [19-host-sideload.md](19-host-sideload.md) | Host 侧载，不在本份公布 |
| [20-not-in-this-release.md](20-not-in-this-release.md) | 明确不进与不在本批 |

各页已写明仍保留的缺口（例如会话流 `event_type` 不是完整目录）。本目录有冻结点源文件指针，或明确标出尚未列全的部分；这不等于真机、Hub 联调或 npm 发布已经做过，也不要求打开 Hub 或网关的实现仓，也不为动态 MCP／代码工具给出固定总数。
