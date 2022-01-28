---
layout: "lesson"
lang: "zh-Hans"
title: "更多：表格"
description: "本课展示更多自定义表格的方式：更改列格式、改变间距和分割线以及提供更多表格扩展的其他宏包。"
toc-anchor-text: "更多：表格"
---

## 其他引导符

由于主课没有涉及所有可用的引导符，这里就用例子介绍一些其他的引导符。您可能想要回顾一下主课开头的表格来对可用符号做一个概览。理解 `l`, `c`, `r` 和 `p` 之后，那里提供的简短说明应该足以理解列类型 `m`, `b`, `w` 和 `W` 在做什么。如果还不太清楚的话，您可能想对它们再试验一下。没有涉及的其他好用引导符还有 `>`, `<`, `@` 和 `|`。

### 更改列样式

由于 `>` 和 `<` 分别用来在列的每个单元格前和后添加内容，所以您可以使用这些引导符来添加影响列样式的命令。比如说，如果您想将第一列设为斜体，并在其后加一个冒号，可以这么做：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{>{\itshape}l<{:} *{2}{l}}
  \toprule
  Animal & Food  & Size   \\
  \midrule
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

`\itshape` 将所有后续的文字变为斜体，但效果范围被限制在单元格的“容器”中。我们将会在[后续课程](lesson-11)中学习如何手动设定文本格式。

您或许想让作为表头的第一个单元格不受影响，这里可以使用 `\multicolumn`。记住它可以用来改变单一单元格的对齐方式，正如下面所展示的那样。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{>{\itshape}l<{:} *{2}{l}}
  \toprule
  \multicolumn{1}{l}{Animal} & Food  & Size   \\
  \midrule
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

### 调整列间距

通常 LaTeX 会对列的两边加些间距，以平衡视觉并分隔它们。这个间距通过 `\tabcolsep` 定义。由于每一列都会在两边增加一个 `\tabcolsep` 的间距，所以两列间的间距是 `2\tabcolsep` —— 每列贡献一个单位长。您可以通过 `\setlength` 将这个默认间距调整到任何长度：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\setlength\tabcolsep{1cm}

\begin{document}
\begin{tabular}{lll}
  Animal & Food  & Size   \\
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

您也可以通过使用 `@` 来将这个间距变更为一任意长度。这将移除两列间的空隙或者是某一端的空隙，取代为添加在参数中的任何放在两列间的东西。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{l@{ : }l@{\hspace{2cm}}l}
  Animal & Food  & Size   \\
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

（我们将会[很快了解](lesson-11) `\hspace`：可以猜到它增加了水平间距。）

`!` 引导符做了类似的一件事。区别在于它向两列间间隙中心 _添加_ 参数中的内容。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{l!{:}ll}
  Animal & Food  & Size   \\
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

### 竖直分割线

有时您想使用竖直分割线。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{l|ll}
  Animal & Food  & Size   \\[2pt]
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

您或许注意到 `|` 的效果很像 `!{decl}`：不改变间距的情况下向两列间增加一竖直分割线。只是这儿有个大缺点：竖直分割线并不能很好地与 `booktabs` 提供的水平分割线兼容。您可以使用 LaTeX 提供的水平分割线：`\hline`（对应于 `\toprule`, `midrule` 和 `bottomrule`）以及 `\cline`（很像 `\cmidrule`）。正如上面所展示的那样，竖直分割线将会延展到 `\\` 可选参数中的空间。

## 自定义 `booktabs` 分割线

所有的 `booktabs` 分割线和 `\addlinespace` 支持方括号内的一个可选参数用来指定分割线的宽度。另外，`\cmidrule` 通过在 `r` 或 `l` 后的花括号中指定长度以自定义修剪范围。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{@{} lll@{}} \toprule[2pt]
  Animal & Food  & Size   \\ \midrule[1pt]
  dog    & meat  & medium \\
  \cmidrule[0.5pt](r{1pt}l{1cm}){1-2}
  horse  & hay   & large  \\
  frog   & flies & small  \\ \bottomrule[2pt]
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

## 数值列对齐

表格中的数值对齐可以通过 `siunitx` 宏包提供的 `S` 列类型处理。

