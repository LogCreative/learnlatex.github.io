---
layout: "lesson"
lang: "zh-Hans"
title: "字体与 Unicode 引擎"
description: "本课讲述了 LaTeX 如何解释 Unicode 输入以及它如何影响你的输入和使用的字体。了解关于 Unicode 和 OpenType 字体支持的相关知识。"
toc-anchor-text: "字体与 Unicode 引擎"
toc-description: "选择字体和文件编码。"
---

# 字体与 Unicode 引擎

<span
  class="summary">本课讲述了 LaTeX 如何解释 Unicode 输入以及它如何影响你的输入和使用的字体。了解关于 Unicode 和 OpenType 字体支持的相关知识。</span>

TeX 和 LaTeX 被广泛使用之前，它们只需内置支持欧洲语言即可。虽然它们对于其他语言（比如德语和俄语）的文字也有一定的支持。

## 重音和重音字母

最初重音和重音字母都是通过控制序列（control sequence）或者宏（macro）输入的，比如：`\c{c}` 来输入 ‘ç’ 以及 `\'e` 来输入 ‘é’。虽然一些人仍然在使用这种输入方式，因为这更容易输入，但是另一些人希望他们能够使用键盘上的按键来直接输入这些符号。

在 Unicode 出现之前，LaTeX 提供了许多种 *文件编码* 以允许很多语言的文字被原生地输入——比如：使用 `latin1` 编码，法国用户就可以输入「`déjà vu`」，LaTeX 会在内部将重音字母转译为 TeX 命令以产生正确的输出。 

这种方法至今仍然在 LaTeX 的 `pdflatex` 引擎中使用。除非另有说明，默认情况下所有的文件都被认为是 Unicode（以 UTF-8 编码）的。虽然这个引擎会限制字体为 8 位长度的，但是许多欧洲语言仍可被支持。

## 字体选择

`pdflatex` 下的字体使用稳健（robust）的 LaTeX 字体选择方法。现在的标准 LaTeX 发行版中包含了许多开箱即用的字体。例如，TeX Gyre 是一套基于大部分人熟知的 Times, Helvetica, Palatino 等字体而制成的高质量字体。加载这些字体，和通过正确名字加载宏包一样简单。对于 Times 类似字体，TeX Gyre 中的名称为 Termes：

```latex
\usepackage{tgtermes}
```
{: .noedit :}

对于 `pdflatex` 而言，许多字体都可以通过宏包加载。你可以查看 [LaTeX 字体目录](https://www.tug.org/FontCatalogue/)或
[CTAN 中的「字体」主题](https://www.ctan.org/topic/font)以查阅一些选择。你也可以在网上搜索需要的字体，并寻找一个 `pdflatex` 兼容的版本。如果你想要使用一种专有字体，可以搜寻一个合适的副本（大部分情况下都存在与原版足够类似的那种）。

## Unicode 时代

因为 `pdflatex` 被限制为 8 位文件编码和 8 位字体，所以它并不能原生地支持现代 OpenType 字体（使用不同的字母与用于输入专业术语的脚本）来在不同的语言之间切换。当下 pdfTeX 有两个可原生使用 Unicode 输入与现代字体的替代引擎：XeTeX 和 LuaTeX。对于 LaTeX，这些引擎通常在你的编辑器中分别可以通过 `xelatex` 和 `lualatex` 被调用。

在这些引擎中，字体选择是通过 `fontspec` 宏包实现的。对于简单文档可以如下面的例子一样简单：
```latex
\usepackage{fontspec}
\setmainfont{texgyretermes-regular.otf}
```
{: .noedit :}

这个例子选择了 TeX Gyre Termes 字体，和上面的 `pdflatex` 例子一样。值得注意的是，这种方法对 *任何* OpenType 字体都能用。一些对 `pdflatex` 可用的字体在 `xelatex` 和 `lualatex` 中通过对应的宏包也可以使用。或者是和上面一样，通过使用 `fontspec` 宏包加载你电脑上安装的任何字体。

[LaTeX 字体目录](https://www.tug.org/FontCatalogue/)展示了可用的 OpenType 字体，因此你也可以用它来查阅字体资源。当然也可以使用前文提到的 [CTAN 页面](https://www.ctan.org/topic/font)。

选择好字体之后，就可以直接向文档里输入普通的 Unicode 字体了。下面的例子展示了一些拉丁字母、德语字母以及中日韩（CJK）表意文字的输入：

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
  class="hint">切换语言的同时，改变断字方式等事项通常也是很重要的。<code>babel</code> 和 <code>polyglossia</code> 宏包为此提供了稳健的功能。</p>
