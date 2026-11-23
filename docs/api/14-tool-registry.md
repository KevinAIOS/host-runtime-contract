# ToolRegistry 固定工具（形状保留不冻；余名不改 238）

日期：2026-11-23，America/New_York（ET；当时为 EST，UTC-5）。约 12:15 PM ET。
性质：Host↔运行时第二批 API 文档。许可 Apache-2.0。本仓库只公开文档，不开放运行时或 Host 实现，也不发布 npm 包。
读者：Host 与运行时实现方，不是用 `registerApp` / `defineExperience` 写 Experience 的应用开发者。
对照冻结点：私有 `KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`；私有 `KevinAIOS/AIOSGlass` 提交 `d5a93a371b3d825b87771ab517c435551948a547`。本仓库不改这两座私有仓，也不改已冻结契约正文的分桶、计数或冻结点。


本页各项均为**形状保留不冻**：只记录名字、路径或类型形状，**不承诺行为**。不得把本页写成已冻结的稳定面。

ToolRegistry 必须作为类出席。已计入 238 的固定工具，只是已点名并计入其他类的感知 5 + MCP 元工具 5。其余已挂名字按下面列出，**不加进 238**。动态 `mcp__*` 与 `code.*` 不计固定总数。

本冻结点核对：经 `register_port` 挂上、且在本提交的构造方式下会进入 `definitions()` 的固定工具，点到 **46** 个名字（含上述已计入其他类的 10 个）。这不是新的冻结总数。旧算术「47」不得写成已复核结论。46 与 47 的差，就是下面未挂装的 `ask`。

- 装配指针：`KevinAIOS/AIOS-new-` 提交 `4b4dd25e65b96ad3eadce4733f1fa269447b9615`，`AIOS2.0/backend/src/aios2/api/composition.py` 的 `register_port`（11 个端口，与已公开契约所列装配一致，仍无 inbox）
- 各 Port 源文件均在同一提交、同一 `AIOS2.0/backend/src/aios2/` 树下

## 本冻结点已挂上的固定工具

| 端口与源文件 | 名字（tool_id） | 项数 | 备注 |
|---|---|---|---|
| `tools` ← `tools/search_notes.py`；转写定义在 `tools/transcribe_audio.py` | `search_notes`（`notes.search@1`）、`transcribe_audio`（`audio.transcribe@1`） | 2 | 后者随 `transcriber` 注入而进入 `definitions()`；本冻结点的 `composition.py` 会注入转写器 |
| `background_job_tools` ← `tools/background_jobs.py` | `start_continuous_transcription`（`audio.continuous_transcription.start@1`）、`get_background_job_status`（`background_job.status@1`）、`stop_background_job`（`background_job.stop@1`） | 3 |  |
| `document_workspace` ← `tools/documents.py` | `list_documents`（`documents.list@1`）、`search_documents`（`documents.search@1`）、`read_document`（`documents.read@1`）、`create_document`（`documents.create@1`）、`append_document`（`documents.append@1`）、`replace_document_section`（`documents.replace_section@1`）、`list_document_versions`（`documents.versions@1`）、`restore_document_version`（`documents.restore@1`） | 8 | 触及 Memory 时为留云调用类型，不写可离线替代；见 [18-cloud-only.md](18-cloud-only.md) |
| `mcp_manager` 元工具 ← `tools/mcp_platform.py` | `search_tools`、`search_resources`、`read_resource`、`search_prompts`、`use_prompt` | 5 | 已在 [13-mcp.md](13-mcp.md) 计入 147，此处不重复加进 238 |
| `skill_tools` ← `skills/tools.py` | `load_skill`（`skills.load@1`）、`run_skill_script`（`skills.run_script@1`） | 2 |  |
| `skill_source_tools` ← `skills/source_tools.py` | `find_skills`（`skills.find@1`）、`install_skill`（`skills.install_remote@1`）、`check_skill_updates`（`skills.check_updates@1`）、`update_skill`（`skills.update_remote@1`） | 4 |  |
| `web_search_tools` ← `tools/web_search.py` | `web_search`（`system.web_search@1`） | 1 |  |
| `reality_tools` ← `reality/perception.py` | `emit_event`、`wake`、`look_closer`、`fast_judge` | 4 | 已在 [12-perception-tools.md](12-perception-tools.md) 计入 147 |
| `segment_tools` ← `reality/segment_tools.py` | `segment_done`（`reality.segment_done@1`） | 1 | 与上一行合计为感知 5 |
| `output_tools` ← `artifacts/generation/tools.py` | `submit_output`（`artifacts.submit_output@1`）、`write_note`（`materials.write_note@1`）、`keep_evidence`（`materials.keep_evidence@1`）、`keep_frame`（`materials.keep_frame@1`）、`query_materials`（`materials.query@1`）、`submit_meeting_notes`（`artifacts.submit_meeting_notes@1`） | 6 |  |
| `conversation_tools` ← `runtime/conversation.py` | `await_answer`（`conversation.await_answer@1`）、`relay_to_assistant`（`conversation.relay@1`）、`assistant_transfer`（`assistant.transfer@1`）、`assistant_launch`（`assistant.launch@1`）、`look`（`assistant.look@1`）、`become_experience`（`assistant.become_experience@1`）、`done`（`assistant.experience_done@1`）、`hand_to_background`（`assistant.background@1`）、`report_to_background`（`background.report@1`）、`hand_to_my_background`（`experience.background@1`） | 10 |  |

## 边界：`inbox.ask` 有定义、未挂上

- 文件存在：`AIOS2.0/backend/src/aios2/inbox/tools.py` @ `4b4dd25e65b96ad3eadce4733f1fa269447b9615`。类 `InboxToolPort`，工具名 `ask`，`tool_id` 为 `inbox.ask@1`。
- `api/composition.py` 的 `register_port` 装配块里**没有** inbox 端口，全文也没有 `InboxToolPort` 引用。
- 因此它**不算**本冻结点已在册的固定工具，不得加入 238，也不得为凑旧「47」而算进去。本批若提到它，只作为边界说明。
