---
layout: "lesson"
lang: "zh-Hans"
title: "数学公式"
description: "本课展示了 LaTeX 的数学模式、如何通过 `amsmath` 宏包排版行内和行间公式、以及如何改变数学模式中的字体。"
toc-anchor-text: "数学公式"
toc-description: "数学模式和记号。"
---

# 数学公式

<span
  class="summary">本课展示了 LaTeX 的数学模式、如何通过 `amsmath` 宏包排版行内和行间公式、以及如何改变数学模式中的字体。</span>

排版复杂的数学公式是 LaTeX 最重要的优势之一。您可以在“数学模式”下通过逻辑标记的方式编写数学公式。

## 数学模式

在数学模式下，空格会被省略，字符间（基本上）都会有恰当的空格。

数学模式有两种形式：

* 行内公式
* 行间公式

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
A sentence with inline mathematics: $y = mx + c$.
A second sentence with inline mathematics: $5^{2}=3^{2}+4^{2}$.


A second paragraph containing display math.
\[
  y = mx + c
\]
See how the paragraph continues after the display.
\end{document}
```

您或许在其他地方看到了“类似 LaTeX 的”数学公式输入系统。比如，可以向网页中放置公式的 MathJax。这些系统之所以通常接受 LaTeX 语法的微小变种作为输入，是因为它们实际上并不使用 LaTeX “后端”。

<p
  class="hint">我们的例子都使用了 <i>标准的</i> LaTeX 语法。如果您在其他地方看到了一些不同的用法，那么可能只是因为您看到的内容用的并不是 LaTeX。</p>

### 行内数学模式和数学符号

由上文可见，行内数学公式是通过一对美元符号（`$...$`）标记的。当然用 `\( ... \)` 标记也是可行的。输入简单表达式不需要任何特殊的标记，您将看到数学公式会被排版出合适的间隔而且文字会变成斜体。

行内数学模式限制了表达式的纵向高度以使数学公式尽可能不打乱段落的行间距。

注意到 _所有的_ 数学符号都应被标记成数学模式下的。即使只是一个字符也应该使用 `... $2$ ...` 而不是 `... 2 ...`。否则，比如说，您需要输入一个负数，然后需要使用数学模式来输入负号，那么 `... $-2$ ...` 可能就会产生与文本模式下不同的数字字体（这取决于文档类的选择）。相反地，要注意从其他地方复制过来的纯文本可能会导致数学模式的构造，比如用于表示金额的美元符号 `$` ，或者是表示文件名的下划线符号 `_`（这些应该分别被标记为 `\$` 和 `\_`）。

我们可以很容易地添加上标和下标：分别通过 `^` 和 `_` 标记。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Superscripts $a^{b}$ and subscripts $a_{b}$.
\end{document}
```

（您可能会看到一些不使用大括号来包裹简单上标和下标的例子，但是这并不是标准的语法，而且可能会导致错误。所以永远记得使用大括号。）

LaTeX 里有 _许多_ 专有的数学模式命令。它们中有些很容易，比如 `\sin` 和 `\log` 用来分别表示正弦符号和对数符号，`\theta` 用于表示对应的希腊符号。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
Some mathematics: $y = 2 \sin \theta^{2}$.
\end{document}
```

虽然我们不能在这里涉及所有标准 LaTeX 数学模式的命令，但是网上有许多列出标准数学命令的资源。您可以在 [Detexify](https://detexify.kirelabs.org/classify.html) 工具里查阅数学模式中符号所对应的命令。

### 行间数学模式

您可以在行间模式中使用与行内模式一样的命令。行间数学模式默认设置在居中位置，并为“仍属于该段”的大型公式所准备。注意到行间数学环境不允许在数学模式中结束该段，所以您也许不能够在该模式的源代码中留有空行。

段落都应当在行间公式 _之前_ 开始，所以不要在行间数学环境之前留有空行。如果您的数学公式有多行，不要使用多个连续的行间数学环境（这将导致不一致的行间距），而是使用一种多行行间公式环境，比如稍后提及的 `amsmath` 宏包中 `align` 环境。

对于积分来说，行间公式尤其有用，来看下面的例子：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
A paragraph about a larger equation
\[
\int_{-\infty}^{+\infty} e^{-x^2} \, dx
\]
\end{document}
```

请注意观察这里是如何使用上标和下标设定积分上下限的。

