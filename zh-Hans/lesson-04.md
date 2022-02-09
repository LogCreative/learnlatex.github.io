---
layout: "lesson"
lang: "zh-Hans"
title: "逻辑结构"
description: "本课展示了一些基础的格式命令，并将其与含有目次命令和列表的语义格式命令进行比较。"
toc-anchor-text: "逻辑结构"
toc-description: "结构与视觉呈现。"
---

# 逻辑结构

<span
  class="summary">本课展示了一些基础的格式命令，并将其与含有目次命令和列表的语义格式进行比较。</span>

LaTeX 不仅提供了专注于文档逻辑结构的方式，也提供了直接修改外观的方式。大部分情况下，最好使用前者，因为这样在迫不得已的时候就能轻易地复用或更改外观。

## 结构与视觉呈现

我们从一个例子开始，展现 LaTeX 中最常见的逻辑标记命令之一——`\emph`：将文字变成斜体。（印刷界里，为了强调文字经常会这么做。）

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Some text with \emph{emphasis and \emph{nested} content}.

Some text in \textit{italic and \textit{nested} content}.
\end{document}
```

您或许猜得到 `\textit` 能够让文字变成斜体，但是 _只_ 是变成斜体，不能嵌套使用，并且可以看到 `\emph` 能够嵌套使用。也有强调格式不是斜体的情况：比如在幻灯片中，使用颜色来强调会更好。使用逻辑标记的方法后，我们就不用担心编写文档主体时格式设定上的细节问题。

我们会稍后看到[手动设定格式](lesson-11)的相关内容，现在我们为这一段增加一个已经学过的 `\textbf` 命令：让文字变粗的命令。

## 目次命令

或许您使用过字处理器：为了开始一节，多数人的习惯是输入标题文字然后简单地让它变大、变粗，换行继续。在 LaTeX 中使用逻辑标记方式比这种手动格式设定方式 _容易_ 得多——使用 `\section` 命令。它可以直接控制字体变化、纵向间距等等，并且可以让整个文章的格式统一。

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

使用标准的 `article` 配置时，LaTeX 会对节与小节进行标号，并把标题加粗。我们会在[下一课](lesson-05)对改变这种设计进行适当的讲述。

LaTeX 可以将文档分成好几个层级：

- `\chapter` （启用它需要 `\documentclass{book}` 或者
  `\documentclass{report}`）
- `\section`
- `\subsection`
- `\subsubsection`

更进一步来讲，再下一个层级就是 `\paragraph`，但是基本上这一层就会对目次划分得“太细”。（没错，`\paragraph` 是一个目次命令， _不是_ 开始新段落的命令！）

您可能在想对于文档标题应该怎么做。确实有一些特殊的命令来声明一个文档的标题，但并不是所有的文档都会使用标题，所以我们把这个知识放在了对应的[进一步细节页面](lesson-04)中。

## 列表

还有一种很常见的使用逻辑标记情况就是撰写列表。LaTeX 主要内置两种常见的列表类型。

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

注意到我们使用 `\item` 来开始每一项，这样每一种列表中使用的标记或编号就会自动递增。

## 练习

对不同的目次层级进行实验。尝试使用 `\documentclass{report}` 而不是 `\documentclass{article}`，并增加 `\chapter` 命令。现在看起来如何？尝试 `\paragraph`（甚至是 `\subparagraph`）来看看它们是如何工作的：一般情况下，它们并 _不会_ 递增编号。

制作一些列表，并在一个列表中嵌套另一个列表。编号和标记的格式是怎么变化的？你至多可以在标准的 LaTeX 中嵌套四层，毕竟多于四层的嵌套列表一般并不是一个好信号！