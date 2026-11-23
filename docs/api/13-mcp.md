# MCP（管理 HTTP 12 + 元工具 5，形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

管理 HTTP 12 与元工具 5 计入形状保留不冻 147（从而计入 238）。动态外部工具 `mcp__{server}__{name}` 数量随配置变化，**不计固定总数**，也不在 147 里。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/app.py` 与 `AIOS2.0/backend/src/aios2/tools/mcp_platform.py`

## 管理 HTTP（12）

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

## 元工具（5）

与 ToolRegistry 去重后，只在本类计入主合计。

| 项 | 指针 |
|---|---|
| `search_tools`（`mcp.search_tools@1`） | `tools/mcp_platform.py` 的 `ToolDefinition` |
| `search_resources`（`mcp.search_resources@1`） | 同上 |
| `read_resource`（`mcp.read_resource@1`） | 同上 |
| `search_prompts`（`mcp.search_prompts@1`） | 同上 |
| `use_prompt`（`mcp.use_prompt@1`） | 同上 |

## 生产网关调用约定（4 个工具 + 4 个协议方法，不计 238）

实现位于 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547` 的 `aios/gateway/mcp.ts`。生产网关实现与 `aios/gateway/` **整仓不开放、明确不进**，见 [20-not-in-this-release.md](20-not-in-this-release.md)。此处只登记调用约定；这 8 个名字**不计入 238**。已在冻结点重读该文件，名字与先前登记一致。

Glass MCP 工具（`GLASS_TOOLS`，4）：

1. `experiences.search_installed`
2. `experiences.start_installed`
3. `glasses.get_capabilities`
4. `glasses.look`

协议方法（`GlassMcp` 对 JSON-RPC `method` 的分支，4）：

1. `initialize`
2. `ping`
3. `tools/list`
4. `tools/call`

以 `notifications/` 开头的方法在该实现里返回 202，不作为第 5 个协议方法列入上表，也不另发明总数。
