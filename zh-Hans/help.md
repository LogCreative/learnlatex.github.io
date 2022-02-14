---
layout: "page"
lang: "zh-Hans"
title: "使用 learnlatex.org 网站"
description: "本页将介绍 learnlatex.org 网站本身，并指导你正确使用。"
permalink: /zh-Hans/help
---
<script>
  function acesettings() {
      editors['pre0'].execCommand("showSettingsMenu");
  }
</script>

# 帮助

## 站点导航

本课程包含 16 篇核心教程，可通过位于[主页](./)上的[目录]({{ "/" | absolute_url | append: page.lang | append: "/#toc" }})访问。

每篇教程都会链接一篇有关相同主题、但更加深入的教程。你可以先直接读完 16 篇核心教程，而**暂时跳过**这些附加的教程。

课程的末尾，还有若干篇专门介绍使用中文排版的教程。很多宏包在本课程中暂未涉及，它们的示例用法也简单列在后面。

---

## 示例

### 运行示例

教程中的示例均包含一份短小但完整 LaTeX 文档，如下所示：

<!-- Each example consists of a complete small LaTeX document shown within
the page like this: -->

```latex
\documentclass{article}
\usepackage[T1]{fontenc}

\begin{document}
Example text.
\end{document}
```

每个示例都是完整的。但你也可以对它稍作改动，这也许正是教程后面相应的练习。

