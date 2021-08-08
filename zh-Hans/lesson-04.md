---
layout: "lesson"
lang: "zh-Hans"
title: "逻辑结构"
description: "本课展示了一些基础的格式化命令，并将其与含有节次命令和列表的语义格式化进行比较。"
toc-anchor-text: "逻辑结构"
toc-description: "结构与视觉呈现。"
---

# 逻辑结构

<span
  class="summary">本课展示了一些基础的格式化命令，并将其与含有节次命令和列表的语义格式化进行比较。</span>

LaTeX 不仅提供了专注于文档逻辑结构的方式，也提供了直接修改外观的方式。大部分情况下，最好使用关注于结构的方式，这样迫不得已的时候就能容易地复用或更改外观。

## 结构与视觉呈现

我们从一个例子开始，展示 LaTeX 中最常见的逻辑标记命令之一——`\emph`：将某文段变成斜体。（为了强调印刷界经常这么做。）

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Some text with \emph{emphasis and \emph{nested} content}.

Some text in \textit{italic and \textit{nested} content}.
\end{document}
```

您或许猜得到 `\textit` 能够让文段变成斜体但是只能变成斜体，而对于嵌套的情况不奏效；并且可以看到 `\emph` 能够嵌套使用。当然，也有强调的格式并不是斜体的情况：比如在幻灯片中，使用颜色来强调是一种更好的方式。使用逻辑标记方法我们就不用担心编写文档主体时在格式设定上的细节问题。

我们会稍后看到 [手动格式化](lesson-11) 的相关内容，现在我们为这一段增加一个已知的 `\textbf` 命令：让文段变粗的命令。

## Sectioning commands

You probably have used a word processor, where  to start a section most people
enter the title text then simply make it bigger and bold, and follow it with a
new line. In LaTeX, using logical markup is actually _easier_ than doing the
formatting by hand; we can use the `\section` command. This handles the font
changes, vertical space, etc., and keeps the output uniform throughout the
document.

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Hey world!

This is a first document.

\section{Title of the first section}

Text of material in the first section

Second paragraph.

\subsection{Subsection of the first section}

Text of material in the subsection.

\section{Second section}

Text of the second section.

\end{document}
```

Using the standard `article` setup, LaTeX numbers the sections and subsections
and includes the titles in boldface. We'll think a bit about changing design [in
the next lesson](lesson-05).

LaTeX can divide up documents into quite a few levels

- `\chapter` (启用它需要 `\documentclass{book}` 或者
  `\documentclass{report}`)
- `\section`
- `\subsection`
- `\subsubsection`

We can go further: the next one 'down' is `\paragraph`, but almost always that's
too much 'detail' in sections. (Yes, `\paragraph` is a section command, _not_ a
way to start a new paragraph!)

You might wonder about the title of a document. There are some special
commands for that, but not all documents use them, so we've
[covered that in the parallel extra lesson](more-04).

## Lists

The other very common place you'll want logical markup is writing lists.
There are two common types of list built in to LaTeX.

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}

Ordered
\begin{enumerate}
  \item An entry
  \item Another One
  \item Wow! Three entries
\end{enumerate}

Unordered
\begin{itemize}
  \item An entry
  \item Another One
  \item Wow! Three entries
\end{itemize}

\end{document}
```

Notice that we use `\item` to start each entry, and that the marker used  for
each type of list is added automatically.

## Exercises

Experiment with different sectioning levels. Try using `\documentclass{report}`
instead of `\documentclass{article}` and adding `\chapter` commands. How
do they look? Try out `\paragraph` and (even) `\subparagraph` to see they work:
by default, they _don't_ add numbers.

Make some lists, and nest one list inside another. How does the format of the
numbers or markers change? You can only go to four levels with standard LaTeX,
but more than four nested lists tends to be a bad sign anyway!
