# 留云调用类型（不列入本批公开 API 的实现与数据面）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


始终留云的服务，本批只标明调用类型，**不写可离线替代**，也不把服务与数据搬离云。完整平台调用面不在本目录公布。16 类主合计里，留云具名项为 0，与已公开契约正文一致；下列项**不改 238**。

## 市场：7 个 `experiences.*`（不列入公开 API）

协议客户端打到 `/api/v1/platform/*` 的下列 7 个方法是留云调用类型，属市场安装，不是 [07-experience-host.md](07-experience-host.md) 的 Host 启停 12 条，也不是 `delegation` / `setDelegation` / `operation`：

- `experiences.catalog`
- `experiences.installed`
- `experiences.config`
- `experiences.install`
- `experiences.setEnabled`
- `experiences.checkUpdate`
- `experiences.uninstall`

指针：`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`，`aios/packages/runtime-client/src/client.ts`。平台侧 `/products/{id}/install` 等安装 HTTP **全表不在本批公布**，见 [20-not-in-this-release.md](20-not-in-this-release.md)。

## 手机市场消费页（不加入 238）

属后续的开发者平台与留云调用面，不把商店面写进本批公开 API。指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`phone/router.py`，前缀 `/api/v1/phone`：

- `GET /api/v1/phone/market`
- `GET /api/v1/phone/market/{slug}`
- `GET /api/v1/phone/market/stories/{story_id}`
- `GET /api/v1/phone/developers/{developer_id}`

## Memory

Memory 是 16 类之一，必须出席，但**始终留云，不进 238**。无独立 HTTP 列入本批公开 API。documents 工具若触及 Memory，为留云调用类型（工具名单见 [14-tool-registry.md](14-tool-registry.md)），不写可离线替代。

## 账号与密钥

始终留云。本批不把账号路由写入公开 API，也不重数、不公布细表。
