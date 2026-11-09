# 龙芯与麒麟平台适配

生产交付面向龙芯 3A5000、LoongArch64 和银河麒麟高级服务器 V11，构建、部署和验收平台为 `linux/loong64`。其他架构用于本地开发、静态检查与界面联调。

## 系统画像与预检

发行版画像读取 `/etc/os-release` 和麒麟版本证据。专项检查覆盖 KYSEC / SELinux、auditd、firewalld、rpm / dnf / yum、systemd、NetworkManager、RAS、SNMP 与 V11 原生工具。

部署预检汇总配置、密钥、状态后端、离线 wheelhouse、Docker 与宿主平台，记录 Python 标签、GCC 目标、glibc、页大小、LSX / LASX 和镜像架构。

## 文档与观测

LoongArch 文档链路使用 Layout Heron ONNX 与 RapidOCR ONNX，结构块由 Docling `HybridChunker` 生成。二进制依赖采用 Loongnix wheel 或明确的原生构建流程，模型制品记录固定版本和 SHA-256。

原生 FAISS 缺失时使用 NumPy 精确检索兼容实现。运行时 Trace 经标准 OTLP/HTTP Bridge 导出脱敏工作流、模型、工具与审批记录，并配置 LoongArch 真机契约工作流。

## 交付记录

镜像、依赖与模型按平台和内容摘要核验，节点按能力目录提供当前可用工具。展示仓库公开适配方案和测量摘要，目标真机验收记录按具体版本、环境与时间维护。
