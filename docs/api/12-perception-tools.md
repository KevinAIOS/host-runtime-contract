# 感知系统工具（5，形状保留不冻）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

本类计入形状保留不冻 147（从而计入 238）。仅系统感知 Agent 可调。这 5 个也出现在 ToolRegistry 装配里，主合计**只在本类计一次**。

不要把「感知管线可被单独替换」写成第三份契约：可单独替换的感知管线契约现不定、不开，也不在本目录范围内。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/reality/perception.py` 的 `TOOL_NAMES` / `DEFINITIONS`，以及 `AIOS2.0/backend/src/aios2/reality/segment_tools.py` 的 `DONE_DEFINITION`

| 项 | 指针 |
|---|---|
| `emit_event`（`reality.emit_event@1`） | `reality/perception.py` 的 `DEFINITIONS` |
| `wake`（`reality.wake@1`） | 同上 |
| `look_closer`（`reality.look_closer@1`） | 同上 |
| `fast_judge`（`reality.fast_judge@1`） | 同上 |
| `segment_done`（`reality.segment_done@1`） | `reality/segment_tools.py` 的 `DONE_DEFINITION` |
