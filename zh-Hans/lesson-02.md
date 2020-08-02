---
layout: "lesson"
lang: "zh-Hans"
title: "让 LaTeX 跑起来"
toc-anchor-text: "Anchor"
toc-description: "Description"
---

# Working with LaTeX (Chinese)

与很多软件不同，LaTeX 并不是一个把「全部家当」打包起来的单独应用。相反，它是由一系列程序组成的复杂系统。通常来说，LaTeX 所需的程序可以分为两个部分：

- TeX 发行版
- 文本编辑器（常常是专门为 LaTeX 设计的）

## {{ site.tex }} 发行版

要让 LaTeX 跑起来，核心就是要有一套 TeX 发行版。TeX 发行版是 LaTeX 工作所需的一组「后台」程序和文件，但是大多数情况下，并不需要直接「运行」它们。

在今天，主要有两大 TeX 发行版：[MiKTeX](https://www.miktex.org) 和 [TeX Live](https://tug.org/texlive)。无论是在 Windows、macOS 还是 Linux 平台上，这两个发行版均可使用。在 Windows 上，MiKTeX 具有更为深厚的背景；而在 macOS 上，TeX Live 则被进一步打包在了 [MacTeX](http://www.tug.org/mactex/) 软件套装中。每个发行版都[各有其优势](https://tex.stackexchange.com/questions/20036)，LaTeX 项目组也给出了[更多建议](https://www.latex-project.org/get/)以供您参考。

由于 TeX Live 在所有常见平台上均可使用，并且具有一定的性能优势，因此如果不确定应该安装哪一个发行版，我们建议您选择 TeX Live。

## 编辑器

LaTeX 文档只是纯文本文件，因此可以使用任何文本编辑器进行编辑。但是，使用专为 LaTeX 设计的编辑器将带来更多便利，因为它们往往会提供一键编译、内置 PDF 阅读器以及语法高亮等功能。几乎所有现代的 LaTeX 编辑器都提供 SyncTeX 这一强大的功能：在源代码点击鼠标即可跳转到 PDF 的对应位置，或者反过来，从 PDF 跳转回源代码。

LaTeX 编辑器的数量可能远超您的想象：StackExchange 上有一个[详尽的列表](https://tex.stackexchange.com/questions/339/latex-editors-ides)。Windows 和 Linux 平台上的 TeX Live 和 MiKTeX 均包含有一个基本的编辑器 [TeXworks](https://tug.org/texworks)，而 MacTeX 则打包了 [TeXShop](https://pages.uoregon.edu/koch/texshop/)。

无论您选择哪种编辑器，我们都建议您放在 TeX 发行版**之后**安装，以便该编辑器可以「找到」TeX 发行版并正确进行设置。

## 在线使用

如今，几个强大的在线系统使您完全不必再安装 TeX 发行版和 LaTeX 编辑器。这些网站允许您直接在网页中编辑文档，然后在后台运行 LaTeX，并显示生成的 PDF。

这些网站中的一部分将 LaTeX 与类似文字处理软件的功能结合在一起；而另一部分则偏重让您直接编写 LaTeX 代码，因此更接近本地安装。

有些网站无需登录便可使用，例如 [LaTeX CGI](https://latexcgi.xyz)，这也是本网站编辑和运行示例代码所依赖的系统。对于更完整和复杂的工作，较为成熟的网站都会要求您事先注册。这样您就可以保存自己的工作，同时也能避免网站过载。我们已经配置好了链接，因此您也可以在 [Overleaf](https://www.overleaf.com) 上面编辑示例代码。Overleaf 也是现在最流行的在线 LaTeX 服务。当然还有其他类似的网站，例如 [Papeeria](https://papeeria.com/)。

## 练习

配置好本地 LaTeX 安装，**或者**注册一个在线 LaTeX 服务的账号。如果是前者，则还需要选择一个编辑器：我们建议从 TeXworks 或 TeXShop（见上文）入手，等到您熟悉 LaTeX 的整套流程之后再去尝试其他编辑器。

尽管[在浏览器中也可以运行其他所有的练习](help)，但我们还是希望能帮助您处理真实的文档，因此最好现在就开始准备。
