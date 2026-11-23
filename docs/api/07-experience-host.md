# Experience 安装启停（12，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。这 12 条是 Host 侧的启停、查询与委托，**不含**市场安装。市场 7 个 `experiences.*` 及平台安装路由见 [18-cloud-only.md](18-cloud-only.md)，不列入公开 API。

## Glass 入口（6）

前缀 `/api/v1/glass`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/glass.py`。

| 项 | 指针 |
|---|---|
| `POST /api/v1/glass/calls/validate` | `api/glass.py:207` |
| `GET /api/v1/glass/experiences` | `api/glass.py:241` |
| `POST /api/v1/glass/experiences/query` | `api/glass.py:245` |
| `PUT /api/v1/glass/experiences/{product_id}/delegation` | `api/glass.py:252` |
| `GET /api/v1/glass/operations/{request_id}` | `api/glass.py:276` |
| `POST /api/v1/glass/experiences/start` | `api/glass.py:284` |

## 手机 experiences（6）

前缀 `/api/v1/phone`。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/phone/router.py`。

| 项 | 指针 |
|---|---|
| `GET /api/v1/phone/experiences` | `phone/router.py:297` |
| `GET /api/v1/phone/experiences/{slug}` | `phone/router.py:302` |
| `POST /api/v1/phone/experiences/{slug}/output-fallback` | `phone/router.py:358` |
| `POST /api/v1/phone/experiences/{slug}/enabled` | `phone/router.py:396` |
| `POST /api/v1/phone/experiences/{slug}/stop` | `phone/router.py:423` |
| `POST /api/v1/phone/experiences/{slug}/uninstall` | `phone/router.py:447` |

协议客户端里与本类对应的拟冻结方法是 `experiences.delegation`、`setDelegation`、`operation`（打到 `/api/v1/glass/*`），见 [17-runtime-client.md](17-runtime-client.md)。不要把它们与留云的市场方法混为一谈。
