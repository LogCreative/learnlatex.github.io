---
layout: "lesson"
lang: "zh-Hans"
title: "更多：交叉引用"
description: "本课展示了如何通过加载 hyperref 宏包为交叉引用添加链接。"
toc-anchor-text: "更多：交叉引用"
---

## 为交叉引用添加链接

通过 `hyperref` 宏包，你可以为交叉引用添加超链接。在大多情况下，`hyperref` 应该在导言区其他宏包之后加载。

```latex
\documentclass{article}
\usepackage[hidelinks]{hyperref}
\begin{document}

\section{Introduction}
Some exciting text with a reference~\ref{sec:next}.

\section{Next thing}
\label{sec:next}

More text here.
\end{document}
```

我们选择了让链接和正常文本颜色相同，尝试删除 `hidelinks` 看看是为什么！
