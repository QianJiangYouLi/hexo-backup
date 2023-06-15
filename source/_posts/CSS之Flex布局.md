---
title: CSS之Flex布局
top_img: https://picsum.photos/seed/picsum/1920/942
cover: https://picsum.photos/seed/picsum/470/315
date: 2023-05-02 01:26:10
tags: CSS
categories: CSS 
toc_number:
updated:
keywords:
description:
sticky:
aplayer:
---

## Flex布局简介
Flex布局也称弹性布局，全称CSS Flexible Box Layout，简称Flexbox，弹性盒。是一套专门用于布局的属性，属性分为两大类：容器（弹性容器flex container）和容器`直接子元素`（弹性项flex item）。

弹性容器就是父盒子，弹性项是子盒子，不涉及到更深层的嵌套。

Flexbox可以控制flex item的如下方面：

- 大小，基于内容以及可用空间；
- 方向，水平排列还是垂直排列，正向还是反向；
- 两个轴方向上的对齐与分布；
- 顺序，所见视图顺序与源码视图顺序无关。

Flexbox在主流浏览器较新版本中都得到了广泛支持，但IE9及以前的版本不支持（IE已经不再维护）。要兼容这些不支持的浏览器可以使用一些类似FlexyBoxes代码生成器。

## 使用Flex布局

任何容器都可以指定为Flex布局，不区分块元素还是行内元素。

```css
.box {
  /*除非显示声明flex-direction属性，否则这行代码也会默认声明，flex-direction:row;*/
  display: flex; 
}
```

使用同样的元素结构简单对比没有使用flex和使用了flex布局的区别：

没有使用flex，块元素默认独占一行，呈现的视觉效果就是垂直排列。而使用了flex的则显示在同一行，视觉效果就是水平排列。

