---
layout: "lesson"
lang: "zh-Hans"
title: "表格"
description: "本课展示了如何在 LaTeX 中构建表格、改变单元格中的对齐选项、对表格添加分割线以及合并单元格。"
toc-anchor-text: "LaTeX 表格"
toc-description: "表格的基本用法。"
---

# 表格

<span
  class="summary">本课展示了如何在 LaTeX 中构建表格、改变单元格中的对齐选项、对表格添加分割线以及合并单元格。</span>

在 LaTeX 中，使用 `tabular` 环境构建表格。本课会假设你已经加载了 `array` 宏包以向 LaTeX 表格添加更多的功能（这些功能因为一些历史原因没有被内置在 LaTeX 内核中）。在导言区添加下面的代码即可继续操作：

```latex
\usepackage{array}
```
{: .noedit :}

为了排版 `tabular` 表格，我们需要告诉 LaTeX 总共有多少列，以及应当怎样对齐。这通常通过一个额外的参数——通常被称为表格导言（table preamble）——来指定 `tabular` 列数。每列通常通过单个字母（被称为引导符，preamble-token）指定。可选的列格式如下：

<!-- don't line wrap this table, markdown seems to not support this -->

| 类型       | 描述 |
| ---        |:-- |
| `l`        | 列左对齐 |
| `c`        | 列居中对齐 |
| `r`        | 列右对齐 |
| `p{width}` | 固定列宽；文字会被自动折行并两端对齐 |
| `m{width}` | 和 `p` 类似，但垂直居中对齐 |
| `b{width}` | 和 `p` 类似，但垂直底部对齐 |
| `w{align}{width}` | 固定列宽，如果太长会稍稍出界。你可以选择水平对齐（align）选项 `l`, `c` 或 `r` |
| `W{align}{width}` | 和 `w` 类似, 但是如果出界的话会收到警告 |

另外，还有一些其他的导言符不定义列，但也可能有用：

<!-- don't line wrap this table, markdown seems to not support this -->

| 类型 | 描述 |
| ---  | :-- |
| `*{num}{string}` | 在表格导言中重复 `string` 引导符 `num` 次。你可以通过这种方式定义相同的列 |
| `>{decl}` | 在当前列的每个单元格前都添加 `decl`（很有用，比如需要对整列设定一个不同的字体时） |
| `<{decl}` | 会在前一列的每个单元格后添加 `decl` |
| <span>`|`</span>  | 添加纵向分割线 |
| `@{decl}` | 将两列之间的空隙替换为 `decl` |
| `!{decl}` | 在两列之间的空隙中央添加 `decl` |

这两个表格列出了 LaTeX 和 `array` 宏包中所有的列描述符。其他宏包提供的一些其他列描述符会在[进一步的细节页面](more-08)给出。

被 `l`, `c`, `r` 标识的列将会根据最宽的单元格自动决定列宽。每一列都需要被声明。如果需要三个居中列，你可以在表格导言使用 `ccc`，当然，因为空格会被忽略掉，`c c c` 也是等同的。

表格主体中，列都是通过 `&` 和号来分隔的，行是通过 `\\` 来另起的。

我们已经了解了制作第一个表格需要的所有知识。下面 `&` 和 `\\` 在代码中是对齐的，这虽然在 LaTeX 中并不是必要的，但是可以让源代码变得更易读。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

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

如果一个表格列包含了太多的文字，仅使用 `l`, `c` 和 `r` 的话你可能会遇到麻烦。可以从下面的例子中观察发生了什么：

<!-- {% raw %} -->

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{cl}
  Animal & Description \\
  dog    & The dog is a member of the genus Canis, which forms part of the
           wolf-like canids, and is the most widely abundant terrestrial
           carnivore. \\
  cat    & The cat is a domestic species of small carnivorous mammal. It is the
           only domesticated species in the family Felidae and is often referred
           to as the domestic cat to distinguish it from the wild members of the
           family. \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

造成这个问题的原因是，`l` 类型的列即使已经超出了页面的范围，也会将所有的内容排版成一行。为了解决它，你可以采用 `p` 类型。这种类型将内容排版为指定宽度的段落，垂直顶部居中——这是你大部分情况下所需要的排版方式。将上面的结果与下面的结果比较一下：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{cp{9cm}}
  Animal & Description \\
  dog    & The dog is a member of the genus Canis, which forms part of the
           wolf-like canids, and is the most widely abundant terrestrial
           carnivore. \\
  cat    & The cat is a domestic species of small carnivorous mammal. It is the
           only domesticated species in the family Felidae and is often referred
           to as the domestic cat to distinguish it from the wild members of the
           family. \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

如果你的表格里有太多列是同样的类型，那么向表格导言重复写入大量描述符就太麻烦了。你可以通过使用 `*{num}{string}` 让事情变得简单一些，这会让 `string` 格式描述符重复 `num` 次。所以 `*{6}{c}` 和 `cccccc` 是等价的。为了展示这一点，下面就是用新学语法重写后的样子：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}

