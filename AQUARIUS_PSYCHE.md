# 🌊 aquarius-psyche

> **水瓶之魂** — 这是 NousResearch/hermes-agent 的机器人+教育领域分支。

## 命名故事

```
aquarius  = 水瓶座（黄道十二宫之一）
psyche    = 普赛克（希腊神话灵魂女神，爱神 Eros 的妻子）
```

- **aquarius** —— 神话中水瓶座是甘尼米德（Ganymede），宙斯最爱的侍酒少年。
  他**会思考**（为众神斟酒需要观察、判断、决策），
  **会服务**（身体力行地端酒）。
  正是"大脑+身体"合一的完美象征 —— 具身智能的本义。

- **psyche** —— 希腊语 ψυχή，灵魂/心灵。
  在亚里士多德哲学里，psyche 是**区别于纯物质的"生命原则"**——
  让一具身体"活"起来的那个东西。
  在神话里，Psyche 是爱神 Eros 的妻子，
  精神与爱（身体的接触）的结合。

- **合在一起** —— `aquarius-psyche` =
  "水瓶之魂" =
  "为学生倾囊相授的灵魂" +
  "身体与心灵合一的具身智能"。

## 三层架构（与 holo_agent / sagittarius 形成家族）

| 层 | 含义 | 项目 |
|---|---|---|
| 灵 · Runtime | 全息智能体壳（runtime / 框架） | `holo_agent`（半年前启动的旧项目） |
| 魂 · Mind | 水瓶之魂（大脑 / 思维 / 学习能力） | **`aquarius-psyche`（本仓库）** |
| 体 · Body | 射手之身体（机械臂 / 执行 / 物理世界） | `sagittarius_humble_ws` |

希腊神话谱系完全闭合：

- **Hermes**（赫尔墨斯）—— 宙斯的信使神，信息流的化身 → 上游项目 `hermes-agent`
- **Psyche**（普赛克）—— 爱神的妻子，灵魂的化身 → 本项目 `aquarius-psyche`
- **Sagittarius**（射手座）—— 半人马弓箭手，远程精准的化身 → 机械臂项目

三者都是宙斯主神体系下的角色，**完整的"灵-魂-体"三层**。

## 上游同步策略

- 仓库：`https://github.com/howe12/aquarius-psyche`
- 上游：`https://github.com/NousResearch/hermes-agent`
- 同步频率：每 2-4 周 rebase 上游 `main`
- 原则：
  - 通用改进 → PR 回上游
  - 机器人/教育特化 → 留在本分支
- 救命索 tag：`v0.16.0-aquarius-baseline`（每次 rebase 前打一个）

## 当前进度

- [x] **阶段 0** — 仓库 fork 公开完成
- [ ] **阶段 1** — 跑通基线 Hermes（DeepSeek 配 + smoke test）
- [ ] **阶段 2** — 机器人特性层（ROS2 桥 → Gazebo → MoveIt2 → 行为树）
- [ ] **阶段 3** — 教育特性层（课程 RAG → 学情 → 编排 → 教学互动 → Web）
- [ ] **阶段 4** — 持续同步 + 持续学习机制

详见各子文档。

## 贡献

- **机器人方向**：详见 [ROBOTICS.md](./ROBOTICS.md)
- **教育方向**：详见 [EDU.md](./EDU.md)
- **变更日志**：详见 [CHANGELOG_HOLO.md](./CHANGELOG_HOLO.md)
- **上游贡献**：通用改进请发 PR 到 [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

## 许可证

继承上游 [MIT License](./LICENSE)。基于 Nous Research 的开源工作。
