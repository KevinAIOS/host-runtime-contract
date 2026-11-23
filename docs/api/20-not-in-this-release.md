# 明确不进，以及不在本批公布的对象

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


下列对象不进本批公开 API，也不另发明一个计入 238 的整数。原则已定的项本目录**不重数**。

## 明确不进

- 已公开的设备契约（CapabilityId / PermissionId、75 个操作、ErrorCode）与体验编写面（含会话处理、代码型 Experience、CLI `sideload`、代码型处理槽与 Capability）。不重冻。
- Host 侧载：见 [19-host-sideload.md](19-host-sideload.md)。
- Harness：无对外 HTTP / SDK 接口，不算一类可公布 API，也不做成并列公开标准。不重数源文件条数。
- 内部回环后台助手（`api/background.py`）：仅 loopback，不是公网 API。不重数，不得把旧约数写成已复核新结论。
- 生产网关实现与网关自有 HTTP/WS 面：`aios/gateway/` 整仓不开放。4+4 调用约定只写在 [13-mcp.md](13-mcp.md)，实现不公开，名字不计 238。
- 可单独替换的感知管线契约：现不定、不开，不在本目录范围内。[12-perception-tools.md](12-perception-tools.md) 的 5 个工具只保留形状。
- 执行脑、两个大脑不作为与本批并列的公开标准。
- Console／Studio／虚拟眼镜、账号鉴权、Memory 服务本身、手机页面／收件箱／权限：不在本目录公布。
- 手机页（`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`phone/router.py`）：`GET /api/v1/phone/home`、`GET /api/v1/phone/privacy`、`GET /api/v1/phone/privacy/summary`。
- `app.py` 上见到但不纳入 238 的：`GET /health`、`GET /product-icons/{name}`、`GET /market-covers/{name}`。
- Marketplace 安装 HTTP 全表（除在 [18-cloud-only.md](18-cloud-only.md) 标明的 7 个协议客户端方法名之外，不公布细表）。
- 未核实的 Mentra `cloud-v2`。

## 形状保留、但不属于 147 的两项

手机侧打断页（与 [08-attention.md](08-attention.md) 不是同一组路由），已锁定为形状保留不冻，但**不属 147**，也不加入 238：

- `GET /api/v1/phone/interrupt/held`
- `POST /api/v1/phone/interrupt/feedback`

指针：`phone/router.py` @ `4b4dd25e65b96ad3eadce4733f1fa269447b9615`。

## 本目录明确不包含的事项

本仓库这一批公开的是文档，不是实现。尚未为本目录打单独的 git 标签。未发 npm。未开放 Reality Runtime、Agent Runtime 或完整 HAL／Host 实现。未做真机或 Hub／Native 联调。网关实现仍不公开。
