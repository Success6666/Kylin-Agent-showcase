# 技术栈与组件职责

以下依赖按主项目 v1.0.2 的前端入口、package.json、pyproject.toml、Spring POM 与运行时实现核对。

## 工作台与认证

| 技术 | 职责 |
| --- | --- |
| Vue 3 | 聊天、节点、巡检、告警、审批、知识、Trace 与评测交互 |
| Vite 6.4.3 / Terser | 静态资源构建与压缩 |
| Mermaid 12.2.0 | 横向业务流程图与组件调用图 |
| Marked 18.1.1 / DOMPurify 3.4.17 | 模型回答的 Markdown 解析与 HTML 清洗 |
| Nginx | 静态资源和 API 反向代理 |
| Java 17 / Spring Boot 3.5.16 | 认证网关、账号与可信身份服务 |
| Sa-Token 1.45.0 | 登录会话、RBAC 与节点权限 |
| H2 | 认证服务用户与配置存储 |

## Agent 与运行时

| 技术 | 职责 |
| --- | --- |
| Python ≥3.10 / FastAPI / Uvicorn | 控制面和节点 API、SSE 与运行时服务 |
| HTTPX | 模型端点、受管节点与集成服务请求 |
| 原生 function-calling 循环 | 主模型自主选择工具、读取观察、提问与继续处理 |
| LangGraph 0.2.76 / checkpoint | 状态、审批恢复及已有兼容工作流 |
| Agent Runtime Governance SDK v0.9.1 | 工具 Schema、审批闸门、持久幂等、UNKNOWN 结果和 JSONL 审计 |
| HMAC v2 / 节点令牌 / 可选 mTLS | 网关可信上下文与受管节点认证 |

SDK 固定到不可变提交 `4cfb9ccc`。Kylin Adapter 负责业务注册表、节点身份和结果映射，Harness 管理任务权限、预检、审批与完成证据。

## 知识、消息与观测

| 技术 | 职责 |
| --- | --- |
| PostgreSQL | 龙芯部署 checkpoint 与恢复会话 |
| SQLite WAL / etcd | 持久任务、租约、幂等和状态配置 |
| SQLite FTS5 / BM25 | 关键词检索；FTS5 缺失时采用 LIKE 扫描 |
| FAISS / NumPy | 向量索引与 LoongArch 精确检索兼容实现 |
| Docling / HybridChunker | 文档结构解析、带标题/页码/引用的语义切块 |
| Layout Heron ONNX / RapidOCR ONNX | LoongArch PDF 版面识别、文字层提取与 OCR |
| RabbitMQ / Pika | durable topic、publisher confirm、manual ACK、DLX / DLQ |
| OpenTelemetry OTLP/HTTP | 脱敏工作流、模型、工具和审批 Trace 导出 |

主模型、Embedding、轻量查询改写与 Rerank 使用分别配置的 OpenAI-compatible 端点。知识库维护向量模型、维度与签名，模型切换后重建索引。LoongArch 运行时使用标准 OTLP/HTTP Bridge；其他开发配置可启用 Future AGI Observe SDK。

## 工程与平台

Docker Compose 编排七服务。GitHub Actions、pytest、Spring 测试、前端浏览器 smoke、工具描述审计和部署预检形成工程检查链。生产平台为龙芯 3A5000 / 银河麒麟 V11 / `linux/loong64`，模型制品和离线依赖通过固定版本与内容摘要维护。

本次执行的检查及结果见 [当前状态](../evaluation/current-status.json)，开发演进见 [Git 取舍](development-decisions.md)。
