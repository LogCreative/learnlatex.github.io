---
layout: "lesson"
lang: "zh-Hans"
title: "字体与 Unicode 引擎"
description: "本课讲述了 LaTeX 如何翻译 Unicode 输入以及它如何影响您的输入和使用的字体。并了解关于 Unicode 和 OpenType 字体支持的相关知识。"
toc-anchor-text: "字体与 Unicode 引擎"
toc-description: "选择字体和文件编码。"
---

# 字体与 Unicode 引擎

<span
  class="summary">本课讲述了 LaTeX 如何翻译 Unicode 输入以及它如何影响您的输入和使用的字体。并了解关于 Unicode 和 OpenType 字体支持的相关知识。</span>

在 TeX 和 LaTeX 被广泛使用之前，它们只需要内置支持欧洲语言。当然对于其他语言（比如德语和俄语）的文字也有一定的支持。

## 重音和重音字母

原本重音和重音字母都是通过控制序列或者宏输入的，比如：`\c{c}` 以输入 ‘ç’ 以及 `\'e` 以输入 ‘é’。虽然一些人仍然在使用这种输入方式因为这更容易输入，另一些人希望能够使用键盘上的按键来直接输入这些符号。

在 Unicode 出现之前，LaTeX 提供了许多种 *文件编码* 以允许很多语言的文字被原生地输入——比如：使用 `latin1` 编码，法国用户输入 “`déjà vu`” ，LaTeX 将会在内部将重音字母转译为 TeX 命令以产生正确的输出。 

这种方法至今仍然在 LaTeX 的 `pdflatex` 引擎中使用。除非另有说明，默认情况下所有的文件都被认为是 Unicode（以 UTF-8 编码）的。虽然这个引擎限制字体为 8 位长度的，但是许多欧洲语言仍然可以被支持。

## 字体选择

`pdflatex` 下的字体使用健壮的 LaTeX 字体选择方法。现在的标准 LaTeX 发布版中包含了许多开箱即用的字体。例如，TeX Gyre 是一套基于大部分人熟知的 Times, Helvetica, Palatino 等字体而制作的高质量字体。加载这些字体，和通过正确名字加载宏包一样简单。为了加载 Times 类似的字体，使用 TeX Gyre 中的名称 Termes：

```latex
\usepackage{tgtermes}
```
{: .noedit :}

对于 `pdflatex` 而言，许多字体都可以通过宏包加载。您可以查看 [LaTeX 字体目录](https://www.tug.org/FontCatalogue/) 或
[CTAN 中的 “字体” 主题](https://www.ctan.org/topic/font) 以查阅选项。您也可以在网上搜索您需要的字体，并寻找一个 `pdflatex` 兼容的版本。如果您想要使用一种专有字体，您可以搜寻一个合适的副本（大部分情况下都和原版足够类似的那种）。

## Unicode 时代

因为 `pdflatex` 被限制为 8 位文件编码和 8 位字体，所以其并不能原生支持现代的 OpenType 字体（使用不同的字母与用于输入专业术语的脚本）来在不同的语言之间切换。当下 pdfTeX 有两个替代的可原生使用 Unicode 输入与现代字体的引擎：XeTeX 和 LuaTeX。对于 LaTeX，这些引擎通常在您的编辑器中可以分别通过 `xelatex` 和 `lualatex` 被调用。

对于这些引擎，字体选择是通过 `fontspec` 宏包实现的。简单文档中可以如下面的例子一样简单：
```latex
\usepackage{fontspec}
\setmainfont{texgyretermes-regular.otf}
```
{: .noedit :}

这个例子选择了 TeX Gyre Termes 字体，和上面的 `pdflatex` 例子一样。值得注意的是，这种方法对 *任何* OpenType 字体都能用。一些对 `pdflatex` 可用的字体在 `xelatex` 和 `lualatex` 中通过对应的宏包也可以使用，或者和上面一样通过使用 `fontspec` 宏包加载您电脑上安装的任何字体。

[LaTeX 字体目录](https://www.tug.org/FontCatalogue/) 也展示了可用的 OpenType 字体，所以您可以用它来查阅字体。当然也可以使用前文提到的 [CTAN 页面](https://www.ctan.org/topic/font)。

选择好字体之后，就可以直接向文档里输入普通的 Unicode 字体了。下面的例子输入了一些拉丁字母、德语字母以及中日韩表意文字：

```latex
% !TEX xelatex
\documentclass{article}
\usepackage{fontspec}
\setmainfont{texgyretermes-regular.otf}
\newfontfamily\cjkfont{FandolSong-Regular.otf}
\begin{document}

ABC → αβγ → {\cjkfont 你好}

\end{document}
```

<p 
  class="hint">切换语言的时候，同时改变断字方式等也是很重要的。<code>babel</code> 和 <code>polyglossia</code> 宏包为此提供了稳定的功能。</p>
