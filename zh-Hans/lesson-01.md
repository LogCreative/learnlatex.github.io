---
layout: "lesson"
lang: "zh-Hans"
title: "LaTeX 是什么？它如何工作？"
description: "本课介绍了 LaTeX 是什么以及它将如何工作，并解释了它与 Microsoft Word 或 LibreOffice Writer 等常见文字处理软件的不同之处。"
toc-anchor-text: "LaTeX 基础"
toc-description: "LaTeX 是什么？它如何工作？"
---

# LaTeX 基础

<span
  class="summary">本课介绍了 LaTeX 是什么以及它将如何工作，并解释了它与 Microsoft Word 或 LibreOffice Writer 等常见文字处理软件的不同之处。</span>

与 Microsoft Word 或 LibreOffice Writer 等常见的文字处理软件不同，LaTeX 通常不提供 WYSIWYG（所见即所得）的功能。使用 LaTeX 时，人们采用纯文本进行编辑，并添加各种标记。与 HTML 类似，这些标记将告诉 LaTeX 文本中特定元素的逻辑含义。

例如，元素 `<h2>` 标记了 HTML 文档中一个新的小节（section）。LaTeX 也提供了类似的功能，即 `\section` 命令。

## LaTeX 的工作流程

LaTeX 文件不是文档本身，而是有关文档各部分内容的说明，因此你通常不会直接把 LaTeX 文件交给别人。相反，在编写好 LaTeX **源代码**之后，需要运行 LaTeX（通常使用名为 `pdflatex` 的程序）以生成 PDF 文件。生成的 PDF 就可以供其他人来阅读。

不同的人采用不同的方式来描述这一过程。使用 LaTeX 有点像写程序，所以很多人把上面的过程称为「编译」，不过也许「排版」一词更为准确。

## 多次运行 LaTeX

对于简单的文档，只需要排版一次即可获得完整的 PDF。然而，一旦加入了更复杂的东西，如交叉引用、引文、图片、目录等，可能就需要多次运行 LaTeX。如果遇到这样的情况，我们将会特别指出。

## LaTeX、pdfLaTeX 还是……

在[下一课](lesson-02)中，我们将看到 LaTeX 并非一个单独的程序。为了不把事情弄复杂，我们将仅使用 pdfLaTeX 来生成 PDF。在本课程的后面，我们还将接触到其他的程序，并了解为什么需要它们。
