---
layout: "lesson"
lang: "zh-Hans"
title: "使用宏包和定义来扩展 LaTeX"
description: "本课展示了如何根据需要扩展 LaTeX、通过宏包和定义改变其布局以及自行定义命令。"
toc-anchor-text: "扩展 LaTeX"
toc-description: "使用宏包、定义命令。"
---

# 扩展 LaTeX

<span
  class="summary">本课展示了如何根据需要扩展 LaTeX、通过宏包和定义改变其布局以及自行定义命令。</span>

声明一个文档类后，你在 LaTeX 导言区中可以通过添加一个或多个「宏包（package）」来修改相关功能。宏包可以：

- 改变 LaTeX 某些部分的功能
- 向 LaTeX 添加新的命令
- 更改文档的设计

## 改变 LaTeX 的工作方式

因为 LaTeX 内核（kernel）对于用户来说，自定义是很受限制的，所以需要使用扩展包来实现一些常见功能。第一件事就是在 LaTeX 中如何改变对于特定语言的排版方式（断字、标点符号、引文、本地化……）。因为不同的语言有不同的规则，所以告诉 LaTeX 要使用哪种规则是很重要的。这可以通过 `babel` 宏包来处理。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

%\usepackage[french]{babel}

\usepackage[width = 6cm]{geometry} % 强制进行断字

\begin{document}

This is a lot of filler which is going to demonstrate how LaTeX hyphenates
material, and which will be able to give us at least one hyphenation point.
This is a lot of filler which is going to demonstrate how LaTeX hyphenates
material, and which will be able to give us at least one hyphenation point.

\end{document}
```

尝试取消注释加载 `babel` 宏包的那一行（显然这一行带有误导性），然后观察排版效果。（标准断字规则是英语(美国)。）

根据涉及语言的不同，`babel` 宏包不仅影响着断字。如有需要，我们给出了[更多细节](more-06)。

## 改变设计

调整某些独立于文档类方面的设计通常是有用的。最常见的是更改页边距。刚刚就在上面的例子中使用了 `geometry` 宏包，让我们现在再来看一个专门关于页边距的例子。

```latex
\documentclass{book}
\usepackage[T1]{fontenc}
\usepackage[margin=1in]{geometry}

\begin{document}
Hey world!

This is a first document.


% ================
\chapter{Chapter One}
Introduction to the first chapter.


\section{Title of the first section}
Text of material in the first section

Second paragraph.

\subsection{Subsection of the first section}

Text of material in the subsection.


% ================
\section{Second section}

Text of the second section.

\end{document}
```

和不加载 `geometry` 宏包相对比，你应该能够看到其效用。

## 添加新功能

LaTeX 的优势之一就是拥有上千个宏包可供挑选，包括编写数学公式的、提供超链接功能的、复杂颜色调整的……在后续的课程中我们会看到更多常见的宏包。

## 定义命令

有时你需要对文档设定一些特定的命令。或许是一些不能从现有宏包中找到的命令，或许只是一个需要重复输入的常见表达式。

下面的例子展示了一个对关键词应用特定样式的命令。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\newcommand\kw[1]{\textbf{\itshape #1}}

\begin{document}

Something about \kw{apples} and \kw{oranges}.

\end{document}
```

在定义中，`[1]` 表示参数个数（这里只有一个），`#1` 表示提供的第一个参数（在这个例子中，指的是 `apples` 或 `oranges`）。你最多可以设置 9 个参数，但一般情况下最好只有一个参数，有时甚至不需要设置任何参数。

在排版一篇文档的过程中，定义命令的作用不仅在于减少输入量，还有助于将格式信息分离出来。如果你准备对关键词采用不同的格式，只需要调换成不同的定义即可，而不是对整篇文档从头到尾地编辑一遍。这里为了设定彩色加载了 `xcolor` 宏包，在格式上把加粗改成了蓝色。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage{xcolor}

\newcommand\kw[1]{\textcolor{blue}{\itshape #1}}

\begin{document}

Something about \kw{apples} and \kw{oranges}.

\end{document}
```

注意，定义太多的命令或者定义太多的参数，都会因使用了不常见的语法而让源文件变得不易读。需要谨慎使用对特定文档定义的命令。

## 练习

尝试使用其他欧洲语言撰写一些文段，并观察 `babel` 是怎么影响断字的：你可以从网上搜集一些文段，并猜测正确的设置应该是什么。

尝试更改 `geometry` 例子中的页边距。你可以通过一个逗号分隔列表来单独地设定 `top`, `bottom`, `left`, `right` 四种边距。

尝试加载 `lipsum` 宏包以向你的文档中添加 `\lipsum` 命令。你能否猜出为什么对于制作例子来说这个宏包特别有用？（译者注：在 `ctex` 启用时可以使用 `zhlipsum` 宏包，并通过 `\zhlipsum` 命令生成中文假文）

尝试改变 `\kw` 的定义以实现一种不同的格式。