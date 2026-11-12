# 🚀 Space Quiz

> 一个零依赖的单页太空知识测验 · A dependency-free, single-page space exploration quiz.

十道单选题，选完立刻告诉你对错和一条科普小知识，最后按得分给出不同的"任务评价"。

**在线试玩**：<https://qing5122.github.io/space-quiz/>（首次在 Settings → Pages 里开启后生效）

---

## 快速开始

不需要安装任何东西，也没有构建步骤。

1. **直接玩**：双击 `index.html`，浏览器就会打开。
2. **想用 `localhost` 打开**（可选，方便以后加网络功能）：

   ```bash
   # 在仓库根目录执行，然后访问 http://localhost:8000
   python -m http.server 8000
   ```

## 项目结构

```
space-quiz/
├── index.html                      # 整个应用：样式 + 题目数据 + 交互逻辑
├── README.md
└── .github/
    └── copilot-instructions.md     # 写代码要遵守的项目约定
```

页面是**完全自包含**的：没有框架、没有 npm 包、没有 CDN 外链，断网也能玩。所以任何人都可以下载一个 `index.html` 就跑起来。

## 代码地图

全部逻辑在 `index.html` 底部的 `<script>` 里：

| 位置 | 作用 |
| --- | --- |
| `questions` 数组 | 题库，每题含 `question` / `answers` / `correct` / `fact` |
| `renderQuestion()` | 按当前题号生成选项按钮 |
| `chooseAnswer()` | 判分、上色、显示科普、推进进度条 |
| `showResults()` | 结算页：emoji 评价、分数、"再玩一次" |
| `restart()` | 复位并重新开始 |
| `currentQuestion` / `score` / `answered` | 仅有的三个状态变量 |

## 怎么加一道题

在 `questions` 数组里追加一项，格式如下（`correct` 是**从 0 开始**的答案下标，上面例子中 1 代表第二项 `Sputnik 1`）：

```js
{
  question: "Which planet is known as the Red Planet?",
  answers: ["Venus", "Mars", "Jupiter", "Mercury"],
  correct: 1,
  fact: "Mars looks red because of iron oxide dust on its surface."
}
```

三个容易踩的坑：

1. `correct` 下标要跟着 `answers` 的实际顺序走，改选项顺序时要一起改；
2. 题量变了，页面上的"第 1 题，共 10 题"和进度条上限也要改——它们目前写死在 HTML 里（`Question 1 of 10`、`aria-valuemax="10"`）；
3. 答案文字是用 `textContent` 渲染的，所以题目数据里不要塞 HTML 标签。

## 设计约定

- 颜色统一用 `:root` 里的 CSS 变量，暗色模式在 `@media (prefers-color-scheme: dark)` 里覆盖同名变量；
- 加动画时要考虑 `prefers-reduced-motion: reduce`；
- 选项和按钮用原生 `<button>`，保留键盘焦点可见、已答选项禁用、`aria-live` 提示和进度条的 `aria-valuenow`；
- 不引入框架、依赖、远程资源或服务器。

## 路线图

- [ ] [#1 保存个人最高分](https://github.com/qing5122/space-quiz/issues/1)（localStorage）
- [ ] [#2 五题速通模式](https://github.com/qing5122/space-quiz/issues/2)
- [ ] [#3 结果页回顾错题](https://github.com/qing5122/space-quiz/issues/3)

## 许可

仓库暂未指定开源许可证。教程/学习用途可直接参考；如需再分发，请先开一个 issue 说明。
