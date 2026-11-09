# 知识检索、经验与核心记忆

模型按需调用 `search_knowledge` 查询资料与已审核经验。检索按操作者和所选节点过滤，返回来源、版本与引用片段。操作完成状态由本次工具和业务健康证据核对。

## 文档与检索

PDF、DOCX、CSV 优先进入 Docling，随后由 `HybridChunker` 生成带标题、页码与 item ref 的语义块。LoongArch PDF 使用 Layout Heron ONNX 版面识别和 RapidOCR ONNX，文字层页面按区域提取，扫描页进入 OCR。

```text
文档与已审核经验 → 解析与结构切块 → 去重与版本管理
                 → 关键词 / 混合检索 → 可选改写与 Rerank → 引用片段
```

未配置 Embedding 时使用 SQLite FTS5 / BM25，FTS5 缺失时使用 LIKE 扫描。配置 OpenAI-compatible Embedding 后启用向量或混合检索，向量保存 provider、model、version、dimensions 与 signature，切换向量空间时重建索引。优先使用 FAISS，LoongArch 可使用 NumPy 精确检索兼容实现。

查询先做运维别名规范化，再可选调用轻量 LLM 改写，漂移或调用失败时使用确定性查询并记录原因。Rerank 支持 lexical 与独立 OpenAI-compatible 服务。主模型、Embedding、轻量 LLM 和 Rerank 分别配置及探测。

## 经验发布与归纳

任务完成检查通过、真实变更成功且所有变更节点取得后续健康证据后，生成引用原 Trace 的待审经验。管理员在原“经验审核”入口修订，再验证并发布；新版本审核期间继续使用旧发布版本，通过后替换索引。

定期整理从至少三个独立、已审核、具有实际证据且权限范围一致的案例归纳共同经验。归纳结果进入同一审核队列，发布后归档重复案例的活跃检索资格，历史内容和证据继续保存。来源撤回、过期或更新时同步调整归纳内容的检索资格。

## 核心记忆与状态事实

每次完整核心上下文最多 2,400 字符、6 项，按当前操作者和节点选择，在当前运行内冻结；恢复审批或用户回答会话时更新快照。

状态事实当前接收真实 `business_health_check` 凭据，保存观察时间、节点、健康值和 evidence_id，有效期 60 秒。迟到记录按观察时间插入，同一时间的不同值进入冲突状态，支持历史查询与人工失效。

Agent 可按需调用 `search_memory_facts`。管理员在“核心记忆与事实”页面预览、整理、失效与追溯来源。150 条当前 RAG 查询的资料源召回见 [评测说明](evaluation.md)。
