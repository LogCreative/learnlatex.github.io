---
layout: "lesson"
lang: "zh-Hans"
title: "插图与定位"
description: "本课展示了如何向您的文档中添加插图、如何改变他们的外观以及如何在 PDF 中自动地定位或浮动这些插图。"
toc-anchor-text: "插图"
toc-description: "图片的外观和位置。"
---

## 插图与定位

<span
  class="summary">本课展示了如何向您的文档中添加插图、如何改变他们的外观以及如何自动地定位或浮动这些插图。</span>

为了向 LaTeX 中插入外部来源的图片，使用 `graphicx` 宏包以向 LaTeX 中添加 `\includegraphics` 命令。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}

\begin{document}
This picture
\begin{center}
  \includegraphics[height=2cm]{example-image}
\end{center}
is an imported PDF.
\end{document}
```

您可以添加 EPS, PNG, JPG 以及 PDF 文档。如果您有多于一种后缀的同名图像，那么可以写成 `example-image.png`。（如果您没有指定后缀的话，`graphicx` 宏包会尝试猜测出后缀名。）

您或许注意到在这儿我们使用了一个新的环境：`center`，它用来将图片在页面中水平居中。[稍后](lesson-11) 我们会讨论更多关于间距和定位的内容。

## 更改图片外观

`\includegraphics` 命令为调整图片大小和形状、裁切图片提供了许多选项。其中有些选项是很常用的，需要稍微关注一下。

最常见的就是设定一个图片的宽度和高度，通常被设定为 `\textwidth`（或 `\linewidth`） 和 `\textheight` 的相对值。这里 `\textwidth` 和 `\linewidth` 之间的差别是很微妙的，并且通常是相同的。`\textwidth` 是一整页的文本区域宽度，而 `\linewidth` 是当前行的宽度，会因为不同的行而不同（当启用文档类中的 `twocolumn` 选项时这种差别会非常明显）。LaTeX 会自动缩放图片以保持正确的宽高比例。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}

\begin{document}
\begin{center}
  \includegraphics[height = 0.5\textheight]{example-image}
\end{center}
Some text
\begin{center}
  \includegraphics[width = 0.5\textwidth]{example-image}
\end{center}
\end{document}
```

您也可以尝试采用 `scale` 命令缩放图片，或者指定 `angle` 角度以旋转图片，亦可通过 `clip` 和 `trim` 裁切图片。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}

\begin{document}
\begin{center}
  \includegraphics[clip, trim = 0 0 50 50]{example-image}
\end{center}
\end{document}
```

## 浮动图片

传统排版业，特别是技术文档的排版，图片可能会移动到文档中的其他位置上。这通常被称为 *浮动*（float）。图片通常会被设定为浮动体以至于页面中不会有大面积的留白。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{graphicx}
\usepackage{lipsum}  % 产生填充假文

\begin{document}
\lipsum[1-4] % 只是一些填充文段

Test location.
\begin{figure}[ht]
  \centering
  \includegraphics[width=0.5\textwidth]{example-image-a.png}
  \caption{An example image}
\end{figure}

\lipsum[6-10] % 只是一些填充文段
\end{document}
```

这里 LaTeX 将图片和题注从 `Test location` 处移动到第二页的顶部，因为第一页下方已经没有图片大小的空间了。`ht` 选项影响了 LaTeX 在何处放置浮动体：这两个字母的意思是浮动体可以在原来的地方（`Test location` 旁边）或者是一页的顶部。您最多可以使用四种位置描述符（position specifier）：

- `h` Here 这里（如果可以的话）
- `t` Top 页面顶部
- `b` Bottom 页面底部
- `p` Page 浮动体专页

[稍后](lesson-09)，我们会了解该如何交叉引用浮动体以在文段中产生指向它们的链接。

您或许注意到了我们使用 `\centering` 而不是采用 `center` 环境来水平居中图片。这将避免浮动环境和 `center` 环境都会增加纵向间隔的局面。

## 练习

尝试替代例子中的“标准”图片为您创建的一张图片。

探索 `height`, `width`, `angle` 和 `scale` 可以做到什么。

使用 `width` 来设定一张图片为 `\textwidth` 的相对值、一张图片为 `\linewidth` 的相对值。在包含 `twocolumn` 选项与否时，尝试观察图片的变化。

使用 `lipsum` 来创建相当长的假文，然后尝试将浮动体设定为不同的位置描述符。不同描述符之间是怎么相互影响的？