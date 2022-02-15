---
layout: "lesson"
lang: "zh-Hans"
title: "更多：组建更长的文档"
description: "本课展示了如何制作索引以及如何使用 imakeidx 宏包以自动化流程。"
toc-anchor-text: "更多：组建更长的文档"
---

## 制作索引

取决于正在编写的文档类型，你有可能想要制作索引。这个过程有点像制作参考文献，因为它也使用辅助文件。幸运的是，`imakeidx` 宏包将这个过程全部自动化了。对此，我们需要对 LaTeX 下达三个指令：

- `\makeindex` 命令，用于开启索引创建过程
- `\index` 命令，用于标记索引项
- `\printindex` 命令，用于排印索引

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage{imakeidx}
\makeindex
\begin{document}
Some text about Foo\index{foo}.
More text\index{baz!bar}.
Even more text\index{alpha@$\alpha$}.
More text about a different part of baz\index{baz!wibble}.

\clearpage
Some text about Foo\index{foo} again, on a different page.
Even more text\index{beta@$\beta$}.
Even more text\index{gamma@$\gamma$}.
\printindex
\end{document}
```

我们在这里展示了索引的两个功能：使用 `!` 划分子级，使用 `@` 来排印一个不同于「排序文本」的索引内容。关于索引，还有很多自定义的可能，可以尝试一些例子然后看看它是怎么工作的。