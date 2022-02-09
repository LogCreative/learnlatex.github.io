---
layout: "lesson"
lang: "zh-Hans"
title: "更多：使用宏包和定义来扩展 LaTeX"
description: "本课对于宏包加载提供了更多的细节，展示了用以语言选择的 babel 宏包，以及自定义命令的更多信息。"
toc-anchor-text: "更多：使用宏包和定义来扩展 LaTeX"
---

## 加载多个宏包

`\usepackage` 命令接受宏包逗号分隔列表作为参数，所以您可以在一行中加载多个宏包：比如，`\usepackage{color,graphicx}`。如果您向其传递参数，那么它们就会向列表中所有的宏包传递。因为如果分别加载的话，注释掉宏包也会更简单，所以我们会保持一行加载一个宏包的这个习惯。

## `babel` 宏包

在 [主课](lesson-06) 中我们展示了用来选择不同断字模式的 `babel` 宏包。取决于使用的不同语言，它可能不仅做了断字这一件事。比如，在德语中，它不仅提供了创建“软”断字符的一些简写，还提供了一种不需要德式键盘来输入元音变音的快速方法。并且可以注意到，一般使用 `\tableofcontents` 生成的 _目录_ 节标题已经变成了德语 Inhaltsverzeichnis。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage[ngerman]{babel} % 注意选项是 'ngerman'

\begin{document}

\tableofcontents

\section{"Uber "Apfel und Birnen}

\subsection{Äpfel}
Äpfel sind rot.

\subsection{Birnen}
Birnen sind gelb.


\end{document}
```

其他的语言设置会改变设计：比如，在传统的法语排版中，一些标点比如 `:` 前会有一个空格。如果您加载 `babel` 时使用 `french` 选项的话，这个空格就会被自动添加。

## 全局选项

有些时候，您想要将一个选项传递给加载的所有宏包。这可以通过在 `\documentclass` 这一行添加选项实现：每一个宏包都可以“看到”这个选项列表。所以为了将语言选项传递给所有宏包，我们可以使用：

```latex
\documentclass[ngerman]{article} % 注意选项是 'ngerman'
\usepackage[T1]{fontenc}

\usepackage{babel}

\begin{document}

\tableofcontents

\section{"Uber "Apfel und Birnen}

\subsection{Äpfel}
Äpfel sind rot.

\subsection{Birnen}
Birnen sind gelb.

\end{document}
```

## 更多的定义

`\newcommand` 允许命令可以最多拥有 9 个参数，其中第 1 个可以被设定为可选参数。

拿主课中的例子来说，我们可以将颜色选项设为可选的，并默认为 blue。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage{xcolor}

\newcommand\kw[2][blue]{\textcolor{#1}{\itshape #2}}

\begin{document}

Something about \kw{apples} and \kw[red]{oranges}.

\end{document}
```

可选参数使用 `[]` 分隔，如果被省略了，就会使用定义中指定的默认值。

## `\NewDocumentCommand`

LaTeX 的 2020 年 10 月更新后，一个扩展的定义系统可以使用了。为兼容性起见，对于老版本的 LaTeX 将会通过加载 `xparse` 宏包使用这个系统。

我们可以通过使用 `\NewDocumentCommand` 再次实现上面的例子。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage{xparse} % 只在老版本的 LaTeX 中需要
\usepackage{xcolor}

\NewDocumentCommand\kw{O{blue} m}{\textcolor{#1}{\itshape #2}}

\begin{document}

Something about \kw{apples} and \kw[red]{oranges}.

\end{document}
```

和 `\newcommand` 一样，`\NewDocumentCommand` 接受正被定义的命令名称（这里是 `\kw`），在定义体中 `#1` 到 `#9` 用来使用参数。而差别在于参数是如何被指定的。 

和 `\newcommand` 只需要指定含有多少个参数不同，`\NewDocumentCommand` 可选地提供第一个参数默认值之后，每一个参数都会被一个字母指定，所以一个含有两个参数的命令就会被指定为 `{mm}` 而不是 `[2]`。这样虽然可能会冗余一些，但可以允许更多的命令形式被定义。在此我们仅给出了一个简单的例子，第一个参数可选，默认为 blue（`O{blue}`，optional），第二个参数必需（`m`，mandatory）。
