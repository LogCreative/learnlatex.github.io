---
layout: "lesson"
lang: "zh-Hans"
title: "更多：逻辑结构"
description: "本课展示了如何设定文档标题，以及如何制作描述列表。"
toc-anchor-text: "更多：逻辑结构"
---

## 文档标题

LaTeX 对于文档标题提供了一些逻辑标记命令：设定「元数据」的三个命令和使用它的一个命令。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}
\author{A.~N.~Other \and D.~Nobacon}
\title{Some things I did}
\date{1st April 2020}
\maketitle

Some normal text.
\end{document}
```

正如所见的那样，`\author`、`\title` 和 `\date` 命令保存信息，`\maketitle` 使用这些信息。你也可以使用 `\and` 分隔多个作者。`\author`、`\title` 和 `\date` 命令需要在 `\maketitle` 之前使用。在这个例子中我们将其置于文档主体中；它们也可以在导言区使用，只是 `babel` 简写将不会在这个地方被启用。

`\maketitle` 提供的设计样式依赖于文档类（见[第 5 课](lesson-05)）。对于想要做自定义设计的人来说，可以使用 `titlepage` 环境，但是这已经超出了本课程的范围。如果你想做出自己的文档设计，可以使用一个类似于 `memoir` 的可自定义类，或者从 LaTeX 基础类的其中一个（比如 `book` 文档类）作为出发点。

## 描述列表

除了有序和无序列表，LaTeX 还提供了不太常见的另一种列表「描述列表」。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\begin{document}

\begin{description}
\item[Dog:] member of the genus Canis, which forms part of the wolf-like canids,
  and is the most widely abundant terrestrial carnivore.
\item[Cat:] domestic species of small carnivorous mammal. It is the only
  domesticated species in the family Felidae and is often referred to as the
  domestic cat to distinguish it from the wild members of the family.
\end{description}

\end{document}
```

## 练习

尝试设定不同的 `\author`，`\title` 和 `\date` 信息来测试 `\maketitle`。哪一个是你**必须**要设定的？必须要有作者、标题以及日期吗？

制作一些描述列表，嵌套使用这些列表（有序、无序或描述列表）。
