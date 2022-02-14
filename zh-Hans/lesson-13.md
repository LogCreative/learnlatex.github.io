---
layout: "lesson"
lang: "zh-Hans"
title: "组建更长的文档"
description: "本课展示了如何使用 LaTeX 将源代码分割成更小、更好管理的文件，并展示这将如何让长文档的构建变得更容易且更快捷。"
toc-anchor-text: "组织源代码"
toc-description: "以可控方式管理代码。"
---

# 组建更长的文档

<script>
preincludes = {
 "pre0": {
    "pre1": "front.tex",
    "pre2": "pref.tex",
    "pre3": "chap1.tex",
    "pre4": "chap2.tex",
    "pre5": "append.tex",
    "pre6": "frontcover.tex",
    "pre7": "dedication.tex",
    "pre8": "copyright.tex",
    "pre9": "backcover.tex",
   }
}
</script>

<span
  class="summary">本课展示了如何使用 LaTeX 将源代码分割成更小、更好管理的文件，并展示这将如何让长文档的构建变得更容易且更快捷。</span>

当您编写长文档的时候，很可能想将源代码分割成多个文件。比如，很常见的做法是，创建一个 `main` 或 `root` 文件，然后每一章创建一个源文件（对于一本书或者一篇论文），或者每一个长节创建一个源文件（对于一篇长文档）。

## 组织源代码

LaTeX 允许我们以可控的方式分割源代码。对此，有两个很重要的命令：`\input` 和 `\include`。我们可以使用 `\input` 让文件“看起来就是输入在这里一样”，所以（几乎）可以用于任何文档。`\include` 命令仅对章节有用：从新页开始并做一些内部调整。但它有一个很大的优势：允许我们选择输入哪些章节，这样就可以不用排印全文而只需要排印这一部分的内容。

一篇长文档可能因此看起来跟下面一样：

<!-- pre0 {% raw %} -->
```latex
\documentclass{book}
\usepackage[T1]{fontenc}
\usepackage{biblatex}
\addbibresource{biblatex-examples.bib}

\title{A Sample Book}
\author{John Doe \and Joe Bloggs}

\IfFileExists{\jobname.run.xml}
{
\includeonly{
  front,
%  chap1,
  chap2,
%  append
  }
}
{
% 包含全部文件来生成所有的 aux 文件
}

\begin{document}
\frontmatter
\include{front}

% =========================
\mainmatter
\include{chap1}
\include{chap2}
\appendix
\include{append}

% ========================
\backmatter
\printbibliography
\newpage
\input{backcover}
\end{document}
```
<!-- {% endraw %} -->

我们将在下文来考察这个文件中的多种用法。（所有的支持文件附于页面结尾）

## 使用 `\input`

`\input` 命令适合于**不**独立于章节的长文件片段。例如，我们用它来分隔前封面和后封面，来保持主文件的简短清晰，并可以在其他文档中复用。我们也用这个命令来分割书的起始“非章节”目次：比如前言。这也是为了保持主文件的结构清晰。

## 使用 `\include` 和 `\includeonly`

对于章节而言，`\include` 很有用，因此我们对于每一个整章都使用了这个命令。我们通过使用 `\includeonly` 来选择哪一章会被实际排印出来（这个命令接受逗号分隔的文件列表）。当您使用 `\includeonly` 时，可以缩短排版出来的文件长度并制作出一个“选择后的” PDF 用于校对。而且，`\includeonly` 的核心优势在于 LaTeX 会使用其他所有包含进来文件的 `.aux` 辅助文件用于章节间的交叉引用。

## 创建目录

`\tableofcontents` 命令使用目次命令的信息来制作目录。它有着以 `.toc` 为后缀的专门辅助文件，所以您可能需要运行 LaTeX 两次以解析这些信息。目录将会从目次标题自动生成。还有一些类似的命令比如 `\listoffigures` 以及 `\listoftables`，将根据浮动体环境的标题分别生成以 `.lof` 和 `.lot` 后缀的文件。

## 将文档分割成部分

`\frontmatter`, `\mainmatter` 和 `\backmatter` 命令影响着格式。例如，`\frontmatter` 改变页码为罗马数字。`\appendix` 命令将改变章节编号为 `A`, `B` ……——所以 `\appendix` 后的第一章被称为 `Appendix A`。

## 练习

对演示文档的基本结构进行实验，尝试添加或删除 `\includeonly` 中的条目并查看效果。

添加一些浮动体并输出图目录和表目录。如果使用本地 LaTeX 编译，您能看出来 LaTeX 编译了几次吗？（在线版本会在后台自动重复运行 LaTeX，所以额外的编译次数可能看起来并没有那么明显。）

----

### front.tex
<!-- pre1 {% raw %} -->
```latex
\input{frontcover}
\maketitle
\input{dedication}
\input{copyright}
\tableofcontents
\input{pref}
```

#### pref.tex
<!-- pre2 {% raw %} -->
```latex
\chapter{Preface}
The preface text. See \cite{doody}.
```
<!-- {% endraw %} -->

#### chap1.tex
<!-- pre3 {% raw %} -->
```latex
\chapter{Introduction}
The first chapter text.
```
<!-- {% endraw %} -->

#### chap2.tex
<!-- pre4 {% raw %} -->
```latex
\chapter{Something}
The second chapter text.
```
<!-- {% endraw %} -->

####  append.tex
<!-- pre5 {% raw %} -->
```latex
\chapter*{Appendix}
The first appendix text.
```
<!-- {% endraw %} -->

#### frontcover.tex
<!-- pre6 {% raw %} -->
```latex
\begin{center}
The front cover
\end{center}
```
<!-- {% endraw %} -->

#### dedication.tex
<!-- pre7 {% raw %} -->
```latex
\begin{center}
\large
For \ldots
\end{center}
```
<!-- {% endraw %} -->

#### copyright.tex
<!-- pre8 {% raw %} -->
```latex
\begin{center}
Copyright 2020 learnlatex.
\end{center}
```
<!-- {% endraw %} -->

#### backcover.tex
<!-- pre9 {% raw %} -->
```latex
\begin{center}
The back cover
\end{center}
```
<!-- {% endraw %} -->

----
