# GitHub Copilot + HVE：从会用工具到可复现的 Agent 工程

面向**合作伙伴工程师**的中文 60 分钟分享包：HVE 深度研究、24 单元连续讲者大纲、可复现操作手册，以及可独立运行的 Agentic Commerce 离线 mock Demo。HVE 是工程方法主线，Commerce 是贯穿实例；本交付**不含 PPT/PPTX**。

> **SIMULATED / OFFLINE：**业务 planner 是确定性离线脚本，使用固定合成报价、身份、余额与模拟支付。没有真实模型推理、支付网络、供应商集成、生产鉴权或云部署。请勿输入真实身份、卡号、凭证或个人财务数据。建议不等于授权，付款仍需独立人工批准与确定性 Authority 校验。

## 快速开始：直接运行本仓库 main

需要 **Node.js 22+**。原生 Node HTTP/static/node:test，无第三方运行依赖、模型密钥或支付账户；`npm ci` 不是运行前置。

```powershell
git clone --branch main https://github.com/turbo998/Copilot-HVE-Engineering-Workshop.git
Set-Location .\Copilot-HVE-Engineering-Workshop
node --version
npm run check
npm run test:e2e
npm run demo
```

| 入口 | 本地地址 |
|---|---|
| Commerce Demo | <http://127.0.0.1:4187> |
| HVE 深度 H5（16 章、26 网页引用） | <http://127.0.0.1:4187/hve-report.html> |
| 60 分钟讲者大纲 | <http://127.0.0.1:4187/workshop/outline.md> |
| Demo 操作手册 | <http://127.0.0.1:4187/workshop/demo-runbook.md> |
| 来源登记（31 项，含执行证据） | <http://127.0.0.1:4187/workshop/sources.json> |

正文、目录、CSS/JS 和材料均本地可读，无 CDN；引用网页不是运行依赖。H5 保留外置资源和脚本/样式限同源的 CSP，不使用 `unsafe-inline`。材料路由仅开放七个明确白名单文件，不开放源码、tracking 或状态目录。

服务只绑定 loopback。`npm run demo` 仅使用**当前克隆的 `data/workshop-state.json`**，与保留的 `npm start`（4173，`data/state.json`）独立。端口占用时不要停止其他服务，在自己的终端选空闲端口：

```powershell
$env:PORT = '4188'
npm run demo
```

对应地址改为 `http://127.0.0.1:4188`。不要让两个进程写同一 workshop 状态。优先在**自己的专用 Demo**页面点击“重置本地模拟”；文件级重置须先停止自己的实例，只删除 `.\data\workshop-state.json`，不删除整个 `data` 或其他 checkout 的文件。完整预检、限定重置与约 9 分钟演示顺序见[操作手册](docs/workshops/copilot-hve-commerce/demo-runbook.md)。

## 分享材料与目录

| 路径 | 内容 |
|---|---|
| [public/hve-report.html](public/hve-report.html) | 16 章 HVE 深读报告，26 网页引用，15 个研究问题；检索、主题、复制反馈、键盘导航和完整打印 |
| `public/hve-report.css`、`hve-theme.js`、`hve-report.js` | 外置样式与交互，无网络运行依赖 |
| [outline.md](docs/workshops/copilot-hve-commerce/outline.md) | 24 单元，连续 00:00–60:00，含讲者展开、原创图示建议、Demo 转场与 Q&A |
| [demo-runbook.md](docs/workshops/copilot-hve-commerce/demo-runbook.md) | 新仓库快速开始、干净状态、业务验收、原开发复演与 VS Code 待预检路径 |
| [sources.json](docs/workshops/copilot-hve-commerce/sources.json) | 官方说明、固定源码合同、实际运行和建议分别标识；31 项登记 |
| [evidence/](docs/workshops/copilot-hve-commerce/evidence/) | 原仓库的 host/skill 哈希、真实 RPI 预演与业务/H5 浏览器断言；不是本仓库新执行日志 |
| `src/`、`public/`、`test/`、`scripts/` | 完整 Node 服务、业务 UI、离线 planner/Authority、回归测试与可选浏览器检查函数 |
| [docs/architecture.md](docs/architecture.md)、[docs/copilot-studio-connector.md](docs/copilot-studio-connector.md)、`connector/` | 业务架构与本地 API 合同；connector 未在真实租户验证 |
| [docs/research.md](docs/research.md)、[Stripe 专题](docs/research/stripe-sessions-2026.md)、[docs/sources.md](docs/sources.md) | Commerce 公开来源研究、证据等级与原实现的公开复用边界 |
| [.github/copilot-instructions.md](.github/copilot-instructions.md) | 开发不变量、最小单位、人审权限、回归与状态隔离规范 |

