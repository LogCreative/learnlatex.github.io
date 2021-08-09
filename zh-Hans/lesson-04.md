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

## 节次命令

或许你使用过字处理器：为了开始一节，多数人的习惯是输入标题文字然后简单地让它变大、变粗，换行继续。在 LaTeX 中用逻辑标记方式比这种手动格式化实际上更容易：我们可以使用 `\section` 命令。它可以直接控制字体变化、纵向间距等等，并且可以让整个文章的格式统一。

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

使用标准的 `article` 配置，LaTeX 会对节与小节进行标号，并把标题加粗。我们会在 [下一节](lesson-05) 对改变这种设计进行适当的讲述。

LaTeX 可以将文档分成好几个层级：

- `\chapter` (启用它需要 `\documentclass{book}` 或者
  `\documentclass{report}`)
- `\section`
- `\subsection`
- `\subsubsection`

我们可以说的更多一点，下一个层级就是 `\paragraph`，但是基本上这一层会对节次划分得过多。（没错，`\paragraph` 是一个节次命令，而 _不是_ 开始新段落的命令！）

您可能在想对于文档标题该怎么做。确实有一些特殊的命令来声明一个文档的标题，但并不是所有的文档都会使用它，所以我们把这个知识放在了对应的 [拓展课程](lesson-04) 中。

## 列表

还有一种很常见的使用逻辑标记的情况就是撰写列表。LaTeX 主要内置两种常见的列表类型。

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

注意到我们使用 `\item` 来开始每一项，这样每一种列表中使用的标记或编号就会被自动增加。

## Exercises

Experiment with different sectioning levels. Try using `\documentclass{report}`
instead of `\documentclass{article}` and adding `\chapter` commands. How
do they look? Try out `\paragraph` and (even) `\subparagraph` to see they work:
by default, they _don't_ add numbers.

Make some lists, and nest one list inside another. How does the format of the
numbers or markers change? You can only go to four levels with standard LaTeX,
but more than four nested lists tends to be a bad sign anyway!
