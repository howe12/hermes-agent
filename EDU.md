# 🎓 EDU.md — 教育方向

> **状态：规划中** — 设计文档编写中。

## 设计原则

1. **以学生为中心** — Agent 既能"教"也能"练"。
   知识讲解 + 苏格拉底式提问 + 错例讲解 + 跟机器人演示打通。
2. **复用上游** — Honcho 用户建模、FTS5 会话检索、autonomous skill creation 都是上游已实现的，
   我们只是接你自己的 7 门课程。
3. **不重复造轮子** — RAG 用上游的 `memory` 子系统，skill 体系用上游的 `skills/`。

## 拟建教学资产

### 课程 RAG 知识库

- 来源：`~/Music/leo_class/`（7 门课）
  - `sagittarius_class/`（机械臂课）
  - `spark_install_class/`（Spark 装机课）
  - `spark_navigation2_class/`（Spark 导航课）
  - `leo_navigation2_class/`（通用 Nav2 课）
  - `leo_2d_slam_class/`（2D SLAM 课）
  - `leo_vision_class/`（视觉课）
  - `leo_sensor_class/`（传感器课）
- 工具：本地 ChromaDB（CPU 跑得动），嵌入用 Qwen3-Embedding-8B（API）
- 索引粒度：每门课独立索引；支持"按章节""按难度""按机器人型号"检索

### 拟建 skill 集合

> 命名约定：`holo_edu_<category>`

| Skill | 状态 | 描述 |
|---|---|---|
| `holo_edu_course_rag` | 📋 规划 | 7 门课统一检索接口 |
| `holo_edu_student_profile` | 📋 规划 | 跟踪学过什么、错在哪里、当前进度（基于上游 Honcho） |
| `holo_edu_curriculum_orchestrator` | 📋 规划 | 根据学生画像自动生成下一节课 |
| `holo_edu_teaching` | 📋 规划 | 苏格拉底式提问、错例讲解、随堂练习、自动批改 |
| `holo_edu_web_portal` | 📋 规划 | 极简 Web UI，学生能在浏览器里看进度、看机器人状态 |

## 教学闭环（"越用越聪明"的具象化）

```
学生提问
  ↓
agent 用 holo_edu_course_rag 检索课程库
  ↓
讲解 + 提问（如果学生答错）
  ↓
agent 触发 holo_robotics_* skill 让真实机械臂演示
  ↓
学生重做 → 错例进 holo_edu_student_profile
  ↓
agent 评估 → 推荐下一节课
  ↓
下一次会话 agent 自动调用 holo_edu_curriculum_orchestrator 排课
  ↓
"越用越聪明"实现
```

## 风险与缓解

| 风险 | 缓解 |
|---|---|
| 课程 RAG 检索不准 | 先手工标 100 个 Q&A 验证集；每周回归 |
| 学情画像不准确 | 用上游 Honcho 的 dialectic user modeling，不自己造 |
| 学生滥用 agent 抄答案 | 教学 skill 强制"先讲后问"模式；不允许直接给完整代码 |
| 课程版本与代码版本脱节 | 每门课配一个 `version` 字段；agent 引用时标注时间 |

## 讨论入口

请发 GitHub Issue 时加 label `education`。

---

> 最后更新：2026-06-13 · 阶段 0 fork 完成后
