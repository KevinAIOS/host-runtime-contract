# 观察器／Glass 信号摄入（24，拟冻结）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**拟冻结**：可写交互形状，仍以冻结点源文件为准。

本类计入拟冻结 91（从而计入 238）。本类是 **24** 条，不是锁前旧约数 14。多出的 10 条是按体验挂载、运行与订阅的路由，已一并列入拟冻结边界。

- 指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/glass_signals.py`
- 行号相对该提交的该文件原文

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

冻的是边界形状。本页不把这些路由写成设备契约或体验编写面的一部分。
