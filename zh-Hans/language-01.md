---
layout: "lesson"
lang: "zh-Hans"
title: "排版中文"
description: "本教程将展示在 LaTeX 中排版中文的基本方法，主要使用 `ctex` 宏包或文档类。"
toc-anchor-text: "排版中文"
toc-description: "如何优雅地在 LaTeX 中使用中文？"
---

如需排版中文文档，可使用 `ctexart`、`ctexrep`、`ctexbook` 分别代替标准文档类 `article`、`report`、`book`；如果使用其他文档类，则可额外调用 `ctex` 宏包。它们会添加对中文字体的支持，同时还会处理中文排版中的一些细节，包括行距调整、段落缩进、标点符号禁则（如句号、逗号不允许出现在行首）等。文档需要以 UTF-8 编码保存，并建议使用 `xelatex` 或 `lualatex` 编译：

```latex
%!TEX xelatex
\documentclass{ctexart}

\begin{document}
你好，世界！

这是一份含有中文的 \LaTeX{} 文档。
\end{document}
```

`ctex` 文档类 / 宏包会自动处理中西文之间的间距，因此中西文混排时，不需要添加额外的空格。当然，为了代码的可读性，加上空格也无妨。汉字换行时也不会引入多余的空格：

```latex
%!TEX xelatex
\documentclass{ctexart}

\begin{document}
汉字和English单词混排
汉字和 English 单词混排

换行不会带来空格（空一行仍然表示分段）
\end{document}
```

日期以及目录、摘要、参考文献等的标题默认会进行汉化，版面样式根据中文习惯也有所调整：

```latex
%!TEX xelatex
\documentclass{ctexart}

\title{文档标题}
\date{\today}

\begin{document}
\maketitle

\begin{abstract}
这是摘要。
\end{abstract}

\tableofcontents

\section{天地玄黄}
\section{宇宙洪荒}

\end{document}
```

`ctex` 文档类 / 宏包默认会使用宋体作为正文字体（`\textrm` / `\rmfamily`），使用黑体作为无衬线字体（`\textsf` / `\sffamily`）。由于中文字体通常没有斜体或意大利体，因此使用楷体显示 `\emph`、`\textit` 或 `\itshape`。此外，还会使用仿宋显示 `\texttt` 或 `\ttfamily`：

```latex
%!TEX xelatex
\documentclass{ctexart}

\begin{document}
\begin{itemize}
  \item 正文（宋体）
  \item \textsc{无衬线（黑体）}
  \item \textit{楷体}
  \item \texttt{仿宋}
\end{itemize}
\end{document}
```

更多信息请参考 `ctex` 的[宏包文档](https://texdoc.org/pkg/ctex)。有关中文字体配置、标点位置调整，还可以参考 [`xeCJK`](https://texdoc.org/pkg/xecjk) 和 [`luatexja`](https://texdoc.org/pkg/luatexja) 的文档，它们分别是 `ctex` 在使用 `xelatex`、`lualatex` 时底层所调用的宏包。