\begin{document}
\begin{tabular}{*{3}{l}}
  Animal & Food  & Size   \\
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

## 添加（行）分割线

在介绍分割线之前，先提个建议：表格中应当少用分割线，而且纵向分割线一般看起来不专业。事实上，在专业表格中，你不应当使用任何标准分割线；取而代之的，你应该熟练使用 `booktabs` 宏包里提供的工具，因此我们这里打算先讨论它。完整起见，我们将标准分割线的相关内容放在了[进一步的细节页面](more-08)中。 

`booktabs` 提供了四种不同的分割线。每一种命令都需要在每一行之前或者在一个分割线之后使用。其中三种分割线命令是：`\toprule`, `\midrule`, `\bottomrule`。顾名思义，你应该清楚这些分割线放在哪儿：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}


\begin{document}
\begin{tabular}{lll}
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

第四种 `booktabs` 提供的分割线命令是 `\cmidrule`，可用来绘制出仅占用指定列范围、而不占满整行的分割线。列范围被表示为一个数字范围：`{`_列号_`-`_列号_`}`。即使你只需要对一列画分割线，也要指定一个范围（范围两端的列号相同罢了）。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{lll}
  \toprule
  Animal & Food  & Size   \\
  \midrule
  dog    & meat  & medium \\
  \cmidrule{1-2}
  horse  & hay   & large  \\
  \cmidrule{1-1}
  \cmidrule{3-3}
  frog   & flies & small  \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

`\cmidrule` 还有其他有用的功能。你可以在小括号中指定对应参数以缩短分割线的任意一端。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{lll}
  \toprule
  Animal & Food  & Size   \\
  \midrule
  dog    & meat  & medium \\
  \cmidrule{1-2}
  horse  & hay   & large  \\
  \cmidrule(r){1-1}
  \cmidrule(rl){2-2}
  \cmidrule(l){3-3}
  frog   & flies & small  \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

你可能猜到了 `r` 和 `l` 的意思是分别缩短分割线**右**（right）端和**左**（left）端。

有时，一条分割线对于分割两行来说可能做的还是太过了，希望通过其他方式将两行更清晰地分隔开。在这种情况下，可以使用 `\addlinespace` 来插入一个小的间隙。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}

\begin{document}
\begin{tabular}{cp{9cm}}
  \toprule
  Animal & Description \\
  \midrule
  dog    & The dog is a member of the genus Canis, which forms part of the
           wolf-like canids, and is the most widely abundant terrestrial
           carnivore. \\
  \addlinespace
  cat    & The cat is a domestic species of small carnivorous mammal. It is the
           only domesticated species in the family Felidae and is often referred
           to as the domestic cat to distinguish it from the wild members of the
           family. \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->


## 合并单元格

在 LaTeX 中，你可以通过 `\multicolumn` 命令水平合并两个单元格，如果需要使用这个命令，必须在输入单元格内容前使用。`\multicolumn` 接受三个参数：

1. 需要合并多少个单元格
2. 合并后单元格的对齐方式
3. 合并后单元格的内容

对齐方式可以使用 `tabular` 中定义的任何方式，但只需要指定**一个**（不是多个）列类型。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}


\begin{document}
\begin{tabular}{lll}
  \toprule
  Animal & Food  & Size   \\
  \midrule
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
  fuath  & \multicolumn{2}{c}{unknown} \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

你也可以在单个单元格上使用 `\multicolumn` 来屏蔽表格导言中对该列的定义。使用下面的方法居中表头：

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}


\begin{document}
\begin{tabular}{lll}
  \toprule
  \multicolumn{1}{c}{Animal} & \multicolumn{1}{c}{Food} & \multicolumn{1}{c}{Size} \\
  \midrule
  dog    & meat  & medium \\
  horse  & hay   & large  \\
  frog   & flies & small  \\
  fuath  & \multicolumn{2}{c}{unknown} \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->

LaTeX 不支持纵向单元格的合并。通常通过将单元格留空的方式，来告诉读者单元格是跨行的。

<!-- {% raw %} -->
```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{array}
\usepackage{booktabs}


\begin{document}
\begin{tabular}{lll}
  \toprule
  Group     & Animal & Size   \\
  \midrule
  herbivore & horse  & large  \\
            & deer   & medium \\
            & rabbit & small  \\
  \addlinespace
  carnivore & dog    & medium \\
            & cat    & small  \\
            & lion   & large  \\
  \addlinespace
  omnivore  & crow   & small  \\
            & bear   & large  \\
            & pig    & medium \\
  \bottomrule
\end{tabular}
\end{document}
```
<!-- {% endraw %} -->


## 练习

使用简单的例子开始试验表格的功能。尝试不同的 `l`, `c` 和 `r` 列对齐描述符。一行中内容太少会发生什么？太多呢？尝试使用 `\multicolumn` 命令产生跨列的单元格。