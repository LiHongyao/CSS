# 一、简介

CSS（Cascading Style Sheets，层叠样式表），用于设置HTML标签的样式，它的基本结构如下：

![](IMGS/css.jpg)

# 二、引入方式

使用样式表主要有4种方式：**行内样式**、**内嵌样式**、**外链样式**、**导入式**。

## 1、行内样式 *

是将 `style` 作为一个标签的属性，然后通过它的值来设置样式。写法如下：

```html
<div style="width: 300px; height: 300px; background-color: red;"></div>
```

## 2、内嵌样式 *

是将 `style` 作为一个标签，然后在标签内通过样式选择符设置样式。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<!-- 内嵌样式 -->
	<style type="text/css">
		div { width:  300px; height: 300px; background-color: red; }
	</style>
</head>
<body>
	<div></div>
</body>
</html>
```

## 3、外链样式 *

将样式单独放置在一个`.css` 文件，然后在页面中通过 `<link>` 标签的 `href` 属性引入该样式文件。这样做的目的为了抽离CSS，便于维护和管理。

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<!-- 外链样式 -->
	<link rel="stylesheet" href="./css/index.css">
</head>
<body>
	<div></div>
</body>
</html>
```

```css
/*index.css*/

@charset "UTF-8";

div {
	width:  300px;
	height: 300px;
	background-color: red;
}
```

> 注意：css文件第一行代码需指定字符编码格式，防止出现乱码：`@charset "utf-8";`

## 4、导入式

该方法是在 `<style>` 标签的内容里通过 `@import` 方法来导入外部CSS文件，这点和通过\<link>标签导入外部样式是一样的，但其它方面却有很大不同。这种方式的写法是：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style type="text/css">
		@import("./css/index.css");
	</style>
</head>
<body>
	<div></div>
</body>
</html>
```

> 拓展：**外链与导入同是外部引用的方式，但他们有哪些区别？**

1. 编码位置不同：\<link> 是放在 \<head> 标签中通过 href 属性引入样式的，而@import 是在样式文件中引入其他CSS文件的。

2. 引入类型不同：@import 只能引入CSS文件，\<link> 可以引用各种类型的外部资源。
3. 主要区别在于加载顺序和浏览器对它们的处理方式。
   - 使用\<link>标签引入的样式表会在网页开始加载时同时加载并解析.
   - 使用@import引入的样式表则要等到当前文档被完全加载之后才会被下载和解析。

> 结论：推荐使用 \<link> 引入外部样式。
>

# 三、通过< link >标签引用CSS文件

在实际的项目开发过程中，我们一般都是将CSS单独存放在一个文件夹中，然后在HTML页面中通过如下形式进行引用。

```html
<link rel="stylesheet" href="样式表路径+名称.css">
```

引用后CSS文件仍然是独立的，不会受到包括HTML和JavaScript任何方法和函数的影响，如果CSS文件中涉及到文件路径的相对位置，那么也是以CSS文件所在的文件路径位置为准，而非引用它的HTML文件的文件路径位置。

相对于“行内样式”和“内嵌样式”而言，“外链样式”即通过\<link>标签引用CSS样式有以下好处：

1. 简化了DOM结构，实现了内容和表现的分离，使HTML和CSS文件结构更加清晰，利于维护
2. 大大减少了CSS代码的编写量。项目越大，这一点体验得越明显
3. \<link>可以和其它\<link>、JS文件以及\<body>内的内容进行多线程加载，使得加载速度更快
4. 利于项目整体风格的调整，维护起来也更加便捷。单文件修改，全网站（应用）生效
5. 浏览器会将CSS文件进行缓存，进一步地减少了加载所需时间
6. 可以根据需要利用JavaScript或Media动态的组合所需的CSS文件
7. 对搜索引擎友好，有利于SEO

# 四、引用优先级

以上四种样式的引用方式，按照优先级从高到低排列分别是：

```
行内样式 > 内嵌样式 > 外链样式 > 导入样式
```

为了便于记忆，我们可以这样理解：越是离我们要设置样式标签元素近的CSS样式，那优先级越高，反之，优先级越低。当然在这里需要明白的是，CSS样式的引用优先级没有优先级越高越好或者优先级越低越好的说法，我们是要利用样式优先级这一特性，在是我们写更少的CSS代码同时，又使我们的Web页面表现力更加丰富。

另外，通过 `!important` 可以提升样式的优先级，如下所示：

```css
.title {
  	color: blue !important;
}
```

# 五、CSS 常用单位

- `px`：固定单位，相对于 **显示器屏幕分辨率** 而言，值是固定的，指定多少就是多少。
- `em`：相对单位，相对于 **父元素** 字体大小，em单位的值可以被子元素继承。
  - em = 像素值 / 父元素字体大小
- `rem`：相对单位，相对于 **根元素** 字体大小，rem单位的值不会被继承。
  - 根元素字体大小 = 设备宽度/设计稿宽度 * 100
  - rem = 设计稿值 / 100











