# Muelsyse

> 做 AI 编码智能体的运行时与插件工程：把「不确定的模型」围在确定性的边界里。
> Runtime & plugin engineering for AI coding agents — keeping non-deterministic models inside deterministic boundaries.

## 开源贡献

| 项目 | 贡献 |
| --- | --- |
| [OldSuns/pi-open-tui](https://github.com/OldSuns/pi-open-tui) · 85★ | [PR #9](https://github.com/OldSuns/pi-open-tui/pull/9) — 修复设置浮层失活：定位跨三层根因（插件 `onConfigChanged` 立即重装编辑器 → Pi core `setCustomEditorComponent()` 无条件 `setFocus` 抢焦点 → TUI 焦点状态机把浮层恢复标记为 `blocked`），改为浮层关闭后再 install/uninstall，附 37 行回归测试 |
| [Ginkgoooo/pi-cc-switch-provider](https://github.com/Ginkgoooo/pi-cc-switch-provider) · 16★ | [PR #2](https://github.com/Ginkgoooo/pi-cc-switch-provider/pull/2) — 修复绕过 ModelRuntime 的 `agentLoop()` 直连路径报 `No API provider registered`：把两个 cc-switch API 注册进 `@earendil-works/pi-ai` compat registry，附 136 行 RPC 回归测试与 fixture |

## 代表项目

### 确定性 Agent 运行时

- **[Elysian-Realm-agent](https://github.com/xMuelsysex/Elysian-Realm-agent)** — 确定性 Agent 认知内核：六阶段认知循环（perceive → retrieve → plan → act → remember → reflect）+ 端口抽象（`PerceptionPort` / `MemoryPort` / `PlanningPort` / `ActionSink` / `LlmPort`）。tick 轨道完全无 LLM 参与计划，对话轨道由 LLM 生成回复；两条轨道在 host 持有的共享状态（记忆流、亲密度快照）汇合，服务只返回提案，host 保持权威。83 个 TS 源文件 / 33 个测试文件。
- **[Elysian-Realm](https://github.com/xMuelsysex/Elysian-Realm)** — 同上的前身 monorepo：本地管理台 + OpenAI 兼容 LLM 边界，核心测试使用确定性假 provider，不需要网络与 API key。91 个 TS 源文件 / 17 个测试文件。

### 游戏引擎与全栈

- **[Hearthstone-web](https://github.com/xMuelsysex/Hearthstone-web)** — 浏览器端确定性卡牌引擎：`command → event → state` 单写入者 + 投影边界，日志经 canonical JSON → SHA-256 → 版本化事务提交，replay 逐事件校验 state hash；版本守卫 / 能力守卫 / 兼容矩阵三层分别解决「版本是否支持」「能力集合是否漂移」「各 carrier 允许什么组合」。三个源码约束脚本把上述不变量变成 CI 可执行门禁。114 个 TS 源文件 / 32 个测试文件（含 Playwright 里程碑 e2e）。
- **[biliNotAiVideo](https://github.com/xMuelsysex/biliNotAiVideo)** — B 站 AI 内容标识：FastAPI + PostgreSQL（alembic 迁移）+ Chrome MV3 扩展，含匿名安装认证、配额与结果验证。73 个 Py + 26 个 TS / 40 个测试文件。
- **[nzyDormitory](https://github.com/xMuelsysex/nzyDormitory)** — 宿舍电费监控：零第三方依赖 Python 后端 + 校园门户对接 + 企业微信告警，Docker 部署。44 个 Py / 14 个测试文件。

### 编辑器扩展与工具链

- **[pi-cyber-working-only](https://github.com/xMuelsysex/pi-cyber-working-only)** — Pi 编码智能体扩展：接管宿主 native working 行，用单一 33ms 挂钟循环渲染脉冲 / 动词 / 时长 / TPS / token HUD，并以版本化全局 lease registry 独占宿主机面（teardown 只恢复可见性，不覆盖其他扩展）。架构测试直接断言源码不变量。
- **[make-mermaid](https://github.com/xMuelsysex/make-mermaid)** — Claude Code 技能：从代码分析或自然语言生成 11 种 Mermaid 图表并渲染 PNG/SVG。
- **[betterLD](https://github.com/xMuelsysex/betterLD)** — LinuxDo 首页 Material 3 卡片化：零依赖 Manifest V3 扩展（Chrome / Firefox 共用一份清单）。

### Linux 桌面基建

- **[MuelNiri](https://github.com/xMuelsysex/MuelNiri)** · **[Muelsyse_dotfile_niri](https://github.com/xMuelsysex/Muelsyse_dotfile_niri)** — Arch + niri + Noctalia 的一键安装器与 chezmoi dotfiles：模块化安装、btrfs 快照安全网、断点续跑、动态取色主题联动。

## 技术栈

**主力语言** TypeScript · Python · C# · Shell
**前端与桌面** React · Vite · Vitest · Playwright · Avalonia · Unity (URP)
**后端与数据** FastAPI · PostgreSQL · SQLAlchemy / alembic · EF Core · SQLite
**AI 工程** Pi / Claude Code 扩展开发 · LLM 端口抽象与确定性假 provider · 事件溯源与确定性重放

