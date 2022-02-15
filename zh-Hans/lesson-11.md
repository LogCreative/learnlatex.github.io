---
layout: "lesson"
lang: "zh-Hans"
title: "格式：字体与间距"
description: "本课展示了如何改变文档中元素的间距以及如何向 LaTeX 源代码中添加明确的格式命令。"
toc-anchor-text: "字体与间距"
toc-description: "视觉呈现的文本样式。"
---

# 格式：字体与间距

<span
  class="summary">本课展示了如何改变文档中元素的间距以及如何向 LaTeX 源代码中添加明确的格式命令。</span>

我们已经看到在 LaTeX 中输入一个空行将会另起一个段落，表征为以一个首行缩进开始的段落。

## 段间距

一种比较常见的样式是段落首行没有缩进，但要在段落之间插入空行。这种情形我们可以使用 `parskip` 宏包实现。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage[parfill]{parskip}
\usepackage{lipsum} % 为了填充假文
\begin{document}
\lipsum
\end{document}
```

## 强制断行

大部分情况下，你都不应当在 LaTeX 中强制断行：你几乎只是想另起一段，或者是想在段落之间添加空行（就像我们看到的那样，使用 `parskip` 宏包就可实现）。

只有**很少的**情况下你需要使用 `\\` 来另起一行而不另起一段：

- 在表行的结尾处
- 在 `center` 环境中
- 诗歌（`verse` 环境）

如果不属于这些情况，大多数时候你就**不**应当使用 `\\`。

## 显式添加间距

我们可以使用 `\,` 添加一个小的间距（大概半个空格宽度）。在数学模式中，还可以使用：`\.`，`\:`，`\;`，以及用于添加负间隙的 `\!`。

极少情况下，比如在做一个标题页的时候，你可能需要显式地添加水平间距或垂直间距。对于这种情形，我们可以使用 `\hspace` 和 `\vspace`。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Some text \hspace{1cm} more text.

\vspace{10cm}

Even more text.
\end{document}
```

## 显式设定文本格式

我们在[第 3 课](lesson-03)提到过，大部分情况下使用逻辑结构是更好的。但是有些时候，你可能想要对字体做加粗、斜体、等宽等等的处理。这时就有两种命令可用：一种用于小段，一种用于大段。

对于小段而言，我们可以使用 `\textbf`, `\textit`, `\textrm`, `\textsf`, `\texttt` 以及 `\textsc`。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Let's have some font fun: \textbf{bold}, \textit{italic}, \textrm{roman},
\textsf{sans serif}, \texttt{monospaced} and \textsc{small caps}.
\end{document}
```

对于大段来说，我们使用能够更改字体设置的命令：比如说 `\bfseries` 和 `\itshape`。因为这些命令设置完毕后不会复原，所以我们需要定义一个**组 (group)**用以防止这些设置作用于整个文档。LaTeX 环境是一个组，表格单元格也是一个组，我们也可以使用 `{...}` 来显式地定义一个组。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Normal text.

{\itshape

This text is italic.

So it this: the effect is not limited to a paragraph.

}
\end{document}
```

我们可以采用类似的方式设置字体大小——这些命令也是持续向后影响的设置。这些命令设置相对字体大小：常见的有 `\huge`, `\large`, `\normalsize`, `\small` 以及 `\footnotesize`。请注意要在改回字体大小**之前**结束该段：可以从下面的例子看到我们是怎么显式地添加 `\par`（结束该段）的。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Normal text.

\begin{center}
{\itshape\large Some text\par}
Normal text
{\bfseries\small Much smaller text\par}
\end{center}

\end{document}
```

## 练习

对手动设定格式进行实验：创建一个 `titlepage` 环境，并尝试插入不同的间隙与字体变更。当我们组合地设置字体变更时会发生什么？这和数学模式相比有什么区别？

如果你在结束组之前改变了一个大段的字体大小（可以先对一段设置 `\tiny` 再对下面一段设置 `\huge`），而没有在最后手动添加 `\par` 会发生什么？
