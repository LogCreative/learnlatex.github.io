---
layout: "lesson"
lang: "zh-Hans"
title: "更多：让 LaTeX 跑起来"
description: "本课对 LaTeX 是什么与运行在什么引擎上做了更多的阐述。"
toc-anchor-text: "更多：让 LaTeX 跑起来"
---

对我们大多数的例子而言，我们使用的程序并不叫做 `latex`，而是 `pdflatex` 。它是 `latex` 相关程序衍生家族的一员。我们选择 `pdflatex` 是因为它大概是目前最广泛使用的系统，能够直接产生 PDF 文件。

## 格式与引擎

正如[之前](more-01)所提到的，LaTeX 是建构在 TeX 系统之上的。我们称 LaTeX 为一种「格式」（format）——一种能被 TeX 所理解的宏集（宏指的是指令和函数）。如果你运行 `pdflatex`，你**实际上**是在运行一个叫 `pdfTeX` 的程序，并预装了对应的「LaTeX 格式」。我们通常称 pdfTeX 为一种**引擎**——可以理解 TeX 指令的程序。

现在大致有三种常见引擎：

- pdfTeX
- XeTeX
- LuaTeX

我们将会在[后面的课程](lesson-14)中讲述 XeTeX 和 LuaTeX：我们目前只需要知道他们能够加载操作系统中安装的字体，而 pdfTeX 并不能这么做。

如果你在日本，并且写很多日语内容，你可能需要与 pTeX 和 upTeX 打交道。它们对竖直排版有着特殊的优化。LuaTeX 也能实现其中的大部分功能，但就目前来讲，upTeX 系统仍然是日语中最常用的。
