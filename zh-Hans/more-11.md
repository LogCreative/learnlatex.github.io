---
layout: "lesson"
lang: "zh-Hans"
title: "更多：格式：字体与间距"
description: "本课展示如何对于单一段落抑制段落缩进。"
toc-anchor-text: "更多：格式：字体与间距"
---


## 对于单一段落抑制缩进

若您想抑制单一段落的缩进，那可以使用 `\noindent`。这应当 _很_ 少被使用。大部分情况下，您应该让 LaTeX 自动处理这些缩进。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
One small paragraph, which we have filled out a little to make sure you can
see the effect here!

One small paragraph, which we have filled out a little to make sure you can
see the effect here!

\noindent  One small paragraph, which we have filled out a little to make sure
you can see the effect here!
\end{document}
```
