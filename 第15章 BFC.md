



# 一、前言

在讲 BFC 之前，我们先来了解一下常见的定位方案，定位方案是控制元素的布局，有三种常见方案:

- 普通流 (Normal-Flow)

> 在普通流中，元素按照其在 HTML 中的先后位置至上而下布局，在这个过程中，行内元素水平排列，直到当行被占满然后换行，块级元素则会被渲染为完整的一个新行，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。

- 浮动 (Float)

> 在浮动布局中，元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移，其效果与印刷排版中的文本环绕相似。

- 绝对定位 (Absolut-Position)

> 在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

# 二、概念

Formatting context（格式化上下文） 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

那么 BFC 是什么呢？

BFC 即 **B**lock **F**ormatting **C**ontexts (块级格式化上下文)，它属于上述定位方案的普通流。

**具有 BFC 特性的元素可以看作是隔离了的 <mark>独立容器</mark>，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。**

通俗一点来讲，可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

常见的格式化上下文有这样几种：

- BFC：**B**lock **F**ormatting **C**ontext

- IFC：**I**nline **F**ormatting **C**ontext

- GFC：**G**rid **F**ormatting **C**ontext

- FFC：**F**lex **F**ormatting **C**ontext

# 三、触发BFC

只要元素满足下面任一条件即可触发 BFC 特性：

- 根元素：`<html>`
- 浮动元素：`!none`
- 绝对定位元素：`fixed && absolute`
- display：`inline-block && table-cell && flex`
- overflow：`!visible `

# 四、解决了什么问题❓

BFC（块级格式化上下文）解决了以下问题：

1. 清除浮动：在一个元素内创建 BFC，可以防止浮动元素溢出到其父元素外部。
2. 避免 margin 重叠：处于同一 BFC 内的相邻块级元素的垂直 margin 不会重叠。
3. 创建独立的布局上下文：BFC 可以将一个元素从文档流中拆分出来，使其不受外部元素影响，从而实现更精细的布局。

# 五、参考

- [MDN >>](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
- [这一次，完全弄懂BFC >>](https://zhuanlan.zhihu.com/p/80855885)
- [10 分钟理解 BFC 原理 >>](https://zhuanlan.zhihu.com/p/25321647)