本网站使用的编辑器是 [ACE](https://ace.c9.io/)。你可以在[网站设置](settings)中自定义编辑器的主题（比如使用深色背景、浅色文字的深色主题）。在任意示例中按 <kbd>Ctrl</kbd>+<kbd>,</kbd>（Mac 里面是 <kbd>⌘</kbd>+<kbd>,</kbd>），也可以很方便地进行设置。此时将会弹出[配置面板](javascript:acesettings())，其中涵盖了 ACE 编辑器的各项配置。

ACE 的代码库中还包含一份[编辑器快捷键列表](https://github.com/ajaxorg/ace/wiki/Default-Keyboard-Shortcuts)。

#### 运行示例的三种方案

* 使用 Overleaf 服务
* 使用 TeXLive.net 服务
* 使用本地安装的 TeX 发行版

##### 使用 Overleaf 服务

Overleaf 是最流行的 LaTeX 在线编辑器之一。点击示例下方的<button>在 Overleaf 中打开</button>，即可提交代码至 [Overleaf](https://www.overleaf.com/about)。

如果你没有注册，或者浏览器没有缓存登录信息，那么会被重定向至 Overleaf 的登录或注册页面。它是免费服务，不过需要你提供一些信息，并接受有关服务条款。

如果浏览器已经保存了你的登录信息，Overleaf 就会在新标签页中打开，同时创建一个新的项目。你可以在其中进行编辑，而 Overleaf 将运行 LaTeX 编译代码，并给出文档输出或错误日志。

与使用 TeXLive.net 不同，你可以将该项目保存起来，以便之后访问。

##### 使用 TeXLive.net 服务

示例下方的 <button>在 TeXLive.net 中运行</button> 按钮，将会把代码提交至 [TeXLive.net](https://texlive.net) 服务[^1]。

TeXLive.net 服务专门为本网站开发，并依靠 [PDF.js](https://mozilla.github.io/pdf.js/) 提供移动端或不支持 PDF 的浏览器中的 PDF 显示。

输出的 PDF 文档（或部分错误日志）会紧跟在示例之后显示。可点击 <button>清除输出</button> 按钮清除输出，（当然也可以直接忽略并继续阅读）。

**TeXLive.net** 无需注册或登录，因此很适合于处理简短的示例。但本网站并未提供保存文档的手段，一旦离开页面，所有的修改都将会丢失。

##### 本地安装的 TeX 发行版

如果本地安装了 TeX 发行版，可以全选并复制示例代码（Windows 快捷键：<kbd>Ctrl</kbd>+<kbd>A</kbd> <kbd>Ctrl</kbd>+<kbd>C</kbd>），即可保存至系统剪贴板中。你可以粘贴到本地的编辑器中，并进行编辑和运行。

### 疑难排查

我们提供的示例均使用最新的 LaTeX 系统。在我们的在线演示系统中它们都能正常工作，因此如果你在运行示例的过程中遇到了问题，不妨先检查自己的 LaTeX 系统是否已更到最新。

---

## 选择 TeX 引擎

提交示例代码后，默认将使用 `pdflatex` 引擎编译。也可以加一行注释来强制使用 `latex`、`pdflatex`、`xelatex`、`lualatex`、`platex` 或者 `uplatex`：

`% !TEX ` *任意文本* `lualatex`

其中开头的空白字符和单词大小写均可忽略，开头、结尾单词之间也可以使用*任意文本*。

这样可以按照一些编辑器的格式要求，使用类似 `% !TEX program=pdflatex` 的语句，不过 `program=` 并不是必须的。需注意只能选择本网站支持的引擎。

在 [这里](more-14) 你可以找到一个通过注释指定使用 LuaLaTeX 的例子。

如果指定 `platex` 或者 `uplatex`，那么便会调用 `dvipdfmx` 程序从 DVI 文件生成 PDF。类似地，如果选择 `latex`，则会调用 `dvips` 和 `ps2pdf` 程序。

如果没有通过 `% !TeX` 注释指定引擎，那么默认会使用 `pdflatex` 编译。默认引擎也可以在[网站设置](settings)中选择。

---

## 选择如何显示输出

如果使用 TeXLive.net，那么 PDF 输出默认将通过 [PDF.js](https://mozilla.github.io/pdf.js/) 显示。这可以保证在大多数浏览器下的一致性。

如果你希望使用浏览器默认的 PDF 阅读器（内置或配置好的外部程序），可以添加如下注释：

`% !TEX ` *任意文本* `pdf`

默认行为相当于把最后的单词换成 `pdfjs`。为了 debug 的方便，即使编译没有出错，有时也需要查看日志文件。此时可以在上面的注释中指定 `log`。

除了使用 `% !TeX` 注释，也可以在[网站设置](settings)中选择默认参数。网站设置是特定于每个浏览器的，因此你可以在移动端指定 `pdfjs`，而在桌面端指定 `pdf` 以使用浏览器默认的 PDF 渲染引擎。

---

## HTML 输出（make4ht、LaTeXML、lwarp）

使用 TeXLive.net 时，还可以指定其他的输出选项，例如 `make4ht`、`LaTeXML` 或 `lwarp`，此时将会生成一个或多个 HTML 子页面。这些参数可以和 `xelatex`、`lualatex` 或是默认的 `pdflatex` 一同使用。

使用如下形式的注释以获得 HTML 输出：

```
% !TeX make4ht
```
{: .noedit :}

也可将 `make4ht` 修改为 `LaTeXML` 或 `lwarp` 以选择对应的程序。你也可以在[网站设置](settings)中选择 `make4ht`、`LaTeXML` 或 `lwarp` 作为默认返回参数。

如果使用本地 TeX 发行版，可通过执行下列命令得到与 `make4ht` 选项相同的结果：

```
make4ht  document.tex "learnlatex4ht,2,mathml,mathjax,svg"
```
{: .noedit :}

附加参数 `-x` 或 `-l` 将会指定 XeLaTeX 或 LuaLaTeX 引擎。在本地运行时，可以使用其他配置。具体参见 [make4ht 手册](https://texdoc.org/pkg/make4ht)。

如需在本地运行 `LaTeXML`，你需要先安装 LaTeXML（它没有被 TeX Live 或 MiKTeX 收录），并执行：

<!-- For `LaTeXML` to run locally, you would need to install LaTeXML (it is not part of TeX Live or MiKTeX)
and use -->

```
latexml document.tex > document.xml
latexmlpost --format=html5 \
   --javascript='https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js' \
   --destination=document.html" document.tex
```
{: .noedit :}

LaTeXML 的更多配置请参考它的 [手册](https://dlmf.nist.gov/LaTeXML/manual/)。

`lwarp` 仍然具有相当的实验性，并且很可能发生改动，因此有关配置不再赘述。当前版本可在[代码库](https://github.com/davidcarlisle/latexcgi/blob/main/lwarp/latexcgilwarp)中找到。

---

[^1]: 在本网站的开发过程中，也曾使用过 [LaTeX.Online](https://latexonline.cc) 和 [LaTeX-on-HTTP](https://github.com/YtoTech/latex-on-http) 服务。对开发者的持续更新及在本网站早期阶段提供的帮助，我们表示感谢。