关于对齐两个数值列的例子如下：

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{booktabs}
\usepackage{siunitx}
\begin{document}
\begin{tabular}{SS}
\toprule
{Values} &  {More Values} \\
\midrule
1        &   2.3456 \\
1.2      &   34.2345 \\
-2.3     &   90.473 \\
40       &   5642.5 \\
5.3      &   1.2e3 \\
0.2      &    1e4 \\
\bottomrule
\end{tabular}
\end{document}
```

注意到任何非数值的单元格必须通过包裹花括号的形式“保护”起来。

`siunitx` 宏包提供了很多不同的格式化数值方式——详见[宏包文档](https://texdoc.org/pkg/siunitx)。

## 指定表格总宽度

`tabular` 环境的宽度是基于表格内容自动确定的。主要有两种方式来指定不同的总宽度。

注意，大部分情况下推荐使用下面的方式格式化表格到指定的宽度（必要时可以使用例如 `\small` 文字大小），而不是将表格使用 `\resizebox` 或相似的命令缩放，因为这会产生不一致的文字大小和分割线宽度。

### `tabular*`

`tabluar*` 环境接受一个额外的 _宽度_ 参数，以指定表格的总宽度。伸缩间距必须通过 `\extracolsep` 命令向表格添加，这个间距将会添加到导言引入点之后的所有列之间。大部分情况下将 `\fill` 作为参数使用，以产生一个尽可能拉大的间距。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\begin{document}

\begin{center}
\begin{tabular}{cc}
\hline
A & B\\
C & D\\
\hline
\end{tabular}
\end{center}

\begin{center}  
\begin{tabular*}{.5\textwidth}{@{\extracolsep{\fill}}cc@{}}
\hline
A & B\\
C & D\\
\hline
\end{tabular*}
\end{center}

\begin{center}  
\begin{tabular*}{\textwidth}{@{\extracolsep{\fill}}cc@{}}
\hline
A & B\\
C & D\\
\hline
\end{tabular*}
\end{center}

\end{document}
```

### `tabularx`

`tabularx` 环境（被同名宏包提供）含有和 `tabular*` 相似的名称，但是相较于调整列间距，它通过指定一种新的列类型 `X` 来调整列宽。这等价于自动确定宽度的 `p{...}` 类型。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{tabularx}
\begin{document}

\begin{center}
\begin{tabular}{lp{2cm}}
\hline
A & B B B B B B B B B B B B B B B B B B B B B B B B\\
C & D D D D D D D\\
\hline
\end{tabular}
\end{center}

\begin{center}  
\begin{tabularx}{.5\textwidth}{lX}
\hline
A & B B B B B B B B B B B B B B B B B B B B B B B B\\
C & D D D D D D D\\
\hline
\end{tabularx}
\end{center}

\begin{center}  
\begin{tabularx}{\textwidth}{lX}
\hline
A & B B B B B B B B B B B B B B B B B B B B B B B B\\
C & D D D D D D D\\
\hline
\end{tabularx}
\end{center}

\end{document}
```

和之前这些课中讨论的其他形式不同，`tabularx` 需要使用试验宽度排版表格数次以做出最终设定。这意味着环境的使用会有些许限制——详见[宏包文档](https://texdoc.org/pkg/tabularx)。

## 跨页表格

`tabular` 构造了一个不可破损的盒子，因此它必须足够小以适配于一页之内，而且经常放置于 `table` 浮动体环境中。

好几个宏包提供了相似的名称变种以允许跨页。这里我们展示 `longtable` 宏包：

```latex
\documentclass{article}
\usepackage[paperheight=8cm,paperwidth=8cm]{geometry}
\usepackage{array}
\usepackage{longtable}
\begin{document}
\begin{longtable}{cc}
\multicolumn{2}{c}{A Long Table}\\
Left Side & Right Side\\
\hline
\endhead
\hline
\endfoot
aa & bb\\  
Entry & b\\  
a & b\\  
a & b\\  
a & b\\  
a & b\\  
a & bbb\\  
a & b\\  
a & b\\  
a & b\\  
a & b\\  
a & b\\  
a & b\\  
a & b b b b b b\\  
a & b b b b b\\  
a & b b\\  
A Wider Entry & b\\  
\end{longtable}

\end{document}
```

`longtable` 很重要因为它保持了所有页的表格列宽度。然而，为了实现这一点，它可能需要 LaTeX 的多次运行以使得后面加载的宽单元格影响到之前页中的表格宽度。

## 表格标注

表格中使用类似于脚注的标记以代指表格后面的标注是很常见的需求。`threeparttable` 宏包简化了这种表格的标记方法，将标注所在的区块宽度设定为表格同宽。详细细节参见[宏包文档](https://texdoc.org/pkg/threeparttable)，我们这里展示一个简单的例子。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{threeparttable}
\begin{document}

\begin{table}
\begin{threeparttable}
   \caption{An Example}
   \begin{tabular}{ll}
    An entry & 42\tnote{1}\\
    Another entry & 24\tnote{2}\\
   \end{tabular}
   \begin{tablenotes}
   \item [1] the first note.
   \item [2] the second note.
   \end{tablenotes}
\end{threeparttable}
\end{table}

\end{document}
```

