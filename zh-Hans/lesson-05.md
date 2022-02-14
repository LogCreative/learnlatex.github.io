---
layout: "lesson"
lang: "zh-Hans"
title: "使用文档类来切换设计"
description: "本课解释了什么是文档类、其如何影响文档的布局、以及在 TeX 发行版中您能够使用的主要文档类。"
toc-anchor-text: "文档类"
toc-description: "设定文档的总体布局。"
---

# 文档类

<span
  class="summary">本课解释了什么是文档类、其如何影响文档的布局、以及在 TeX 发行版中您能够使用的主要文档类。</span>

您或许注意到了，目前为止我们所创建的 LaTeX 文档都是从 `\documentclass` 一行开始的，并且 `\documentclass{article}` 是目前为止最常见的选择。（在[上一课](lesson-04)我们需要 `\documentclass{report}` 来尝试 `\chapter` 命令。）所有 LaTeX 文档都需要这一行命令，并且（几乎）是您第一个要输入的命令。

## 文档类做了什么

文档类设置了文档的一般布局，比如：

- 设计了边距、字体、间隔等等；
- 是否需要设置章这一级；
- 标题是否需要另起一页。

更一般来讲，文档类也可以添加新的命令：特别是对于专用情形，比如创建幻灯片时。

文档类这一行也可以被设置一些 _全局选项_——对整个文档起作用的选项。这些选项需要在方括号中给出：`\documentclass[<选项>]{<文档类>}`。许多 LaTeX 命令都会使用这种首先在方括号中给出可选信息的语法。

## 基本文档类

LaTeX 提供了一系列标准文档类，它们看起来都相像，但也有些许变化：

- `article`  
  不包含章的短文档
- `report`  
  含有章的长文档，单面印刷
- `book`  
  含有章的长文档，双面印刷，包含正文前材料（front-matter）和正文后材料（back-matter，比如索引）
- `letter`  
  不包含目次信息
- `slides`  
  幻灯片（详见后文）

我们已经看到，`article`, `report`, `book` 文档类都有非常相似的命令。当撰写一个 `letter` 时，可以使用的命令已经有点不同了。

```latex
\documentclass{letter}
\usepackage[T1]{fontenc}
\begin{document}

\begin{letter}{Some Address\\Some Street\\Some City}

\opening{Dear Sir or Madam,}

The text goes Here

\closing{Yours,}

\end{letter}

\end{document}
```

观察 `\\` 是如何分隔地址行内容的。我们会在[稍后](lesson-11)来探讨断行问题。又见， `letter` 文档类针对信件提供了一个新的环境与一些专有的命令。

标准的 `article`, `report`, `book` 文档类接受 `10pt`, `11pt`, `12pt` 选项用于更改字体大小，使用 `twocolumn` 选项用于制作双栏文档。

## 富功能文档类

核心文档类都很稳定，但也就意味着在设计和提供的命令范围上非常保守。长久以来，也出现了许多非常强大的文档类，可以让您不必手动操作就可以彻底改变一些设计（这一点我们会在[稍后](lesson-11)提及）。

美国数学会提供了一些标准文档类的变种（`amsart`, `amsbook`），它们更接近于当时数学期刊出版物的传统设计。

两个最大且最流行的扩展类是 KOMA-Script 包和 memoir 文档类。KOMA-Script 包提供了标准类的一些“平行”类：`scrartcl`, `scrreprt`, `scrbook` 以及 `scrlttr2`，而 `memoir` 文档类更像是 `book` 类的一种拓展。

（译者注：CTeX 中文社区也提供了 ctex 宏包，其中包含了 `ctexart`, `ctexrep` 和 `ctexbook` 三个文档类，用来编写中文短文、中文报告和中文书籍。更多内容，可参见课程[排版中文](language-01)。）

这些拓展的文档类提供了许多个性化钩子，我们会在一个练习中探索一番。您可能会思考我们怎么才能知道它们提供了哪些钩子，这一点将会在[稍后的课程](lesson-16)中提到，您可以跳读看看！

## 幻灯片演示

`slides` 是为 20 世纪 80 年代中期物理投影片开发的文档类，它没有 PDF 交互式演示的一些功能。虽然的确有做到后者的现代文档类，但是对于一般的 LaTeX 文档来说，它们可能会稍显专业一些，所以我们会在[进一步的细节页面](more-05)讲述它。

## 练习

改变文档类为标准类、KOMA 包和 `memoir`，探索其是如何影响文档外观的。

```latex
\documentclass{article} % 在此处更改文档类
\usepackage[T1]{fontenc}

\begin{document}

\section{Introduction}

This is a sample document with some dummy
text\footnote{and a footnote}. This paragraph is quite
long as we might want to see the effect of making the
document have two columns.

\end{document}
```

添加文档类选项 `twocolumn` 并观察布局是怎么变化的。

当使用 `scrreprt` 文档类时，更改 `\section` 为 `\chapter`，并观察下面的文档类选项会产生什么影响。

- `chapterprefix`
- `headings=small`
- `headings=big`
- `numbers=enddot`
