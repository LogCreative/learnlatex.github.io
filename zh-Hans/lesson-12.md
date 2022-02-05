---
layout: "lesson"
lang: "zh-Hans"
title: "引用与参考文献"
description: "本课展示了引用数据库的基础知识。将学习如何构建自己的数据库以及如何通过两种主流的工具流将其应用于自己的文档中。"
toc-anchor-text: "引用与参考文献"
toc-description: "使用参考文献数据库。"
---

# 引用与参考文献

<script>
preincludes = {
 "pre1": {
    "pre0": "learnlatex.bib"
   },
 "pre2": {
    "pre0": "learnlatex.bib"
   }
}
</script>

<span
  class="summary">本课展示了引用数据库的基础知识。将学习如何构建自己的数据库以及如何通过两种主流的工具流将其应用于自己的文档中。</span>

对于文献引用来说，虽然您可以直接引用当前文档中的内容，但是大部分情况下，您可能会从一个或多个外部文件得到文献信息。这种文件就是文献数据库，以一种便于处理的格式存储。使用一个或多个文献数据库可以让您复用一些信息并避免手动设定格式。

## 引用数据库

引用数据库一般被称作“BibTeX 文件”，并带有文件扩展名 `.bib`。它们包含一条或多条记录，每条记录对应一个引用，每条记录中都会有一系列的域（field）。让我们看一个例子：

<!-- {% raw %} -->
```bibtex
@article{Thomas2008,
  author  = {Thomas, Christine M. and Liu, Tianbiao and Hall, Michael B.
             and Darensbourg, Marcetta Y.},
  title   = {Series of Mixed Valent {Fe(II)Fe(I)} Complexes That Model the
             {H(OX)} State of [{FeFe}]Hydrogenase: Redox Properties,
             Density-Functional Theory Investigation, and Reactivity with
             Extrinsic {CO}},
  journal = {Inorg. Chem.},
  year    = {2008},
  volume  = {47},
  number  = {15},
  pages   = {7009-7024},
  doi     = {10.1021/ic800654a},
}
@book{Graham1995,
  author    = {Ronald L. Graham and Donald E. Knuth and Oren Patashnik},
  title     = {Concrete Mathematics},
  publisher = {Addison-Wesley},
  year      = {1995},
}
```
<!-- {% endraw %} -->

这两条中一条是文章，另一条是书籍——这些是目前最常见的类型。正如上面所示，每个记录都以 `@` 开头，之后所有的信息都会被一对大括号包裹起来。

我们需要的大部分域虽然都以键值对的格式给出，但是与“主键”（key）相区别：“主键”是引用的名字。您可以使用任意一个名字，毕竟它只是一个标签。而在上面的例子中我们选择使用“作者名+年份”的格式（通常都是这么做的）。

虽然您需要确切提供什么域取决于记录类型的选择，但是大部分的域都是顾名思义的。您可能注意到了在 `author` 域，每一个作者都以 `and` 分开。这很 _重要_：_输出_ 格式需要了解哪一块是这个作者。您可能还注意到了在文章标题中，有些值还会被大括号包裹——以避免被作用任何大小写更正规则。