Demo 核心场景：USD 70 推荐相机 59.99 和咖啡 18.99 作为**各自独立**候选，耳机 79.99 明确超限 9.99；USD 10 为 `no_action`；币种错配不换汇。相机经独立人审执行后，同任务咖啡会被累计预算拒绝；重复同一授权不产生重复模拟付款。HTTP 402-shaped 指南挑战不是完整 MPP/x402 互操作。

## 来源、发行身份与证据边界

完整课程从公开原仓库 [`turbo998/agentic-commerce-lab` 固定提交 `202f9b3defa6b40d3c60d18b82066af846431d52`](https://github.com/turbo998/agentic-commerce-lab/tree/202f9b3defa6b40d3c60d18b82066af846431d52) 导入。原开发基线 `7c5d931…`、功能 `d39a5d4…`、材料检查点 `a998f5f…` 和 PR 记录是**原仓库历史**，不是新仓库的开发或合并记录。运行本仓库不依赖原未合并分支，也不需要原仓库 checkout、Git 对象或服务。

本仓库是课程发行，**不是 `microsoft/hve-core` 官方分支或官方课程**，没有将整个上游 HVE vendor 进来。HVE `49dfb738…` 仅是固定研究快照。保留原 [MIT License](LICENSE) 和 `Agentic Commerce Lab contributors` 归属，不另选许可证。第三方产品、协议名称和链接不代表背书或认证。

原研究/开发记录发生于 2026-10-12，实际 host 为 **Copilot App/CLI 1.0.94-3 + 本机 user-scoped RPI phase skills**；旧 skills 的上游 revision 未确定，以哈希标识。原 check 38/38、HTTP e2e 2/2、业务浏览器 13 项、H5 浏览器 35 项均是原仓库历史。VS Code Chat、当前 upstream RPI Agent wrapper、HVE Builder 未执行，不能由文件存在推断已运行。本次发行验证与原记录分开，不把 HTTP e2e 称为浏览器重跑。

原浏览器验证包含真实 Chromium PDF 渲染，但不代表实体打印或全面 WCAG 合规；复制 API 参数及失败降级已验证，**OS 剪贴板读回不可用**，不声称 round-trip 通过。没有真实模型/支付、生产认证或量化提效实验。所有运行状态、会话凭据、环境变量、日志、依赖与原始 `.copilot-tracking` 均不发布。

## 本发行验证（2026-10-13）

在新仓库隔离工作区以 Node 24.13.1 / npm 11.8.0 执行：`npm run check` **39/39**（原完整回归加一项新仓库 main 入口检查），`npm run test:e2e` **2/2**。许可证、31 项来源登记及四份原历史 evidence 与固定源提交逐字节一致；发行仅调整 README、操作手册、大纲发行说明、H5 历史口径及入口回归，不修改业务权限层。

另从本次发行文件导出**无 `.git`、无初始 data、无原 checkout** 的干净快照，用自己的 `127.0.0.1:43187` 临时服务验证：9 个页面/外置资源与 7 个白名单材料地址均 HTTP 200，8 个非公开路径均 404；CSP 无 `unsafe-inline`，16 章/26 引用/31 登记项/15 研究问题对账通过。HTTP 实际走通 USD 70/10、币种错配、agent 越权拒绝、独立 human 批准、累计预算、同授权重放和专用 reset；默认 `data/state.json` 未创建。临时服务验证后停止，不影响原 4187 服务。

以上是**本仓库 Node/HTTP 发行检查**，不是 Playwright、VS Code、RPI wrapper 或 HVE Builder 的新执行；原浏览器证据仍按原日期解释。
