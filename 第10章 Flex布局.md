Flexbox 演示站：https://xluos.github.io/demo/flexbox/

MDN：https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex

# 概述

网页布局（layout）是 CSS 的一个重点应用。

![](IMGS/flex_01.gif)

布局的传统解决方案，基于[盒状模型](https://developer.mozilla.org/en-US/docs/Web/CSS/box_model)，依赖 [`display`](https://developer.mozilla.org/en-US/docs/Web/CSS/display) 属性 + [`position`](https://developer.mozilla.org/en-US/docs/Web/CSS/position)属性 + [`float`](https://developer.mozilla.org/en-US/docs/Web/CSS/float)属性。它对于那些特殊布局非常不方便，比如，[垂直居中](https://css-tricks.com/centering-css-complete-guide/)就不容易实现。

![](IMGS/flex_02.png)

2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

![](IMGS/flex_support.jpg)

Flex 布局将成为未来布局的首选方案，本文介绍它的语法。

# Flex 布局是什么？

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。

```css
.box {
  	display: flex;
}
```

行内元素也可以使用 Flex 布局。

```css
.box {
  	display: flex;
}
```

Webkit 内核的浏览器，必须加上`-webkit-` 前缀。

```css
.box {
  	display: -webkit-flex; /* Safari */
  	display: flex;
}
```

> 注意：设为 Flex 布局以后，子元素的 `float`、`clear` 和 `vertical-align` 属性将失效。

# 基本概念

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![](IMGS/flex_concept.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做 `main start`，结束位置叫做 `main end`；交叉轴的开始位置叫做 `cross start`，结束位置叫做 `cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做 `main size`，占据的交叉轴空间叫做 `cross size`。

# 容器的属性

以下6个属性设置在容器上：

- `flex-direction`
- `flex-wrap`
- `flex-flow`
- `justify-content`
- `align-items`
- `align-content`

## flex-direction *

`flex-direction` 属性决定主轴的方向（即子元素的排列方向）。

```css
.box {
  	flex-direction: row | row-reverse | column | column-reverse;
}
```

![](IMGS/flex_direction.png)

该属性有四个值：

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

## flex-wrap *

默认情况下，子元素都排在一条线（又称"轴线"）上。`flex-wrap` 属性定义，如果一条轴线排不下，如何换行。

![](IMGS/flex_t.png)

```CSS
.box{
	  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

该属性有以下三个值：

- nowrap：（默认），不换行

  ![](IMGS/flex_nowrap.png)

- wrap：换行，第一行在上方

  ![](IMGS/flex_wrap.png)

- wrap-reverse：换行，第一行在下方

  ![](IMGS/flex_wrap_reverse.png)


## flex-flow

`flex-flow` 属性是 `flex-direction` 属性和 `flex-wrap` 属性的简写形式，默认值为 `row nowrap`。

```css
.box {
 	 flex-flow: <flex-direction> || <flex-wrap>;
}
```

## justify-content *

`justify-content` 属性定义了子元素在主轴上的对齐方式。

```css
.box {
  	justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

该属性有5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

- `flex-start`（默认值）：左对齐

  ![](IMGS/flex_justify_content_start.png)

- `flex-end`：右对齐

  ![](IMGS/flex_justify_content_end.png)

- `center`： 居中

  ![](IMGS/flex_justify_content_center.png)

- `space-between`：两端对齐，子元素之间的间隔都相等。

  ![](IMGS/flex_justify_content_space_between.png)

- `space-around`：每个子元素两侧的间隔相等。所以，子元素之间的间隔比项目与边框的间隔大一倍。

  ![](IMGS/flex_justify_content_space_around.png)

## align-items *

`align-items` 属性定义项目在交叉轴上如何对齐。

```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

该属性与`justify-content` 类似，可设置5个属性值，具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

- `flex-start`：交叉轴的起点对齐。

  ![](IMGS/flex_align_items_start.png)

- `flex-end`：交叉轴的终点对齐。

  ![](IMGS/flex_align_items_end.png)

- `center`：交叉轴的中点对齐。

  ![](IMGS/flex_align_items_center.png)

- `baseline`: 子元素的第一行文字的基线对齐。

  ![](IMGS/flex_align_items_baseline.png)

- `stretch`（默认值）：如果子元素未设置高度或设为auto，将占满整个容器的高度。

  ![](IMGS/flex_align_items_stretch.png)

## align-content *

`align-content ` 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```css
.box {
 	 align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

该属性可以设置6个值：

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴（需设置高度为auto）。

![](IMGS/flex_align_content.png)

> 提示：为了美观，前面五个元素我都设置了 `margin:10px 0`，而 stretch 为了直观的显示其效果，我没有设置。

# 元素的属性

以下6个属性设置在子元素上：

## order

`order` 属性定义子元素的排列顺序。数值越小，排列越靠前，默认为0。

```css
.item {
 	 order: <integer>;
}
```

![](IMGS/flex_order.png)

## flex-grow

`flex-grow ` 属性定义子元素的放大比例，默认为`0`，即就算存在剩余空间，也不放大。如果所有子元素的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

```css
.item {
  flex-grow: <number>; /* default 0 */
}
```

![](IMGS/flex_grow.png)

## flex-shrink

`flex-shrink `属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

![](IMGS/flex_shrink.png)

如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

> 结论：
>
> 1、如果父级的空间足够：`flex-grow`有效，`flex-shrink`无效。
>
> 2、如果父级的空间不够：`flex-shrink` 有效，`flex-grow`无效。

## flex-basis

`flex-basis` 属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。

```css
.item {
 	 flex-basis: <length> | auto; /* default auto */
}
```

![](IMGS/flex-basis.png)

它可以设为跟 `width` 或 `height` 属性一样的值（比如350px），则项目将占据固定空间。

## flex

`flex` 属性是 `flex-grow`,  `flex-shrink` 和 `flex-basis`的简写，默认值为 `0 1 auto`。后两个属性可选。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

 建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

## align-self *

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

![](IMGS/flex_align_self.png)

# 实际使用

在开发中，我们经常会遇到如下布局：

![](./IMGS/flex-layouts.png)

布局代码如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>flex-layouts</title>
    <style>
      .wrap {
        /* 核心代码 */
        display: flex;
        flex-flow: row wrap;
        align-content: flex-start;
      }
      .item {
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: cornflowerblue;
        color: #fff;
        font-weight: bold;
        border-radius: 6px;
        /* 核心代码 */
        flex: 0 0 calc((100% - 3 * 10px) / 4);
      }
      .item:not(:nth-child(4n)) {
        margin-right: 10px;
      }
      .item:not(:nth-last-child(-n + 4)) {
        margin-bottom: 10px;
      }
    </style>
  </head>
  <body>
    <div class="wrap">
      <section class="item">1</section>
      <section class="item">2</section>
      <section class="item">3</section>
      <section class="item">4</section>
      <section class="item">5</section>
      <section class="item">6</section>
      <section class="item">7</section>
      <section class="item">8</section>
      <section class="item">9</section>
      <section class="item">10</section>
      <section class="item">11</section>
      <section class="item">12</section>
      <section class="item">13</section>
      <section class="item">14</section>
      <section class="item">15</section>
      <section class="item">16</section>
      <section class="item">17</section>
      <section class="item">18</section>
      <section class="item">19</section>
      <section class="item">20</section>
      <section class="item">21</section>
      <section class="item">22</section>
    </div>
  </body>
</html>
```

























