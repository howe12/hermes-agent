# CHANGELOG_HOLO.md

> aquarius-psyche 分支的独立变更日志。
> 上游 Hermes 的变更请看 [NousResearch/hermes-agent/releases](https://github.com/NousResearch/hermes-agent/releases)。

## [Unreleased] — 2026-06-13

### Added
- 仓库从 [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) fork 到 [howe12/aquarius-psyche](https://github.com/howe12/aquarius-psyche)
- 公开仓库（MIT 协议，与上游一致）
- 配双远程：`origin`（fork）+ `upstream`（NousResearch 官方）
- 新增文档：
  - `AQUARIUS_PSYCHE.md` — 命名哲学、愿景、三层架构（灵-魂-体）
  - `ROBOTICS.md` — 机器人集成方向（规划中）
  - `EDU.md` — 教育方向（规划中）
  - `CHANGELOG_HOLO.md` — 本文件
- README 顶部加 aquarius-psyche 分支横幅，注明"机器人集成规划中"

### Pending (待你定方向后启动)
- 阶段 1：跑通基线 Hermes（DeepSeek 配 + smoke test）
- 阶段 2：机器人特性层（ROS2 桥 → Gazebo → MoveIt2 → 行为树）
- 阶段 3：教育特性层（课程 RAG → 学情 → 编排 → 教学互动 → Web）
- 阶段 4：持续同步上游

### Notes
- 上游基线 commit：`95715dcb03003eab086eb0494083e6dc1c65f3b3`（v0.16.0 "The Surface Release"）
- 救命索 tag：`v0.16.0-aquarius-baseline`（阶段 0 收尾时打）
- 任何 PR 合入前必须保证能 `git checkout v0.16.0-aquarius-baseline` 回到干净基线
