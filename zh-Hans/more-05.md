---
layout: "lesson"
lang: "zh-Hans"
title: "更多：使用文档类来切换设计"
description: "本课提供了关于 LaTeX 中更专用文档类的信息。"
toc-anchor-text: "更多：使用文档类来切换设计"
---

## 期刊专用文档类

很多学术期刊提供用于提交的 LaTeX 文档类。这些文档类一般都会设定与最终期刊相似的排版，虽然受制于字体的使用等其他因素。如果有文档类可用的话，一般都会由编辑部直接提供，也应该由编辑部提供关于功能方面的适当细节。大部分这种文档类在 [CTAN](https://ctan.org) 和标准 TeX 发行版中都可用。

## 用于演示的文档类

需要很多特别处理的一个领域就是创建演示文稿。`slides` 文档类是为了传统印制幻灯片编写的，对于屏幕演示没有任何特殊的支持。两种文档类被开发出来用于后者的用途，并被广泛使用：`beamer` 和 `powerdot`。因为 `beamer` 可能是更加常见的一种，我们将会给出它如何工作的一个例子：

```latex
\documentclass{beamer}
\usepackage[T1]{fontenc}
\begin{document}

\begin{frame}
  \frametitle{A first frame}
  Some text
\end{frame}

\begin{frame}
  \frametitle{A second frame}
  Different text
  \begin{itemize}
    \item<1-> First item
    \item<2-> Second item
  \end{itemize}
\end{frame}

\end{document}
```

这里展示了两个重要的想法。首先，`beamer` 将文档分割成帧，每一帧都可以产生多于一个幻灯片（页）。其次，`beamer` 向普通的 LaTeX 语法添加功能以允许代码中的一些部分“每次显示一点”。这很强大，但是也比我们能够涉及的已经更复杂了：可以查看[这个博文](https://www.texdev.net/2014/01/17/the-beamer-slide-overlay-concept/)以了解更多。

## 产生图片的文档类

有些情况下，您需要使用 LaTeX 制作图像（可能是很多文本的那种）。通常请款不修改，在这一“页”中您不需要除了内容本身的其他任何东西。最简单的做法就是使用 [`standalone`](https://ctan.org/pkg/standalone) 文档类。它为了包裹排印出的内容自动设定页面大小。

```latex
\documentclass{standalone}
\usepackage[T1]{fontenc}
\begin{document}
A simple document: this will be a very small box!
\end{document}
```
