---
layout: "lesson"
lang: "zh-Hans"
title: "更多：字体与 Unicode 引擎"
description: "本课对于想要在文档中插入 Lua 代码的用户展示了一个基本的 Lua 例子。"
toc-anchor-text: "更多：字体与 Unicode 引擎"
---



## Lua

LuaTeX 引擎提供了类似于 XeTeX 访问 OpenType 字体的方式，`fontspec` 宏包大部分的使用方法在两种引擎中工作的一样好。

LuaTeX 也在其它方式上扩展了 TeX，值得注意的一点就是可以嵌入 Lua 脚本语言。这是一种对于习惯“主流”编程语言的人来说更熟悉的编程风格。这也提供了一种能够访问 TeX 系统内部工作方式并通过替换为 Lua 新代码来更改行为的可能。

本课程并不涵盖 Lua 编程的内容，这里展示一个计算 2π 的简单例子。

```latex
%!TEX lualatex
\documentclass{article}

\begin{document}

$ 2\pi \approx \directlua{ tex.print(2 * math.pi) } $

\end{document}
```