![没有使用flex](https://pic2.imgdb.cn/item/64500f290d2dde57772b48a5.png)![使用了flex](https://pic2.imgdb.cn/item/64500f280d2dde57772b483f.png)

行内元素使用flex布局也可以这样写：

```css
.box {
  flex: inline-flex;
}
```

注意：<span style="font-size:20px;color:#ffa500;font-weight:700">设置flex后，子元素的float、clear和vertical-align属性会失效</span>

## Flex轴方向

flexbox可以针对页面某一个区域控制子元素的顺序、大小、分布与对齐。

这个区域内的子元素可以沿着两个方向排列：水平排列，垂直排列。排列的方向称为`主轴`(main axis)。

与主轴垂直的方向称为`辅轴`（cross axis），区域内的子元素可以沿着辅轴发生位移或伸缩。

flex container默认主轴水平，辅轴垂直。主轴的开始位置叫做main start，结束位置叫main end。辅轴开始的位置叫cross start，结束的位置叫cross end。单个项目占据的主轴空间叫main size，占据的辅轴空间叫做cross size。

这样描述很抽象，借助下图可以非常容易理解：

![主轴与侧轴](https://pic2.imgdb.cn/item/64501ed00d2dde57773b9e2f.png)

### flex-direction主轴方向

`flex-direction`属性决定主轴的方向，有4个可选值：

- `row `（默认），从左往右，主轴水平
- row-reverse，从右往左，主轴水平
- `column`，从上往下，主轴垂直
- column-reverse，从下往上，主轴垂直

一般row和column常用，其他的不是很常用。

注意：**如果flex container没有指定大小，flex item会自动收缩，即一行中各项会收缩到各自的最小宽度，一列中的各项会收缩到各自的最小高度，以恰好容纳自身内容。**

## 对齐与空间

flexbox对flex item的排列方式有很多种。沿着主轴的排列叫`排布`（justification），沿着辅轴的排列叫`对齐`（alignment）。

由于主轴既可以水平也可以垂直，为了方便理解，只要记住**主轴方向叫排布**就行，以免混乱。

用于指定排布的属性是`justify-content`

### justify-content主轴对齐

`justify-content`属性定义了项目在主轴上的对齐方式，有如下5个值（假设主轴水平从左往右）：

- flex-start（默认），左对齐
- flex-end，右对齐
- center，居中
- space-between，两端对齐，项目之间的间隔都相等
- space-around，每个项目两侧间隔相等，项目之间的间隔是与边框距离的两倍

Flexbox不允许通过上面的五个属性值来指定单个flex item的排布方式，但可以为flex item指定值为auto的外边距。利用这点，可以实现让一项位于一侧，其他项位于另一侧的布局。本质上是因为自动外边距吃掉了其他项的排布效果，没有多余空间分配，但其他项依然可以用外边距。

![水平排布](https://pic2.imgdb.cn/item/64502d430d2dde577747a87e.png)

### align-items辅轴对齐

`align-items`属性定义项目在辅轴上如何对齐。

给flex container自身或者其中一项flex item设置一个高度，另一轴向属性默认值会发生一些变化。没错，这些flex item会自动等高。

![](https://pic2.imgdb.cn/item/645030d00d2dde577749d875.png)

实际上这是因为控制辅轴对齐的属性align-items默认值是stretch（拉伸）

align-items的取值：

- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度
- flex-start：交叉轴的起点对齐
- flex-end：交叉轴的终点对齐
- center：交叉轴的中点对齐
- baseline: 项目的第一行文字的基线对齐

![](https://pic2.imgdb.cn/item/645035560d2dde57774d6df7.png)

flex-start/flex-end/center会把子项收缩成原有大小，然后沿着辅轴进行上中下对齐。

baseline会将子项中文本基线与容器基线对齐，效果与行内块默认行为类似，当希望子项在辅轴上位置不同，但本身对齐时可以用。

### 对齐个别项

除了同时对齐所有项，还可以设置辅轴上对齐个别项。

如：第一个对齐到左上角，其他对齐到右下角

```css
.box {
    align-items: flex-end;
}

.box li:first-child {
    align-self: flex-start;
    margin-right: auto;
}
```

![](https://pic2.imgdb.cn/item/645038400d2dde57774f65bb.png)

### flexbox垂直对齐

当flex container中只有一个flex item，只要将容器设置为flex，再将需要居中的元素外边距设置为auto就行。本质是flexbox中各项的外边距会扩展填充相应方向空间。

无论容器多大或者其中的元素多大，想要水平并且垂直居中.flex-item，只需要以下css代码：

```html
<div class="flex-container">
    <div class="flex-item">
        <h2>Not so lost in space</h2>
        <p>This item sits right in the middle of its container ...</p>
    </div>
</div>

<style>
  html, body {
    height: 100%;
}

.flex-container {
    height: 100%;
    display: flex;
}

.flex-item {
    margin: auto;
}
</style>
```

![](https://pic2.imgdb.cn/item/64503ade0d2dde577750b985.png)

有多个item，可以使用对齐属性将它们都聚集到水平和垂直中心上，把排布和对齐都设置成center（当然单个项目也能这样搞，但marign：aoto代码更少）。

## 可伸缩的尺寸

flexbox支持对元素大小的灵活控制，这是实现精确布局的关键，也是flexbox中的难点。

flex意为可伸缩，体现在flex item上，主要有三个属性：`flex-basic\flex-grow\flex-shrink`。

还有一个复合属性flex，是三个属性的综合写法。

### flex-basis

flex-basis定义在**分配多余空间之前**，flex item占据的主轴空间，浏览器会根据该数据计算**主轴是否有多余的空间**。

默认取值auto，即item本身的大小（weight、height）。

```css
.item {
  flex-basis: <length> | auto;
}
```

直接设置为width或者height属性一样的值表示item占据固定空间。

### flex-grow

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

flex-grow是一个弹性系数。

```css
.item {
  flex-grow:<number>;
}
```

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。

如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### flex-shrink

`flex-shrink`属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。

如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

### flex

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

## 个别item排序

flex item有一个`order`属性，可以让设置该属性的item摆脱源代码中顺序的约束，只需要告诉浏览器这个item排第几就行。

默认情况下所有的order值都为0（按照源码顺序排列）。

数值越小，排列越靠前。

```css
.item {
  order:<integer>;
}
```

## item不同对齐方式

`align-self`属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

## 总结

flex布局两组属性的运用。

flex container属性：

>- flex-direction
>- flex-wrap
>- flex- flow (flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap)
>- justify-content
>- align-items
>- align-content
>
>

flex item属性：

>- `order`
>- `flex-grow`
>- `flex-shrink`
>- `flex-basis`
>- `flex`
>- `align-self`