## 窄列排版

默认的断行设置假定行宽相对较大，以在断行选择上给予一些灵活性。下面的例子展示了一些可能的方法。第一个表格展示了扩张的词间间距，TeX 会警告之为未填满的行盒子。使用 `\raggedright` 通常避免了这个问题，但也会使得一些行太“锯齿”了。`ragged2e` 宏包中的 `\RaggedRight` 命令是一种折中方案——它将允许行宽上的一定的锯齿形态，但也会在必要时断词，正如第三个表格所展示的那样。

注意这里使用了 `\arraybackslash`，将重新设定 `\\` 的定义以结束一行。

另一种替代技巧，正如第四个表格所展示的那样，用更小的文字以使得列相对于这种文字大小不再狭窄。

```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{ragged2e}
\begin{document}

\begin{table}

\begin{tabular}[t]{lp{3cm}}
One & A long text set in a narrow paragraph, with some more example text.\\
Two & A different long text set in a narrow paragraph, with some more  hard to hyphenate words.
\end{tabular}%
\begin{tabular}[t]{l>{\raggedright\arraybackslash}p{3cm}}
One & A long text set in a narrow paragraph, with some more example text.\\
Two & A different long text set in a narrow paragraph, with some more  hard to hyphenate words.
\end{tabular}%
\begin{tabular}[t]{l>{\RaggedRight}p{3cm}}
One & A long text set in a narrow paragraph, with some more example text.\\
Two & A different long text set in a narrow paragraph, with some more  hard to hyphenate words.
\end{tabular}

\footnotesize
\begin{tabular}[t]{lp{3cm}}
One & A long text set in a narrow paragraph, with some more example text.\\
Two & A different long text set in a narrow paragraph, with some more  hard to hyphenate words.
\end{tabular}

\end{table}

\end{document}
```

## 定义新的列类型

正如[主课](lesson-08)所展示的那样，`array` 宏包允许构造诸如 `>{\bfseries}c` 的方式以表示一个粗体居中列。定义一个新的列类型来封装这种用法通常是方便的，比如

```latex
\newcolumntype{B}{>{\bfseries}c}
```
将允许在表格导言中使用 `B` 来代指一个粗体居中列。

## 纵向技巧

相较于使用一个单元格占据多行，使用嵌套的 `tabular` 环境将一行的一些单元格纵向分割通常是更好的选择。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{lcc}
  \toprule
  Test & \begin{tabular}{@{}c@{}}A\\a\end{tabular} & \begin{tabular}{@{}c@{}}B\\b\end{tabular} \\
  \midrule
  Content & is & here \\
  Content & is & here \\
  Content & is & here \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

注意到您可以通过一个 `tabular` 的可选参数来控制纵向对齐——支持使用 `t`, `c` 或 `b` 分别表示顶部、居中、底部对齐。使用方法像这样：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{lcc}
  \toprule
  Test & \begin{tabular}[b]{@{}c@{}}A\\a\end{tabular} & \begin{tabular}[t]{@{}c@{}}B\\b\end{tabular} \\
  \midrule
  Content & is & here \\
  Content & is & here \\
  Content & is & here \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

## 表格中的行间距

在主课中我们演示了 `booktabs` 宏包的 `\addlinespace` 用来在指定行之间增加额外的空隙。

主要有两个默认参量来控制行间距：`\arraystretch` 和 `\extrarowheight`（后者来自 `array` 宏包）。

```latex
\renewcommand\arraystretch{1.5}
```

将增加 50% 的基线间距。


特别在使用 `\hline` 的时候，通常更好的做法是增加行高，而不增加基线下的深度。下面的例子演示了 `\extrarowheight` 参数。

```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\begin{document}


\begin{center}
\begin{tabular}{cc}
\hline
Square& $x^2$\\
\hline
Cube& $x^3$\\
\hline
\end{tabular}
\end{center}


\begin{center}
\setlength\extrarowheight{2pt}
\begin{tabular}{cc}
\hline
Square& $x^2$\\
\hline
Cube& $x^3$\\
\hline
\end{tabular}
\end{center}
\end{document}
```
