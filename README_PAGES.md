# 📚 aquarius-psyche Pages 顶层设计

> **目的**：让 4 个（未来 10+）教学页面保持一致的导航结构，避免"页面一多就乱套"。

---

## 🎯 核心原则

**骨架先行 · 肌肉后填**

- 导航结构（顶部 nav / 浮动按钮 / 进度条）= **骨架**，一定下来就不轻易改
- 具体页面内容（章节、图表、代码）= **肌肉**，可以频繁改

未来加新附录就像加一根新骨头——**不动现有结构**。

---

## 🏛️ 4 层跳转体系

每篇页面都有 **4 层跳转入口**，确保任何位置都能找到路：

| 层 | 元素 | 位置 | 跳转能力 |
|---|------|------|----------|
| **L1 顶部** | `nav.holo-topnav` sticky 顶部 | 滚动时**永远可见** | 4 tab 一键切页 |
| **L2 浮动** | `a.holo-fab` 右下角 2 个 | 滚动时**永远可见** | ↑ 顶部 / 📚 目录 |
| **L3 页内** | footer 链接 | 页面底部 | 4 页 + 1 目录 |
| **L4 进度** | `div.holo-progress` 顶部 2px | 实时 | 阅读进度反馈 |

**5 个总入口**（每个页面都能直达）：
1. 📖 主阅读手册 `./`
2. 📎 附录 A `./docs/index.html`
3. 📎 附录 B `./docs/appendix-b-skills.html`
4. 📎 附录 C `./docs/appendix-c-sharing.html`
5. 📚 目录 `./toc.html`

---

## 🎨 颜色编码体系

一眼看出"这是哪类内容"：

| 颜色 | 主题 | 现有页 | CSS var |
|------|------|--------|---------|
| 🔵 蓝 `#1e6091` | 主线 / 入门 | 主阅读手册 / 附录 A | `--accent` |
| 🟠 橙 `#a04a1d` | 持续学习 / 自动化 | 附录 B | `--warm` |
| 🟣 紫 `#5b21b6` | 工程 / 部署 | 附录 C | `--purple` |
| 🟢 绿 `#1f6b3c` | 测试 / QA | (未来) | `--ok` |
| 🔴 红 `#8e2a3b` | 安全 / 警告 | (未来) | `--q` |

**新附录默认用蓝/橙/紫之一**，特殊场景用绿/红。

---

## 🗂️ 当前页面布局

```
/
├── index.html                            📖 主阅读手册（蓝）
├── toc.html                              📚 总目录（紫主题） ★ 新
├── docs/
│   ├── index.html                        📎 附录 A · FTS5（蓝）
│   ├── appendix-b-skills.html            📎 附录 B · 技能沉淀（橙）
│   ├── appendix-c-sharing.html           📎 附录 C · 多实例共享（紫）
│   ├── appendix-d-XXX.html               (待定)
│   └── ...
└── README_PAGES.md                       ★ 本文档
```

**`toc.html` 是顶层目录**，列 4 张卡片（每页一张），每张卡内是该页所有章节锚点。

---

## 🛠️ 加新附录的标准流程（附录 D / E / F...）

### 第 1 步：复制一份"模板骨架"

```bash
# 在 docs/ 下新建空文件
touch docs/appendix-d-XXX.html
```

### 第 2 步：跑注入脚本

```bash
python3 inject_nav.py
# 脚本会自动为新页加 holo-topnav + holo-fab + holo-progress
# 编辑脚本里的 PAGES dict 加一行即可
```

### 第 3 步：编辑 `toc.html` 加新卡片

只改 `toc.html` 里 `<div class="pages-grid">` 的最后一个 `<article class="page-card">` 之后追加一张新卡。

### 第 4 步：commit + push

```bash
git add docs/appendix-d-XXX.html toc.html
git commit -m "feat(pages): add Appendix D - <topic>"
git push origin gh-pages
```

**其他 4 个页面不用改**——这就是"骨架不动"的好处。

---

## 🔧 工具脚本说明

### `inject_nav.py`

- 自动为 4 个页面注入统一导航
- 用 Python 写**只用一次**——如果未来要重跑，只改 `PAGES` dict 即可
- 不会重复注入（检测到 `class="holo-topnav"` 就跳过）
- 写在仓库根目录，临时性质

**注意**：这个脚本**不**进 gh-pages 分支（用户已经体验过导航，git push 时会把它排除掉）。

---

## 📋 跳转体系验证清单

- [x] 4 个页面都有顶部 nav
- [x] 当前页 nav tab 高亮
- [x] 4 个页面都有 2 个浮动按钮（顶部 / 目录）
- [x] 4 个页面都有进度条
- [x] 4 个页面都有 footer 跳转链接
- [x] 5 个总入口可互相跳
- [x] 远端 HTTP 200 验证

---

## ⏭️ 未来 TODO

- [ ] 暗色模式开关（豪华派留下未做）
- [ ] 章节折叠/展开
- [ ] 阅读历史记录（localStorage）
- [ ] 附录 D · 待定主题
- [ ] 附录 E · 待定主题
