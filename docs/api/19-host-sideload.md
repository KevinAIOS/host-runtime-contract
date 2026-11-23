# Host 侧载（明确不进，不在本份公布）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


Host 侧载是 16 类之一，目录必须出席，但本份**明确不进、不在本份公布**，不写调用手册，也不计入 238。这是调试侧载，不是商店发布。CLI `sideload` 已在体验编写面契约中处理，本份不重复公布、不重冻。

已在冻结点打开、仅用于确认排除范围的源文件（`KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`）：

- `mobile/src/glass-host/sideload.ts`：`sideloadToken`、`assertSideloadToken`、`finishSideload`（另有 `SideloadReceipt` 类型）。这 3 个导出归明确不进。
- `mobile/src/glass-host/sideload-native.ts`（约 1915 字节）：补核已打开。导出 `writeSideloadReceipt`、`prepareSideload`（依赖 `sideload.ts` 的 `assertSideloadToken` 与 `SideloadReceipt`，处理收件箱里的 zip 与收据）。这两个导出**仍然不公布**，不写成新的公开 API。
