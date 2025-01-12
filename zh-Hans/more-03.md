---
layout: "lesson"
lang: "zh-Hans"
title: "更多：LaTeX 文档基本结构"
description: "本课对于如何运行 LaTeX、使用的特殊字符、以及如何向输出的 PDF 中插入特殊字符提供了更多的细节。"
toc-anchor-text: "更多：LaTeX 文档基本结构"
---

## 运行 LaTeX

正如[之前提到过的](lesson-02)，LaTeX 文档只是普通文本。为了验证这一点，可以尝试在一个简单的文本编辑器（比如 Windows 上的记事本）打开你的第一个文档。你应该会看到与 LaTeX 专用编辑器中一样的文本，只是没有对关键词的高亮。

你也可以在不使用编辑器来将文档转换为 PDF —— 使用命令行或终端（当然如果不熟悉命令行也不用担心）。如果你**熟悉**命令行的话，可以导航到包含你 `.tex` 源文件的目录中，然后运行

`pdflatex first`

或者

`pdflatex first.tex`

来排版 PDF。注意 `.tex` 后缀名是可选的：LaTeX 会默认文档以 `.tex` 结尾，除非你特别指定了后缀名。

## 特殊字符

如果你需要排印一个特殊字符，大多数情况下你只要简单地在它前面添加反斜杠，例如 `\{` 可以用来排印一个字面量 `{`。当然在小部分的情况下，你需要使用一个更长的命令：

| 符号 | 短命令 <br><small>(数学和文本模式)</small> | 长命令 <br><small>(文本模式)</small> |
| --- | --- | --- |
| `{`    | `\{`          | `\textbraceleft`  |
| `}`    | `\}`          | `\textbraceright` |
| `$`    | `\$`          | `\textdollar`     |
| `%`    | `\%`          |                   |
| `&`    | `\&`          |                   |
| `#`    | `\#`          |                   |
| `_`    | `\_`          | `\textunderscore` |
| ``\``  |               | `\textbackslash`  |
| `^`    |               | `\textasciicircum`|
| `~`    |               | `\textasciitilde` |

对于最后三个字符没有可用的短命令，是因为 `\\` 被用来指定断行，`\~` 和 `\^` 被用来在仅使用 ASCII 字符输入的情况下排印波浪和扬抑重音。