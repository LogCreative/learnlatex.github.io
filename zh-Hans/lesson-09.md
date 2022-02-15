---
layout: "lesson"
lang: "zh-Hans"
title: "交叉引用"
description: "本课展示了如何在文档中引用被编号的元素，比如图、表、目次等。"
toc-anchor-text: "交叉引用"
toc-description: "引用图片、表格等。"
---

# 交叉引用

<span
  class="summary">本课展示了如何在文档中引用被编号的元素，比如图、表、目次等。</span>

在编写任何长度的文档时，你可能都会想引用一些编号过的项目，例如：图片、表格或者公式。幸运的是，我们只需要进行些许设置，LaTeX 便能够自动添加正确的编号。

## `\label` 和 `\ref` 机制

为了让 LaTeX 记住文档中的一个位置，你必须先标记它，然后在其他位置引用它。

```latex
\documentclass{article}

\begin{document}
Hey world!

This is a first document.

\section{Title of the first section}

Text of material for the first section.

\subsection{Subsection of the first section}
\label{subsec:labelone}

Text of material for the first subsection.
\begin{equation}
  e^{i\pi}+1 = 0
\label{eq:labeltwo}
\end{equation}

In subsection~\ref{subsec:labelone} is equation~\ref{eq:labeltwo}.
\end{document}
```

这里有两个 `label{...}` 命令，一个在 subsection 之后，一个在 equation 环境内部。它们在最后一句的 `\ref{...}` 命令中一起出现。当你运行 LaTeX 时，它保存 labels 的信息到辅助文件 `(.aux)` 中。对于 `\label{subsec:labelone}` ，LaTeX 知道现在位于 subsection 环境中，所以保存了 subsection 的编号。对于 `\label{eq:labeltwo}`，LaTeX 知道最新关注的环境是 equation，所以它保存了对应 equation 的信息。当你要求引用时，LaTeX 会在辅助文件中得到它。

`subsec:` 和 `eq:` 并不被 LaTeX 使用；实际上，它只是为了记下来在这个标签之前最近在处理什么内容。而明确地写出它们可以帮助你记住标签的含义。

你或许会看到引用的内容在输出的 PDF 文件中显示为两个加粗的问号，**??**。这是由于辅助文件的工作性质所导致，在第一次编译文档时标签尚未保存到辅助文件中。再运行一次 LaTeX，你会得到正确的结果。（通常在你编写文档时，无论如何都会多次运行 LaTeX，所以在实践中，这并不是什么麻烦。）

注意引用前的符号带子（`~`）。你或许不想在 `subsection` 和它的编号之间、或者是 `equation` 和它的编号之间产生断行。放一个符号带子表示 LaTeX 不会在这里产生断行。

## 在哪里加入 `label`

`\label` 命令总是引用在此之前编号过的一个对象：一个章节、一个公式、一个浮动体等。这意味着 `label` 总是添加在你想引用的东西**后面**。特别地，当你创建浮动体时，`\label` 应该跟在 `\caption` 命令后面（或者更好的方式是在里面），并处于浮动体环境内部。

## 练习

尝试添加新的可编号环境（section，subsection，编号的列表）来测试文档，找出让 `\label` 命令成功运行都需要编译几次。

添加一些浮动体，观察将 `\label` 命令放在 `\caption` **前面**而不是后面会发生什么。你能预测出这个结果吗？

如果你把 `\label` 放在 equation 环境的 `\end{equation}` **后面**会发生什么？
