---
layout: "start"
lang: "zh-Hans"
title: Learn LaTeX online for free in beginner friendly lessons
description: "Learn LaTeX in 16 beginner friendly lessons. Take your first steps with LaTeX, a document preparation system designed to produce high-quality typeset output."
permalink: /zh-Hans/
---

# Learn LaTeX

<h2 class="heading__introduction">Take your first steps with LaTeX, a document preparation system designed to produce high-quality typeset output.</h2>

<div
  class="text-columns">
  <section>
    <h3 
      class="text-columns__heading"
      >介紹</h3>
    <p>LaTeX can be scary for new users as it is <em>not</em> a word processor, 
    and because it is not a single program. Our aim is to help you get 
    started with LaTeX from the basics, installation, to writing code, without 
    trying to show you <em>everything</em> in one go. <a href="./mission">More on our mission &hellip;</a></p>
  </section>
  <section>
    <h3
      class="text-columns__heading"
      >這個怎麼運作</h3>
      <p>We have taken 16 of the most important things you will need to know, and made them into short <em>lessons</em> which should not take long to cover. In each lesson, we give lots of examples of what you would write. You can edit and run them in this website. <a href="./help#examples">More on examples &hellip;</a></p>
  </section>
</div>

<h2 
  class="heading__toc" 
  id="toc"
  >經驗教訓</h2>

<p
  class="paragraph__toc"
  >We have included a <b>More on this topic</b> page for each lesson. This extra information is there to support you when you need the detail, but should not get in your way if you don't.</p>

{% include toc-lessons.html prefix="zh/lesson" %}

<h2
  class="heading__toc"
  >Additional lessons</h2>
<ul 
  class="lessons-toc">
  {% include toc-additional-lessons.html prefix="zh/language" %}
  {% include toc-additional-lessons.html prefix="zh/extra" %}
</ul>

## Going further

We cover getting more information in [the last lesson](./lesson-16), but it is worth saying now that getting access to a book about LaTeX is still the best way to learn the details. We give some recommendations in the last lesson.

## 欢迎来到 learnlatex.org！

本网站旨在帮您迈出使用 LaTeX 的第一步。LaTeX 是一个用来排版高质量作品的文档准备系统。对于新手而言，LaTeX 可能会有些吓人，因为它既**不是**文字处理软件，也不是一个简单的程序。我们这里的目标是帮助您入门，而并非一口气向您展示**所有**的东西。

为此，我们将您需要了解的 16 件最重要的事情做成了简短的「课程」。每节课的内容都非常集中，因此无需花费过多时间来学习。在每节课中，我们都提供了一些辅助您理解的例子，它们可以直接在线尝试。

我们知道，大家想要学习的东西将远超这短短 16 节课程所能涵盖的范围。因此，为了在您需要更多信息时提供指导，我们在每节课程中都包含了一个「延伸阅读」的页面。这些额外的内容将在您想要了解更多细节时助以一臂之力——当然，如果暂时不需要，它们也不会妨碍到您。

## 如何使用示例

本网站提供了众多示例以辅助您的学习。在[第 2 课](lesson-02)中，我们将讨论如何使用 LaTeX，包括在线使用和本地安装。为了帮助您入门，我们已经配置好了示例，您可以直接在本网站编辑和运行。我们还将它们链接到了 [Overleaf](https://www.overleaf.com)，这是时下最流行的在线 LaTeX 编辑服务之一。但不必担心，您同样也可以在本地计算机上使用这些示例。在[帮助页面](help)，您可以获取到更多有关如何使用示例的信息。

我们的示例基于最新版本的 LaTeX。在本网站的在线演示系统中，它们都应当能正常使用。因此，如果您在使用我们提供的示例时遇到了问题，则可能需要检查本地的 LaTeX 系统是否是最新版本的。

## 课程目录

{% include toc.html  prefix="zh-Hans/lesson" %}

### learnlatex.org/zh-Hans 中的额外课程

{% include toc.html  prefix="zh-Hans/language" %}

## 进一步学习

这里的课程并不能涵盖关于 LaTeX 的全部内容；我们希望为您提供足够的入门知识，并让您能够**理解**从其他地方获取的示例和建议。需要指出的是，深入学习 LaTeX 的最佳方案仍然是阅读有关的书籍。具体信息和更多建议请参考本课程的[最后一课](lesson-16)。

最后，我们提供了一组简短的示例，用来展示了那些本课程未涉及到的主题，以及相关 LaTeX 宏包的用法。

{% include toc.html prefix="zh-Hans/extra" %}
