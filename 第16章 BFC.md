# 一、前言

BFC全称是Block Formatting Context，即块级格式化上下文。BFC最初被定义在CSS2.1规范的[Visual formatting model](https://link.zhihu.com/?target=https%3A//www.w3.org/TR/CSS2/visuren.html)中。

我们先来看看w3c对于BFC的定义：

> Floats, absolutely positioned elements, block containers (such as inline-blocks, table-cells, and table-captions) that are not block boxes, and block boxes with 'overflow' other than 'visible' (except when that value has been propagated to the viewport) establish new block formatting contexts for their contents.

也就是说，有这样几种情况会创建BFC：

- 根元素（\<html />）或其他包含它的元素
- 浮动元素
- 绝对定位元素
- 非块级盒子的块级容器（inline-blocks, table-cells, table-captions等）
- overflow不为visiable的块级盒子

要想明白BFC到底是什么，首先来看看什么是Visual formatting model。

**➦ 视觉格式化模型（Visual Formatting Model）**

视觉格式化模型是用来处理文档并将它显示在视觉媒体上的机制，它让视觉媒体知道如何处理文档。（视觉媒体——user agent通常指的浏览器）

在视觉格式化模型中，文档树的每个元素根据盒模型生成零个或多个盒子。这些盒子的布局受以下因素控制： <u>盒子的尺寸和类型、定位方案（普通文档流，浮动流和绝对定位流）、文档树中元素间的关系、 外部因素（如视口大小，图像本身的尺寸等）</u>。

**➦ 普通文档流**

普通文档流是一种定位方案。

在CSS2.1中，普通文档流包括： 块级盒子的块级格式化上下文/内联级盒子的内联格式化上下文 /块级和内联级盒子的相对定位

在普通文档流内的盒子属于格式化上下文（Formatting Context）。可以属于块级或者内联级，但不能同时属于。块级盒子属于块级格式化上下文。内联盒子属于内联格式化上下文。

**➦ 格式化上下文（Formatting Context）**

Formatting Context，既格式化上下文。用于决定如何渲染文档的一个区域。

不同的盒子使用不同的格式化上下文来布局。

每个格式化上下文都拥有一套不同的渲染规则，他决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

不明白没关系，你可以简单理解为格式化上下文就是**为盒子准备的一套渲染规则**。

常见的格式化上下文有这样几种：

- 【Block formatting context】(BFC)

- 【Inline formatting context】(IFC)

- 【Grid formatting context】(GFC)

- [Flex formatting context](FFC)

# 二、范围

> A block formatting context contains everything inside of the element creating it that is not also inside a descendant element that creates a new block formatting context.

一个BFC包含创建该上下文元素的所有子元素，但不包括创建了新BFC的子元素的内部元素。

换句话说，一个元素不能同时存在两个BFC中

# 三、特性

- 盒子从顶部开始垂直排列
- 两个相邻的盒子之间的垂直距离由外边距（既margin）决定
- 块级格式化上下文中相邻的盒子之间的垂直边距折叠
- 每个盒子的左外边与容器的左边接触（从右到左的格式化则相反），即使存在浮动也是如此，除非盒子建立了新的块格式化上下文
- 形成了BFC的区域不会与float box重叠
- 计算BFC的高度时，浮动子元素也参与计算

# 四、参考

- [MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
- [这一次，完全弄懂BFC](https://zhuanlan.zhihu.com/p/80855885)

