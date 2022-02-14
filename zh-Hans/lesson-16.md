---
layout: "lesson"
lang: "zh-Hans"
title: "查看说明文档并获取帮助"
description: "本课展示了 LaTeX 相关软件和宏包的主要文档资源，以及当您遇到困难时应当如何获取帮助。"
toc-anchor-text: "帮助与文档"
toc-description: "查看说明文档并获取帮助。"
---

# 查看说明文档并获取帮助

<span
  class="summary">本课展示了 LaTeX 相关软件和宏包的主要文档资源，以及当您遇到困难时应当如何获取帮助。</span>

查看宏包或文档类的说明文档有很多种方式。

## `texdoc`

如果您已经安装了 TeX 发行版（如 TeX Live 或 MiKTeX），并在安装时选择包含文档，那么就可以通过命令行工具 `texdoc` 来查看它们。使用

`texdoc` < _pkg_ >

命令将打开包 `<pkg>` 对应的文档。程序会搜索可用的文档，并打开它认为与搜索项最为匹配的结果。使用

`texdoc -l` < _pkg_ >

命令将会列出所有可能的结果，您可以从中选择所需要的文档。

## texdoc.org

它是一个类似 `texdoc` 工具的[网站](https://texdoc.org/)。通过它可以像 `texdoc -l` 那样在海量文档中进行搜索，然后在其中找到您所需要的。

## CTAN

[CTAN](https://www.ctan.org) 全称 Comprehensive TeX Archive Network（TeX 综合资料网）。绝大多数的 LaTeX 宏包都会在这里发布，因此您也可以通过在该网站搜索以访问其文档。一般来说，宏包会位于 `ctan.org/pkg/<pkg-name>` 路径下，在这里通常可以找到相应的 README 和文档。

## 关于 LaTeX 的书籍

这里的一些书籍可以帮助您进一步了解 LaTeX。作为初学者，您总能从那些条理清晰的入门指南上获益良多，毕竟与我们这儿相比，它们往往会写得更加详尽。您也可能需要手边常备一本参考书，用来找寻各种琐碎的细节和建议。

LaTeX 小组有一个主要有其成员完成的书的[书籍清单](https://www.latex-project.org/help/books)。最值得一提的是 [Lamport 纂写的官方指南](https://www.informit.com/store/latex-a-document-preparation-system-9780201529838)以及所涉甚广的 [LaTeX Companion](https://www.informit.com/store/latex-companion-9780201362992)。

其他旨在学习 LaTeX 的书籍有如：

- [_Guide to LaTeX_](https://www.informit.com/store/guide-to-latex-9780132651714)，由  Helmut
  Kopka 及 Patrick Daly 所著——可作为电子版获得。
- [_LaTeX for Complete Novices_](https://www.dickimaw-books.com/latex/novices/) 由
  Nicola Talbot 所著——可获得免费的电子版，还可选择低价印刷版。
- [_Using LaTeX to write a PhD thesis_](https://www.dickimaw-books.com/latex/thesis/) 自
  Nicola Talbot——可获得免费的电子版，亦可选择低价印刷版。
- [_LaTeX Beginner's Guide_](https://www.packtpub.com/gb/hardware-and-creative/latex-beginners-guide)
  自 Stefan Kottwitz——电子版和印刷版均可获得。
- [_LaTeX and Friends_](https://www.springer.com/gp/book/9783642238154) 由
  Marc van Dongen 所著——电子版和印刷版均可获得。

## 寻求帮助

您可以在许多在线论坛询问 LaTeX 的相关问题；其中当下风靡的也许是 [TeX - LaTeX StackExchange](https://tex.stackexchange.com)。当您遇到任何问题，首先最好给出一个清楚的例子 —— 也就是为人所熟知的「最小工作案例（MWE）」。这并不意味着这段代码真的起作用（不然您当然就不需要提问了！），而表示您已然尽力使问题代码清晰、独立并且最简。后者意味着它仅有能充分展示问题的文本。

### 如何构建一个最小工作案例（MWE）

该如何构建一个 MWE？通常，最简单的方法是从：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Text
\end{document}
```

开始并逐行增加直到问题复现。或者，您也可以尝试「削减」您的原始文本，但是这可能耗费较长的时间。

<p 
  class="hint">如果您需要更多的文本来展示分页或者别的什么效果，则不妨尝试用 <code>lipsum</code> 这样的宏包以生成假文段落，以免测试文件过大。</p>

### 日志文件

日志文件（即 log 文件）可能是另一个您想要获得的东西；它由 LaTeX 于每次运行时创建，和您的输入有着相同名字不过以拓展名 `.log` 结尾。

<p 
  class="hint">您可能需要选择「显示扩展名」以找出它，这依赖于您的桌面界面。</p>

您可以在日志文件中看到完整的错误信息。LaTeX 的错误信息一般很有帮助，当然也并不提供和字处理器中一样的错误信息。

<p 
  class="hint">有些编辑器也会让查看「完整」错误文本变得很难。这可能会隐藏一些关键细节。</p>

当您提出问题时，LaTeX 专家通常会询问能否获得日志文件的一份拷贝。

### 更进一步

最后，我们提供了[案例展示](extra-01)，使用例子来展现一些本课程中没有涉及的不同学科领域，以及这些领域中不同的 LaTeX 宏包。