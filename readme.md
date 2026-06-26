# 简兮 · 轻量纯静态工具集

> 简兮简兮，方将万舞。——《诗经・邶风・简兮》

**简兮（Janxi）** 是一个纯静态页面构建的实用工具合集。取名自《诗经》「简兮」，承简约之旨，藏轻盈之态：无后端依赖、无需注册、打开即用、数据不离本地。

---

## 有哪些工具？

| 分类 | 页面 | 一句话说明 |
|------|------|-----------|
| **格式转换** | [file-converter.html](./file-converter.html) | 本地离线文件格式互转（文本 / 文档 / PDF 等） |
| **格式转换** | [pdf-to-ppt-converter.html](./pdf-to-ppt-converter.html) | 将 PDF 页面识别并导出为可编辑 PPTX |
| **效率专注** | [番茄时钟.html](./番茄时钟.html) | 番茄工作法计时器，支持任务与统计 |
| **学习速查** | [ai_learning_path_for_programmers.html](./ai_learning_path_for_programmers.html) | 普通程序员转 AI 的阶段性学习路径 |
| **学习速查** | [data_structures_guide.html](./data_structures_guide.html) | 算法与数据结构完全指南（Python 版） |
| **学习速查** | [algo_tier1.html](./algo_tier1.html) | 算法第一梯队速查手册 |
| **学习速查** | [algo_tier2_3 (1).html](./algo_tier2_3%20(1).html) | 算法第二、三梯队速查手册 |

---

## 快速开始

1. 克隆或下载本仓库到本地。
2. 直接用浏览器打开根目录下的 `index.html`（或任意一个 HTML 文件）。
3. 所有工具均为前端原生实现，无需启动服务器。

> 提示：部分工具依赖 CDN（如 Tailwind、PDF.js、Tesseract 等），首次使用需要联网加载；页面逻辑与数据均在本地运行，不会上传你的文件。

---

## 页面索引

首页已经合并为一个文件，内置三种可切换的皮肤：

- **[index.html](./index.html)**
  - **原版** — 现代 Bento / 玻璃质感风格（默认）
  - **仙侠** — 水墨修真 / 万法玉简风格
  - **杂志** — 杂志 / 编辑排版风格

切换按钮固定在页面顶部，选择后会自动保存到本地（`localStorage`），下次打开仍是该皮肤。

每个皮肤都支持：

- 按分类浏览所有工具
- 点击打开对应工具页面
- 点击「下载」将单个 HTML 文件保存到本地

---

## 项目结构

```
HTML_合集/
├── index.html                          # 统一首页，支持原版 / 仙侠 / 杂志三种皮肤
├── file-converter.html                 # 文件格式转换工具
├── pdf-to-ppt-converter.html           # PDF 转 PPT 工具
├── 番茄时钟.html                        # 番茄工作法计时器
├── ai_learning_path_for_programmers.html
├── data_structures_guide.html
├── algo_tier1.html
├── algo_tier2_3 (1).html
├── designSKILL.md                      # 设计系统参考
└── readme.md                           # 本文件
```

---

## 设计原则

- **纯静态**：所有页面都是单个 HTML 文件，无后端、无数据库。
- **隐私优先**：文件转换、PDF 识别等操作均在浏览器本地完成。
- **即开即用**：双击打开即可使用，无需安装依赖或配置环境。
- **克制简洁**：每个工具只保留最核心的功能，不堆叠无关选项。

---

## 本地使用建议

- 推荐在 Chrome / Edge / Safari 最新版中打开。
- 若使用 `file://` 协议打开，部分浏览器的下载功能可能受限；如遇问题，可临时通过任意本地静态服务器访问，例如：

  ```bash
  python3 -m http.server 8000
  ```

  然后访问 `http://localhost:8000`。

---

## 许可证

本项目为个人学习与小工具集合，页面代码可自由参考与修改。
