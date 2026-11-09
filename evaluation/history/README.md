# 历史版本与测量记录

本目录按原版本保存阶段性结果，当前进展见 [current-status.json](../current-status.json)。历史 JSON 的展示说明已统一为测量范围和状态，原有运行标识、计数与结果字段保留。

| 记录 | 测量范围与结果 |
| --- | --- |
| [v0.6.203](evaluation-results-v0.6.203.json) | 769 例，764 通过、5 失败，其中 2 个 critical safety failure 触发 hard gate，最终 score 为 0 |
| [v0.6.169](evaluation-results-v0.6.169.json) | 255 例，252 通过、1 失败、2 不可用；原始 pass_rate 口径为 252/253，score 为 0.9893 |
| [工具效果 v0.6.169](tool-effect-summary-v0.6.169.json) | Windows 主机：87 个注册工具，22 个可执行且验证通过，28 个不可用、37 个未执行 |
| [性能 v0.6.169](performance-baseline-v0.6.169.json) | 本地 2 用例，P50 / P90 / P99 均值为 55.39 / 55.62 / 55.63 ms |

v0.6.280 的旧工程记录（2026-08-09）：2352 passed、4 skipped，覆盖率 80.58%。该次 CI 记录覆盖 Python、Java、浏览器、打包、观测和 Docker smoke；当前本地功能回归另见当前状态文件。

旧 `evidence_governed_aiops_zh_v1` 清单共 4,380 加载行：OpsIntent 800、OpsRAG 300、OpsSafety 1,200、Evidence Gate 1,600、Fault Recovery 300、Agent 单工具投影 180。OpsIntent 使用 80 个模板，OpsSafety 使用 60 个模板，恢复规格来自 10 个故障族，RAG 来自 75 份工具资料与 4 类问题格式，投影由 OpsIntent 派生。数据来源与构造单位分别记录。
