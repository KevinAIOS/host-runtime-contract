# 分桶与计数规则

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


## 四桶

| 桶 | 在本批文档里怎么写 |
|---|---|
| 拟冻结 | 写出交互形状与当前冻结点上的入口名单。这是本批稳定面。细则若契约已写明边界，本页沿用；不发明未经源文件支撑的请求体或行为保证。 |
| 形状保留不冻 | 只写名字、路径或类型形状，并在页首标明**不承诺行为**。 |
| 留云调用类型 | 可点名，并写清不是离线替代，实现与数据面不进本批。市场 7 个 `experiences.*` 只在 [18-cloud-only.md](18-cloud-only.md) 出现，**不列入公开 API**。 |
| 明确不进 / 不在本份公布 | 目录或专节列出边界，不写调用手册。Host 侧载见 [19-host-sideload.md](19-host-sideload.md)。 |

## 主合计怎么加

16 类主合计只含已从钉死提交列出、并写入已公开契约正文的项。进入 238 的构成见 [README.md](README.md)。下列**不相加**：

- 7 个 Host↔运行时能力名（拟冻结标识符）
- `@aios/runtime-client` 的 29 个方法、会话流、输入传输与辅助类型（只计类）
- 输入预备 5 条 Glass 认证入口（与会话 HTTP 去重，类要出席，数不加第二次）
- ToolRegistry 中除已计入感知 5 + MCP 元工具 5 以外的余名
- 网关 4 个 Glass MCP 工具 + 4 个协议方法（可写调用约定，实现不公开）
- 手机侧代码宿主在冻结点上点到的 35 个 session API 名（附录，不与 Hub 侧 Deno 52+12 合并）
- `inbox.ask`（有定义、未挂装）
- 动态 `mcp__*` 与 `code.*` 工具（不计固定总数）
- 内部回环后台、Harness、Marketplace 安装 HTTP 全表、账号路由（不重数、不公布）
- 手机市场消费 4 条、手机打断页 2 条、手机页 `GET /home` 等（见 [18-cloud-only.md](18-cloud-only.md)、[20-not-in-this-release.md](20-not-in-this-release.md)）

`event_type` 不按接口另计，也不得写成「共 N 种」。

## 与已公开契约的关系

本批是契约 v0.1.0 的厂商面目录，不是一份新的冻结集。名单、分桶、238 / 91 / 147 以已公开契约为准。本目录在同一冻结点上补充了契约撰写时未点完的名字与指针（工具余名、网关 4+4、侧载 Native 文件、手机 session API 名、更多 `event_type` 字面量），**没有改锁**。
