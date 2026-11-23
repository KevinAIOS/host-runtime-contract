# Host↔运行时契约

AIOS Host 与运行时之间的契约。仓库：https://github.com/KevinAIOS/host-runtime-contract

许可为 [Apache-2.0](LICENSE)。契约版本是 **v0.1.0**。本仓库只公开契约文档，不开放运行时或 Host 实现，也不发布 npm 包。

本契约 v0.1.0 与已公开的 [glass-contract](https://github.com/KevinAIOS/glass-contract)（设备契约）和 [glass-sdk](https://github.com/KevinAIOS/glass-sdk)（体验编写面契约 / 第一版 SDK）的标签或契约 `v0.1.0` **不是同一份**，也与 `@aios/glass` 0.5.0、`@aios/glass-cli` 0.2.0 不是一回事。若为本仓库打 git 标签，使用 `contract-v0.1.0`，不要只用 `v0.1.0`。

## 这是什么

**Host ↔ 运行时契约**：Host 和运行时怎么配合，保住「前端现实、后端订阅」——Host 持有现实世界的信号与轨迹，运行时订阅并被叫醒，而不是由运行时自己占有传感器。完整正文见 [docs/Host运行时契约.md](docs/Host运行时契约.md)。

**第二批 API 文档**：面向 Host 与运行时实现方的厂商面目录，见 [docs/api/](docs/api/README.md)。它对照契约 v0.1.0，不改契约正文里的分桶、计数或冻结点。

冻结集：16 类去重主合计 **238**（拟冻结 **91**，形状保留不冻 **147**）。另有 7 个 Host↔运行时能力名拟冻结，不与 238 相加。`@aios/runtime-client` 是 Host 连接运行时的协议客户端，只计类，方法不与上述合计相加；本仓库不开放该包的源码，也不发 npm。

它**不是**：

- **不是设备契约**：Host ↔ 眼镜怎么说话，见 [KevinAIOS/glass-contract](https://github.com/KevinAIOS/glass-contract)。
- **不是体验编写面契约**：开发者怎么写 Experience，见 [glass-sdk 的体验编写面契约](https://github.com/KevinAIOS/glass-sdk/blob/main/docs/%E4%BD%93%E9%AA%8C%E7%BC%96%E5%86%99%E9%9D%A2%E5%A5%91%E7%BA%A6.md)。
- **不是运行时或 Host 实现**：私有工程仓仍是私有，本仓不开放 Reality Runtime、Agent Runtime、完整 HAL／Host，也不开放 `@aios/runtime-client`。
- **不是 npm 发布**，也不是运行时或 Host 源码。第二批厂商面 API 文档见 [docs/api/](docs/api/README.md)。

## 版本与冻结点

| 名称 | 值 |
|---|---|
| 本契约版本 | v0.1.0 |
| 协议 `contract_version` | `d21.v1`（schema `aios2.capabilities/v1`） |
| 对应协议客户端包（仍未公开实现） | `@aios/runtime-client` `0.1.0-d21.1` |
| Host／协议客户端冻结点 | 私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547` |
| Hub 冻结点 | 私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615` |
| 本仓库建议标签 | `contract-v0.1.0`（不要只用 `v0.1.0`） |

上述两座仓仍是私有。本仓库只公开契约文档，不改变它们的许可或可见性。指针里的路径指向这些私有仓中的源码位置，便于对照，并不等于那些实现已经开源。

## 限制

第一切版已对照冻结点完成分类盘点，每一拟冻项都有源码或类型指针，并用协议客户端类型做过真实类型检查。这只证明稳定面的类型形状对得上。

尚未做真机验证，未连接生产或测试 Hub，未做系统级端到端（Host 启动 Experience 并收到订阅叫醒），未编 Native，未发 npm。不得把类型检查或纸面说明写成已跑通端到端。市场安装与 Memory 始终留云，不提供可离线完整替代。

## 来源与许可

本文是 AIOS 第一份 Host↔运行时契约文档，不是 Mentra 或其 SDK 的派生作品。Copyright 2026 Kevin AIOS（陈子恒）。Apache-2.0，见 [LICENSE](LICENSE) 与 [NOTICE](NOTICE)。
