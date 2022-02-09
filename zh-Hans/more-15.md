---
layout: "lesson"
lang: "zh-Hans"
title: "更多：处理错误"
description: "本课展示了一些 LaTeX 中更常见的错误，并解释连环错误和静默错误。"
toc-anchor-text: "更多：处理错误"
---


## 在环境结束处报告的错误

一些环境（尤其是 `amsmath` 对齐环境和 `tabularx` 表格环境）会在处理内容前扫描整个环境主体。这就意味着任何环境内的错误都会在最后一行被报告。然而，正如主课所讲的那样，TeX 展示错误内容时仍然会精准定位错误位置。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\usepackage{amsmath}

\begin{document}

\begin{align}
\alpha &= \frac{1}{2}\\
\beta  &= \frak{2}{3}\\
\gamma &= \frac{3}{4} 
\end{align}

\end{document}
```

这里错误会在第 11 行被报告

```
l.12 \end{align}
```
{: .noedit :}

正如下面错误内容所展示的那样，真正的错误发生在第 9 行：

```
! Undefined control sequence.
<argument> ...ha &= \frac {1}{2}\\ \beta &= \frak 
                                                  {2}{3}\\ \gamma &= \frac {...
```
{: .noedit :}


## 由于早先错误而导致的以假乱真错误

当从命令行交互式运行 LaTeX 时，在第一个错误处使用 `x` 来终止运行、编辑文档之后重新运行是可行的。然而，如果您跳过错误（或者是使用的编辑器与在线系统帮您做了这个操作），那么 TeX 就会尝试恢复——这就可能导致几个更多的错误被报告。

所以不要太在意错误报告的 _数目_，永远要专注于修复第一个被报告的错误。


```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\begin{document}
Text_word  $\alpha + \beta$.

More text.
\end{document}
```

这里的错误是下划线 `_` 应该被输入为 `\_`。

TeX 确实会在 _第一个_ 错误信息中正确报告这一点

```
! Missing $ inserted.
<inserted text> 
                $
l.5 Text_
         word  $\alpha + \beta$.
?
```
{: .noedit :}

然而如果您跳过了 `?` 提示，那么之后 TeX 就会通过添加一个 `$` 来修复，从而 `_` 会在数学模式中被视作为下标。之后数学模式会持续被开启直到下一个 `$` 来结束数学模式。因此之后的 `\alpha` 会处于文本模式并产生另一个错误

```
! Missing $ inserted.
<inserted text> 
                $
l.5 Text_word  $\alpha
                       + \beta$.
? 
```
{: .noedit :}


## 不触发错误提示的错误

一些错误（尤其是直到文件结尾都没有被检测到的错误）并不会产生错误提示，而只是在日志中给出一个警告。

如果您使用 TeXLive.net 服务器来尝试下面这个例子，默认情况下会返回一个 PDF 文件。（在开头）添加 `%!TeX log` 来查看日志中的错误信息。

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\begin{document}

 Text {\large some large text) normal size?

\end{document}
```

在这个例子中，字体大小更改被错误地以 `)` 结束，而不是 `}`。这一直都不会被检测到，直到文件结束时，TeX 检测到了仍有一个组（group）尚未被结束。它将会在组开始处（以 `{` 为界）被报告，并不能检测真正的错误因为 `)` 被当做了“正常文本”。

```
(\end occurred inside a group at level 1)

### simple group (level 1) entered at line 5 ({)
```
{: .noedit :}


<script>
  window.addEventListener('load', function(){
      if(editors['pre0'] != null) editors['pre0'].moveCursorTo(8, 15, false);
      if(editors['pre3'] != null) editors['pre3'].moveCursorTo(3, 5, false);
      if(editors['pre6'] != null) editors['pre6'].moveCursorTo(4, 30, false);
  }, false);
</script>