这里我们手动添加了一个间隙：`\,`，以在 `dx` 前添加一个小间隙。微分符号的格式各有差别：一些出版商使用直立的“d”而其他出版商使用斜体的“_d_”。为了适应这两种方式，编写源代码的一种方法就是定义一个 `\diff` 命令，这样您就能够根据需要进行调整，[比如说](http://www.tug.org/TUGboat/tb41-1/tb127gregorio-math.pdf)：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\newcommand{\diff}{\mathop{}\!d}            % For italic
% \newcommand{\diff}{\mathop{}\!\mathrm{d}} % For upright
\begin{document}
A paragraph about a larger equation
\[
\int_{-\infty}^{+\infty} e^{-x^2} \diff x
\]
\end{document}
```

您通常需要对公式编号，使用 `equation` 环境可以创建这些编号。让我们再次尝试同一个例子：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
A paragraph about a larger equation
\begin{equation}
\int_{-\infty}^{+\infty} e^{-x^2} \, dx
\end{equation}
\end{document}
```

公式编号将会自动递增，公式旁或者只有一个数字（就像这个例子一样）或者会加一个目次号码的前缀，比如 (2.5) 表示第 2 节的第 5 个公式。设定编号格式是在文档类内进行的，这里就不再展开了。

## `amsmath` 宏包

数学符号太多了，就意味着 LaTeX 内核内置的工具并不能提供所有内容。`amsmath` 宏包拓展了内核以提供更多的方案。[`amsmath` 用户手册](http://texdoc.org/pkg/amsmath)提供了比本课更多的例子。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}

\begin{document}
Solve the following recurrence for $ n,k\geq 0 $:
\begin{align*}
  Q_{n,0} &= 1   \quad Q_{0,k} = [k=0];  \\
  Q_{n,k} &= Q_{n-1,k}+Q_{n-1,k-1}+\binom{n}{k}, \quad\text{for $n$, $k>0$.}
\end{align*}
\end{document}
```

`align*` 环境会让公式在和号 `&` 处对齐，这和表格的用法是一样的。注意一下我们是如何使用 `\quad` 添加小间距、以及使用 `\text` 向数学模式添加正常的文字。我们这里还使用了另一个数学模式命令：二项式 `\binom`。

还注意到我们使用了 `align*` 环境，让公式不被编号。大部分的数学环境都会默认对公式编号，而带星号（`*`）的变式关闭了编号功能。

该宏包还提供了其他几个很方便的环境，比如说对于矩阵：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}
\begin{document}
AMS matrices.
\[
\begin{matrix}
a & b & c \\
d & e & f
\end{matrix}
\quad
\begin{pmatrix}
a & b & c \\
d & e & f
\end{pmatrix}
\quad
\begin{bmatrix}
a & b & c \\
d & e & f
\end{bmatrix}
\]
\end{document}
```

## 数学模式的字体

和正常文本不同的是，数学模式的字体变化通常会蕴含非常特定的意义。所以它们经常被写做特殊的命令。下面就是您需要的一组命令：

- `\mathrm`: 罗马字体（直立体）
- `\mathit`: 使用普通文本字间隔的斜体
- `\mathbf`: 粗体
- `\mathsf`: 衬线字体
- `\mathtt`: 等宽字体（打字机字体）
- `\mathbb`: 双重粗体（黑板粗体，由 `amsfonts` 宏包提供）

这些命令接受英文字母作为参数，因此如果我们要写出一个矩阵符号的话：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
The matrix $\mathbf{M}$.
\end{document}
```

注意默认情况下数学斜体会让字母产生较大的间距，以至于它们可能会看起来像是一些变量的乘积。这种情况下，使用 `\mathit` 来产生斜体文字。

这些数学字体命令 `\math..` 针对数学使用了特殊的字体。有时您可能需要在数学公式中嵌入一个属于外部句子的词，并需要使用当前文段的字体，在这种情况下可以使用 `\text{...}`（由 `amsmath` 宏包提供）或者是特定的字体比如 `\textrm{..}`。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}
\begin{document}

$\text{bad use } size  \neq \mathit{size} \neq \mathrm{size} $

\textit{$\text{bad use } size \neq \mathit{size} \neq \mathrm{size} $}

\end{document}
```

如果您需要加粗其他符号，请见[进一步的细节页面](more-10)。

## 练习

尝试一些数学模式的基本操作：尝试上面的例子，然后在行内和行间数学模式之间切换。您能看出这有什么效果吗？

尝试输入其他的大写的和小写希腊字母。您应该能够猜出来它们的命令名称。

对字体切换命令进行实验：当嵌套使用的时候会发生什么？

行间公式通常是居中对齐的。尝试向文档类添加选项 `[fleqn]`（向左对齐），然后观察上面的例子，会产生不同的布局。类似地，公式编号通常是向右对齐的，尝试向文档类添加选项 `[leqno]`（编号在左边）。
