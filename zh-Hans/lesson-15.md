---
layout: "lesson"
lang: "zh-Hans"
title: "处理错误"
description: "本课展示了 LaTeX 文档中一些常见的错误，并讲解它们意味着什么，以及如何处理它们。"
toc-anchor-text: "处理错误"
toc-description: "应对预料之外的行为。"
---

# 处理错误

<span
  class="summary">本课展示了 LaTeX 文档中一些常见的错误，并讲解它们意味着什么，以及如何处理它们。</span>

与典型的字处理系统不同，LaTeX 是一个编辑/运行/浏览工作循环，一种接近于编程语言编译器的工作方式。因为程序员输入时会犯错，所以需要处理系统报告错误信息。

## 常见错误

本页面给予几个常见错误的例子。每个错误例子都会对错误信息对应的形式进行讨论。

对此可以很有启发的是，尝试这些例子并使用编辑器特性来修复文档，以解决这些错误。

### pdflatex 未找到

人们开始时第一个常见的错误是：

Windows 上

```
'pdflatex' 未被识别为内部或外部命令，可操作程序或批处理文件。
```
{: .noedit :}

或 Linux 上

```
bash: pdflatex: command not found
```
{: .noedit :}

这并不是一个 TeX 错误，而是一个操作系统错误，表明 TeX 并没有被安装或者未被找到。常见的情形是只安装了诸如 TeXworks 或 TeXShop 的 _编辑器_ 但并没有安装诸如 TeX Live 或 MiKTeX 的 TeX 系统。

### TeX 错误信息结构

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\newcommand\mycommand{\textbold{hmmm}}

\begin{document}

My command is used here \mycommand.

\end{document}
```

这会在日志文件中报告一段消息。

```
! Undefined control sequence.
\mycommand ->\textbold 
                       {hmmm}
l.8 My command is used here \mycommand
                                      .
? 
```
{: .noedit :}

* 第一行，以 `!` 开头，给出了错误的基本属性（在这个例子中是未定义命令）。
* 接下来两行表明 TeX 正在处理的代码行，以一处断行表明 TeX 已经处理到的地方。未定义的命令就是最后一个被读取的记号（token），所以在这里就是断行前的最后一个单词 `\textbold`。断行后剩余的记号 `{hmmm}` 可能就是已经被读取的、但尚未被 TeX 执行的参数。
* 此处可能还会有几行来展示更多的错误信息。
* 最后以 `l.` 开头，并跟随一个行号，之后就是源文件中错误发生的代码行。
* 最后一行是一个问号 `?`。如果 TeX 是以交互模式执行的，那么此时就可以向 TeX 输入指令。但是大部分编辑器和在线系统都会以一种批处理方式运行，所以不会在错误处暂停，而是跳过此处，并尝试处理完文档的剩余部分。如果是交互模式，在命令行输入 `s` 会让 TeX 以这种批处理模式继续执行。


这里要注意 TeX 并不会在定义处检测到这种错误：实际上，如果 `\mycommand` 被定义但从未被使用过，那么就不会产生任何错误。所以尽管被报告错误产生在第 8 行，但是“真正的”错误是在第 4 行的定义处出现的。所以看清楚整个错误信息是很重要的。

需要意识到有些编辑器只会展示错误日志的一行“总结”，下面的消息可能很容易会被错误理解：

`line 8: undefined command: ...\mycommand`

它看起来就像是 `\mycommand` 没有被定义一样。


### 未配对括号

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage[leqno}{amsmath}

\begin{document}

\end{document}
```

这里错误出现于结束可选参数时无法匹配的 `}`。这个大括号会导致 LaTeX 解析选项时发生错误，您将得到一个没有帮助的内部错误：

```
! Argument of \@fileswith@ptions has an extra }.
```
{: .noedit :}

虽然这个错误信息并没有什么帮助，但是接下来的两行会准确地展示错误的位置，并通过断行展示 TeX 已经处理到的部分：

```
l.4 \usepackage[leqno}
                      {amsmath}
```
{: .noedit :}



### 未找到文件

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage{amsmathz}

\begin{document}

\end{document}
```

这将产生如下错误：

```
! LaTeX Error: File `amsmathz.sty' not found.
```
{: .noedit :}

注意，两种原因会导致同样的错误：一是和这里一样的误输入，可以通过修正为正确的宏包名解决；二是确实找不到文件，需要安装对应的宏包。

### 行间公式中的空行

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\begin{document}

Some text
\begin{equation}

  1=2

\end{equation}

\end{document}
```

会产生相对隐晦的错误：

```
! Missing $ inserted.
```
{: .noedit :}

但修复起来是很容易的，行间公式不允许空行，空行应该被删除。

## 练习

尝试修复例子中的错误。

尝试写一个充满 bug 的小文档并查看错误信息的形式。

<script>
  window.addEventListener('load', function(){
      if(editors['pre2'] != null) editors['pre2'].moveCursorTo(3, 31, false);
      if(editors['pre4'] != null) editors['pre4'].moveCursorTo(3, 18, false);
      if(editors['pre7'] != null) editors['pre7'].moveCursorTo(3  , 20, false);
      if(editors['pre9'] != null) editors['pre9'].moveCursorTo(7, 0, false);
  }, false);
</script>
