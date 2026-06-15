# 🤖 ROBOTICS.md — 机器人集成方向

> **状态：规划中** — 设计文档编写中，欢迎讨论。

## 设计原则

1. **不碰 core** — 严格遵守上游 AGENTS.md 的"narrow waist"哲学。
   所有机器人特性都是 `optional-skills/holo_robotics/*` 或 `plugins/holo_robotics/*`。
2. **Gazebo 优先** — 教学场景下，永远先在 Gazebo 仿真里跑通，再考虑真机。
3. **Safety by default** — 所有机械臂/底盘指令都过 `check_fn` 安全检查；
   危险动作（如全速旋转、接触式抓取）需要二次确认。
4. **可降级** — 任何机器人 skill 在没有 ROS2 环境时优雅降级（返回"未连接"），不崩溃。

## 拟集成资产

- `~/sagittarius_humble_ws/` — 机械臂完整栈（ROS2 Humble + Gazebo + MoveIt2）
- `~/sagittarius_gazebo/` — Gazebo 仿真（已与 ros2_control 跑通）
- `~/holo_agent/` — 半成品 ROS2 语音 LLM agent
- Spark 机器人 192.168.50.125（Ubuntu 20.04 + ROS1 Noetic）— 待连通
- py-trees-ros 2.4.0（行为树 runtime）— 已装

## 拟建 skill 集合

> 命名约定：`holo_robotics_<category>`

| Skill | 状态 | 描述 |
|---|---|---|
| `holo_robotics_ros2_bridge` | 📋 规划 | 订阅/发布 ROS2 topic、调用 service、发送 action |
| `holo_robotics_gazebo_bridge` | 📋 规划 | 起 Gazebo → 加载 URDF → 仿真/真机切换 |
| `holo_robotics_sagittarius_arm` | 📋 规划 | 封装 MoveIt2 调用（plan + execute、抓取放置、关节运动） |
| `holo_robotics_behavior_tree` | 📋 规划 | 自然语言 → 任务 DAG → py-trees XML |
| `holo_robotics_safety` | 📋 规划 | 统一安全网关：动作分类、限速、二次确认 |

## 风险与缓解

| 风险 | 缓解 |
|---|---|
| 14 万行 core 改坏了 | baseline tag 救命索；任何 PR 必须能 `git checkout v0.16.0-aquarius-baseline` 回到起点 |
| 上游更新快，机器人分支被甩开 | 每 2-4 周 rebase；通用改进 PR 回上游 |
| 机器人指令被学生误触 | safety skill 强约束；Gazebo 仿真环境优先 |
| Gazebo 服务通信超时 | 沿用上游已有的 ros_gz_bridge；如有必要降级为纯 MoveIt 模式 |

## 讨论入口

请发 GitHub Issue 时加 label `robotics`。
设计文档完成后会发 PR 到本仓库的 `dev/robotics-design` 分支。

---

> 最后更新：2026-06-13 · 阶段 0 fork 完成后