因为手动编写 `.bib` 可太枯燥了，所以大部分人都会选择一个专用编辑器。[JabRef](https://www.jabref.org) 跨平台并被广泛使用，当然也可用其他很多软件。
如果引用有 DOI（数字对象唯一标识符，Digital Object Identifier），您可能想要尝试 [doi2bib](https://doi2bib.org) 来方便地得到 BibTeX 记录（译者注：JabRef 也已内置）。但一定要检查记录是不是正确的那个！

这里我们将使用上面的小数据库来做下面的演示——我们已经将其保存为 `learnlatex.bib`。

## 从数据库转化信息

将信息插入您的文档分三步走。第一步，使用 LaTeX 编译您的文档，这将会产生包含文档引用列表的文件。第二步，运行一个从引用数据库获取信息的程序，检索出您使用的引用条目，然后按照顺序将它们排列起来。第三步，再次编译您的文档，这样 LaTeX 就可以使用这些信息来解析您的引用信息。通常这需要至少两次的编译来解析所有的引用。

对于第二步而言，现在有两种广泛使用的系统：BibTeX 和 Biber。Biber 仅供 LaTeX 中一个叫 `biblatex` 的宏包使用，而 BibTeX 可以不搭配宏包使用或者搭配 `natbib` 使用。

LaTeX 与这两者在不同编辑器上运行需要用不同的方式处理。我们的在线示例有一些后台脚本可以一键完成所有的事宜。
您的编辑器可能有“一键完成”按钮，否则您可能需要在不同的 LaTeX 文档编译中手动选择 BibTeX 或 Biber。

引用（citation）和参考（reference）的格式是独立于 BibTeX 数据库的，并且被一种名为 `style`（样式）的东西所设定。我们将会看到这些东西在 BibTeX 和 `biblatex` 工作流中有些许差异，但整体思想是一致的：我们可以选择引用显示的方式。

## 配合 `natbib` 的 BibTeX 工作流

虽然可以在不加载任何宏包的情况下向 LaTeX 文档插入引用，但这还是比较局限的。与之相对的，我们将使用 `natbib` 宏包，允许我们创建不同类型的引用，并且可以使用许多类型的样式。

我们输入的基本结构如这个例子所示：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{natbib}

\begin{document}
The mathematics showcase is from \citet{Graham1995}, whereas
there is some chemistry in \citet{Thomas2008}.

Some parenthetical citations: \citep{Graham1995}
and then \citep[p.~56]{Thomas2008}.

\citep[See][pp.~45--48]{Graham1995}

Together \citep{Graham1995,Thomas2008}

\bibliographystyle{plainnat}
\bibliography{learnlatex}
\end{document}
```

您可以看到我们通过对应的键名引用了数据库里不同的记录。`natbib` 宏包提供了文本和括号的引用样式：分别是 `\citet` 和 `\citep`。参考文献样式是通过 `\bibliographystyle` 这一行选择的：这里我们使用了 `plainnat` 样式。参考文献实际上是通过 `\bibliography` 这一行插入的，同时也选择了使用的数据库（多个数据库采用逗号分隔数据库名）。

页码引用可以通过一个可选参数添加。如果提供了两个可选参数，那么第一个可选参数就被当作引用前的小标记，第二个可选参数就被当作引用标签后的页码引用。

上述设定使用了作者—年份（author-year）样式。但是我们也可以采用数字编码的引用方式。这可以通过向 `natbib` 行添加 `numbers` 选项来实现。

## `biblatex` 工作流

`biblatex` 宏包和 `natbib` 运作方式稍有不同，主要体现在导言区内选择数据库和文档正文内的打印上。为此，要使用一些新的命令。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage[style=authoryear]{biblatex}
\addbibresource{learnlatex.bib} % 引用文件

\begin{document}
The mathematics showcase is from \autocite{Graham1995}.

Some more complex citations: \parencite{Graham1995} or
\textcite{Thomas2008} or possibly \citetitle{Graham1995}.

\autocite[56]{Thomas2008}

\autocite[See][45-48]{Graham1995}

Together \autocite{Thomas2008,Graham1995}

\printbibliography
\end{document}
```

注意到 `\addbibresource` _需要_ 数据库文件名的全称，而不是我们对于 `natbib` 下的 `\bibliography` 中省略 `.bib` 的情形。虽然 `biblatex` 使用了相对更长的引用命令，但是这些基本上都是顾名思义的。

再次地，引用前后的文字可以通过可选参数插入。注意这里页码不需要加以 `p.~` 或者 `pp.~` 前缀，`biblatex` 可以自动添加合适的前缀。

在 `biblatex` 中，当加载宏包的时候文献样式就被选择了。这里，我们使用了 `authoryear`，当然也可以用 `numeric` 数字编码和其他许多样式。

## 在 BibTeX 工作流和 `biblatex` 中选择

纵使 BibTeX 工作流和 `biblatex` 都需要 BibTeX 文件作为输入，并在文档中产生类似结构的输出，但他们产生这样的结果使用了截然不同的方法。这就意味着两种方法之间存在一些差异，通过这些差异可以帮助您选择最适合的方式。

在 BibTeX 工作流中，文献样式最终会被一个由 `\bibliographystyle` 命令选择的 `.bst` 文件决定。`biblatex` 不使用 `.bst` 文件而是使用了不同的系统。如果您使用的模板附带了 `.bst` 文件或者您的项目被要求使用特定的 `.bst` 文件，您必须选择 BibTeX 工作流而不可以使用 `biblatex`。

`biblatex` 采取了不同方式意味着，您可以通过在文档导言区使用基于 LaTeX 的命令直接修改参考文献和引用的输出格式。而修改 BibTeX 的 `.bst` 样式通常需要考察这些外部文件以及 BibTeX 编程语言的相关知识。一般来讲，`biblatex` 被称为是比 BibTeX 工作流更容易定制化的一种方案。

在 `biblatex` 中，通过更广泛的引用命令通常可以更加容易实现许多精心设计的引用样式。这也提供了更多独立于内容的特性。大致来说，许多理工科（STEM）科目来讲不太需要关注这种样式设定，但是对于一些人文学科的许多复杂样式来讲，这变得非常重要。

BibTeX 只能对美式 ASCII 字符正确排序，对于非美式 ASCII 字符的排序需要依赖于美式 ASCII 字符的变通方法。而 Biber `biblatex` 提供了完整的 Unicode 排序能力。因此对于非 ASCII 或非英语的文献排序而言，`biblatex` 通常是一个更好的选择。

谈了这么久 `biblatex`，实际上，BibTeX 工作流比 `biblatex` 更容易建立，这意味着许多出版社和期刊都希望通过 BibTeX 工作流生成参考文献。这些出版社不能或者一般不期望 `biblatex` 的提交。

总之，最重要的就是：向一个期刊或者出版社提交时，要阅览作者指南或提交指南。如果提供了 `.bst` 文件，您必须使用 BibTeX 工作流。如果您希望一个相对简单的文献和引用样式，并且只需要美式 ASCII 排序，BibTeX 工作流即可胜任。如果您需要稍微复杂的引用样式、非英语排序、或者想要更轻松地定制引用和文献样式，您可能需要考虑一下 `biblatex`。

## 练习

尝试 `natbib` 和 `biblatex` 的例子。对于 `natbib`，您将要运行：LaTeX, BibTeX, LaTeX, LaTeX；对于 `biblatex`，就是：LaTeX, Biber, LaTeX。查明怎么在您的编辑器中这么编译它，或者尝试一下 Overleaf 和 TeXLive.net 的自动化工具。

当您创建一个新的数据库记录和新的引用时观察会发生什么。添加不在数据库的引用记录然后看看会发生什么。实验 `natbib` 的 `numeric` 选项和 `biblatex` 的 `style=numeric` 选项。
