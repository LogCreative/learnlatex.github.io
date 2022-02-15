---
layout: "lesson"
lang: "zh-Hans"
title: "更多：数学公式"
description: "本课展示了更多的 amsmath 对齐环境、如何在数学环境中加粗、数学扩展宏包 mathtools 以及使用 Unicode 输入于数学环境。"
toc-anchor-text: "更多：数学公式"
---

## 更多的 `amsmath` 公式对齐方式

除了在主课中展示的 `align*` 环境，`amsmath` 还有其他几种构造行间数学环境的方法。值得注意的有：用于不需要对齐多行公式的 `gather`，用于单个大型公式多行分割的 `multline`（将第一行左对齐，最后一行右对齐）。所有环境对应的 `*` 形式将默认省略公式编号。

```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}

\usepackage{amsmath}

\begin{document}

Gather
\begin{gather}
  P(x)=ax^{5}+bx^{4}+cx^{3}+dx^{2}+ex +f\\
  x^2+x=10
\end{gather}

Multline
\begin{multline*}
   (a+b+c+d)x^{5}+(b+c+d+e)x^{4} \\
    +(c+d+e+f)x^{3}+(d+e+f+a)x^{2}+(e+f+a+b)x\\
    + (f+a+b+c)
\end{multline*}
\end{document}
```

### 数学对齐环境中的列

`amsmath` 对齐环境被设计为每两个对齐列的第一栏右对齐、第二栏左对齐。这将允许展示多个公式，每个公式内部的列向它关系符号的方向对齐。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}
\begin{document}
Aligned equations
\begin{align*}
a &= b+1   &  c &= d+2  &  e &= f+3   \\
r &= s^{2} &  t &=u^{3} &  v &= w^{4}
\end{align*}

\end{document}
```


另外，还有以 `ed` 结尾的行间数学环境变种，来在大型公式中产生子环境。比如说，`aligned` 和 `gathered` 分别是 `align` 和 `gather` 环境的变种。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}
\begin{document}
Aligned:
\[
\left.\begin{aligned}
a&=b\\
c&=d
\end{aligned}\right\}
\Longrightarrow
\left\{\begin{aligned}
b&=a\\
d&=c
\end{aligned}\right.
\]
\end{document}
```

`aligned` 有着与 `tabular` 很像的一个可选位置参数。对于想要对齐行内数学公式最顶行很有用——可以在下面的例子中比较列表中的两项。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{amsmath}
\begin{document}
\begin{itemize}
\item 
$\begin{aligned}[t]
a&=b\\
c&=d
\end{aligned}$
\item 
$\begin{aligned}
a&=b\\
c&=d
\end{aligned}$
\end{itemize}
\end{document}
```

## 数学环境中的加粗

标准 LaTeX 对插入加粗符号于数学环境有两种方法。若让整个公式加粗，在输入公式前使用 `\boldmath`；若让单独的字母或单词加粗，可以使用 `\mathbf` 以产生直立罗马加粗体。

```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}

\begin{document}


$(x+y)(x-y)=x^{2}-y^{2}$

{\boldmath $(x+y)(x-y)=x^{2}-y^{2}$ $\pi r^2$}

$(x+\mathbf{y})(x-\mathbf{y})=x^{2}-{\mathbf{y}}^{2}$
$\mathbf{\pi} r^2$ % \mathbf 的不良使用
\end{document}
```

如果你使用类似于正常字重的粗体符号（正如 `\boldmath` 所用的那样），那么你可以用 `bm` 宏包里的 `\bm` 命令。注意 `\bm` 对于像 `=` 和希腊字母之类的符号也适用。（注意 `\mathbf` 在上面的例子中对于 `\pi` 并没有作用。）

```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}
\usepackage{bm}

\begin{document}

$(x+\mathbf{y})(x-\mathbf{y})=x^{2}-{\mathbf{y}}^{2}$

$(x+\bm{y})(x-\bm{y}) \bm{=} x^{2}-{\bm{y}}^{2}$

$\alpha + \bm{\alpha} < \beta + \bm{\beta}$

\end{document}
```

## Mathtools

`mathtools` 宏包会加载 `amsmath` 并添加一些额外的功能，例如，提供允许指定列对齐方式的 `amsmath` 矩阵环境变种。
```latex
\documentclass[a4paper]{article}
\usepackage[T1]{fontenc}
\usepackage{mathtools}

\begin{document}

\[
\begin{pmatrix*}[r]
  10&11\\
   1&2\\
  -5&-6
\end{pmatrix*}
\]

\end{document}
```

## Unicode Math

将会在[第 14 课](lesson-14)看到，也有使用 OpenType 字体的 TeX 变种引擎。默认情况下，这些引擎还是会使用经典 TeX 数学字体，但允许你加载 `unicode-math` 宏包来使用 OpenType 数学字体。该宏包的细节已经超出本课程的范畴，可参见[宏包文档](https://texdoc.net/pkg/unicode-math)。当然，我们将在此给出一个小例子。

```latex
% !TEX lualatex
\documentclass[a4paper]{article}
\usepackage{unicode-math}
\setmainfont{TeX Gyre Pagella}
\setmathfont{TeX Gyre Pagella Math}

\begin{document}

One two three
\[
\log \alpha + \log \beta = \log(\alpha\beta)
\]

Unicode Math Alphanumerics
\[A + \symfrak{A}+\symbf{A}+ \symcal{A} + \symscr{A}+ \symbb{A}\]

\end{document}
```
