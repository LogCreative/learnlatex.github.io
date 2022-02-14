---
layout: "lesson"
lang: "zh-Hans"
title: "更多：插图与定位"
description: "本课对于如何更好地命名和存储用于 LaTeX 的图片、如何在 LaTeX 中制作图片给出了更多的细节。"
toc-anchor-text: "更多：插图与定位"
---

## 命名图片文件

由于 LaTeX 工作在很多计算机平台上，所以文件名理应需要受到一些考虑。最安全的方式就是将图片命名得简单点，尤其注意不要有空格。比如，如果您想通过把所有的图片放在一个子文件夹中来整理文件，那么像 `\includegraphics[width=30pt]{pix/mom.png}` 这样的命令就既方便也不会过时。

文件名中包含空格在传统上都会有点问题，虽说现在已经被广泛支持了。然而，如果您在名称中包含空格，然后遇到了问题，那么第一步应该尝试删去这些空格。

重音字符在支持上有点说不准——在某些系统（特别是 Windows）会有问题。如果您在含有重音字符名称的文件上发现了问题，尝试只使用 ASCII 字符用于测试。

## 在子文件夹中存储图片

放置源文件的一种通常方法是将所有的图片文件放在一个子文件夹中。您可以使用相对路径，正如上面所展示的那样。注意到 `/` 字符被用来分隔路径部件（**甚至在 Windows 上也如此**）。

如果您有很多图片，可能想要提前设定一个子目录来使用它们。这可以通过使用 `\graphicspath` 来实现。注意对每一个子文件夹项都包裹大括号，比如，为了同时包含 `figs` 和 `pics` 两个子文件夹，我们需要：

<!-- {% raw %} -->
```latex
\graphicspath{{figs/}{pics/}}
```
<!-- {% endraw %} -->

特别注意这里文件夹结尾的 `/` 符号。

## 制作图片

正如之前所讨论的，LaTeX 可以轻松地使用大多数来源的图片，其中包括从科学软件生成的统计图。使用外部来源图片的时候，需要尽可能保存为 PDF，因为这是一种可缩放的格式。如果您确实想要创建一个位图，就需要输出尽可能高分辨率的图片。您可以通过 [Inkscape](https://inkscape.org/) 制作可包含 LaTeX 标注的鼠绘图像。另一种替代品是 [Asymptote](https://www.ctan.org/pkg/asymptote)，以扩展这些绘图技巧于三维空间。这两个软件会输出图片文件，以插入于文档中。

您也可以创作为 LaTeX 专门适配的极高精度绘图，并包含匹配文档格式的公式和标注。您可以在文档中通过 [Ti*k*Z](https://ctan.org/pkg/pgf) 直接绘制图像。这虽然很方便但也会让文档变得复杂，并需要更多的依赖。另一种替代品是 [PSTricks](https://ctan.org/pkg/pstricks-base)。

## 放置浮动体

LaTeX 的浮动体放置是相对复杂的。最常见的需求是将图片在输出中放置在对应于输入的位置上。`float` 宏包可以实现这一点。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}
\usepackage{lipsum}  % 用于填充假文
\usepackage{float}

\begin{document}
\lipsum[1-7]
\begin{figure}[H]
  \centering
  \includegraphics[width=0.5\textwidth]{example-image}
  \caption{An example image}
\end{figure}
\lipsum[8-15]
\end{document}
```

注意 `H` 选项，它会将图片「就放在这儿」。然而通常不推荐使用 `H`，因为它可能在您的文档中产生大片区域的空白。

## 其他类型的浮动体

我们[很快会看到](lesson-08)可以在浮动体中放置表格——置于 `table` 环境中。当然，我们并不是必须要将图片放在 `figure` 环境中或将表格放在 `table` 环境中——这只是一个通常做法。

您或许需要其他类型的浮动环境——每一种类型都可被单独地插入，对此可以使用 [`trivfloat`](https://ctan.org/pkg/trivfloat) 宏包，它只提供了一个命令 `\trivfloat`，用以创建新的浮动体类型。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}
\usepackage{lipsum}  % 用于填充假文
\usepackage{trivfloat}
\trivfloat{image}

\begin{document}
\begin{image}
  \centering
  \includegraphics[width=0.5\textwidth]{example-image}
  \caption{An example image}
\end{image}
\end{document}
```