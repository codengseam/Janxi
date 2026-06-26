# 全量 HTML 审计与优化 Spec

> 目标：对简兮工具集 8 个 HTML 文件做功能性/性能/稳定性/美观/适用性审计并逐一修复，critical/high 优先，medium 兼顾。

## 修复优先级 Checklist（按严重度）

### P0 Critical（核心功能失效 / 数据损坏 / 不可用）
- [ ] **data_structures_guide.html L3867** `totalPages=18` → `24`（连带修复键盘导航 L3896-3902、进度条溢出 L3882/3906、面包屑分母 258 等 18 处）
- [ ] **data_structures_guide.html L2816** page-17 缺「下一节」按钮，补 `showPage(18)`
- [ ] **index.html L752/L813** localStorage 裸调用 → try/catch 封装 + 降级
- [ ] **file-converter.html L715-720** 中文 PDF 字体 fallback 失效（helvetica 无中文 → 乱码）→ 可靠字体源或加载失败明确提示/拒绝
- [ ] **pdf-to-ppt-converter.html L9** PDF.js `workerSrc` 未设置 → 设置 worker
- [ ] **pdf-to-ppt-converter.html L494-495** PptxGenJS `w:'100%'` 不支持 → 改英寸数值

### P1 High
- [ ] **index.html** Canvas rAF 永不停止（L782/L807）→ 按 xianxiaActive 启停 + cancelAnimationFrame
- [ ] **index.html** 杂志皮肤缺搜索/筛选/空状态（L536-571, L706-742）→ 补齐
- [ ] **index.html** `innerHTML +=` 循环累加（L611/667/713/733）→ 数组 join 一次性赋值
- [ ] **file-converter.html L858-859** 进度回调全量重渲染 → 局部更新进度条
- [ ] **file-converter.html L269/917-919** 文件名 XSS → 统一 escapeHtml
- [ ] **file-converter.html L949-960** 下载 revoke 过早 → 延迟 revoke + 区分 AbortError
- [ ] **file-converter.html L502/826-828** MOBI 读写无效 → 移除/明确不支持
- [ ] **file-converter.html L220** crypto.randomUUID 兼容 → polyfill
- [ ] **pdf-to-ppt-converter.html L480-510** ocrResults[i] undefined 崩溃 → 长度校验
- [ ] **pdf-to-ppt-converter.html L380** canvas 引用未释放 → 移除字段 + 清零释放
- [ ] **pdf-to-ppt-converter.html L140** 50MB 限制未实现 → file.size 校验
- [ ] **番茄时钟.html L4121-4147** 完成态 1s 窗口双倍计数 bug → isCompleting 拦截
- [ ] **番茄时钟.html L4081-4090** setInterval 递减漂移 → 墙钟时间
- [ ] **番茄时钟.html L3973/4124/4131** pomodoroCount 未持久化 → 纳入 state
- [ ] **番茄时钟.html L3733-3736** saveState 无 try/catch → 包裹+降级
- [ ] **番茄时钟.html L2836-2842 + L4316-4318** 导航 div 不可键盘 + 胶囊无触屏拖拽
- [ ] **data_structures_guide.html L871-878** OpenHashMap.put 墓碑 bug
- [ ] **data_structures_guide.html L1688-1702** Trie.delete 未维护 count
- [ ] **data_structures_guide.html L220-248/L39-47** 侧栏不可键盘 + 移动端不可用

### P2 Medium（a11y / 美观 / 稳定性加固 / 一致性）
- [ ] 全文件统一：`prefers-reduced-motion`、`aria-label`/`role`/焦点管理、装饰 SVG `aria-hidden`、对比度达标
- [ ] **algo_tier1.html / algo_tier2_3 (1).html** 语法高亮 + 字体加载 + 复制按钮 + TOC 锚点 + 语义化标题 + 裸 `<` 转义
- [ ] **ai_learning_path_for_programmers.html** 卡片 div+onclick 键盘可达 + aria-expanded/pressed + 文档结构/变量回退
- [ ] **data_structures_guide.html** 算法示例次要 bug：BIT 建树 O(n)、动态线段树缺 query、LCA O(1)、空堆/空队判空、heap_sort/最大矩形副作用、hljs 守卫
- [ ] **番茄时钟.html** modal dialog 语义 + ESC + 焦点陷阱；拖拽 clamp 视口；fullscreenchange 同步
- [ ] **file-converter.html** EPUB 命名空间解析、空文件校验、accept 属性、进度条 role
- [ ] **pdf-to-ppt-converter.html** file 类型双校验、isProcessing 防并发、scale 动态、错误信息含 error.message、textarea label

## 执行方式
- 并行 fix agent 按文件分组，每个 agent 拿到该文件精确行号清单，做**最小化定向修复**，不重写整文件、不改动无关代码、保留既有可用逻辑。
- 完成后专家团（功能/性能/a11y/美观）复检，loop 修复残余问题直至无 critical/high。
