---
title: CSS基础
top_img: https://picsum.photos/seed/picsum/1920/942
cover: https://picsum.photos/seed/picsum/470/315
date: 2023-05-19 21:02:50
tags: CSS
categories: 前端
toc_number:
updated:
keywords:
description:
sticky:
aplayer:
---

## 01-CSS初体验

层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 **样式表** 语言，用来**描述 HTML 文档的呈现**（**美化内容**）。

书写位置：**title 标签下方添加 style 双标签，style 标签里面书写 CSS 代码**。

```html
<title>CSS 初体验</title>
<style>
  /* 选择器 { } */
  p {
    /* CSS 属性 */
    color: red;
  }
</style>

<p>体验 CSS</p>
```

> 属性名和属性值成对出现 → 键值对。 

## 02-CSS引入方式

* **内部**样式表：
  * CSS 代码写在 style 标签里面
* **外部**样式表：
  * CSS 代码写在单独的 CSS 文件中（**.css**）
  * 在 HTML 使用 link 标签引入

```html
<link rel="stylesheet" href="./my.css">
```

* **行内**样式：
  * CSS 写在标签的 style 属性值里

```html
<div style="color: red; font-size:20px;">这是 div 标签</div>
```

## 03-选择器

作用：**查找标签**，设置样式。 

### 标签选择器

标签选择器：使用**标签名**作为选择器 → 选中**同名标签设置相同的样式**。

例如：

```html
<style>
  p {
    color: red;
  }
</style>

```

> 标签选择器**无法差异化**同名标签的显示效果。

### 类选择器

作用：查找标签，**差异化**设置标签的显示效果。

步骤：

* 定义类选择器 → **.类名**
* 使用类选择器 → 标签添加 **class="类名"**

```html
<style>
  /* 定义类选择器 */
  .red {
    color: red;
  }
</style>

<!-- 使用类选择器 -->
<div class="red">这是 div 标签</div>
<div class="red size">div 标签</div>
```

注意：

* 类名**自定义**，不要用纯数字或中文，尽量用英文命名
* 一个类选择器**可以供多个标签使用**
* **一个标签可以使用多个类名**，类名之间用**空格**隔开

> 开发习惯：类名见名知意，多个单词可以用 - 连接，例如：news-hd。

### id选择器

作用：查找标签，差异化设置标签的显示效果。

场景：id 选择器一般**配合 JavaScript** 使用，很少用来设置 CSS 样式

步骤：

* 定义 id 选择器 → #id名
* 使用 id 选择器 → 标签添加 id= "id名"

```html
<style>
  /* 定义 id 选择器 */
  #red {
    color: red;
  }
</style>

<!-- 使用 id 选择器 -->
<div id="red">这是 div 标签</div>
```

> 规则：同一个 id 选择器在一个页面只能使用一次。
>
> 少用id选择器设置样式，多用类选择器

### 通配符选择器

作用：查找页面**所有**标签，设置相同样式。

通配符选择器： ***，不需要调用**，浏览器自动查找页面所有标签，设置相同的样式

```css
* {
  color: red;
}
```

> 经验：通配符选择器可以用于**清除标签的默认样式**，例如：标签默认的外边距、内边距。

![1680317584651](assets/1680317584651.png)

## 04-盒子尺寸和背景色



| 属性名           | 作用   |
| ---------------- | ------ |
| width            | 宽度   |
| height           | 高度   |
| background-color | 背景色 |

## 05-文字控制属性

### 字体大小

* 属性名：**font-size**
* 属性值：文字尺寸，PC 端网页最常用的单位 **px**

```css
p {
  font-size: 30px;
}
```

> 谷歌浏览器默认字号是16px。

### 字体样式（是否倾斜） 

作用：清除文字默认的倾斜效果

属性名：**font-style**

属性值

* 正常（不倾斜）：**normal** 
* 倾斜：**italic**

### 行高

作用：设置多行文本的间距

属性名：line-height

属性值

* 数字 + px
* 数字（当前标签font-size属性值的倍数）

```css
line-height: 30px;


/* 当前标签字体大小为16px */
line-height: 2;
```

> 行高的测量方法：从一行文字的最顶端（最底端）量到下一行文字的最顶端（最底端）。 

#### 单行文字垂直居中

垂直居中技巧：**行高属性值等于盒子高度属性值**

注意：该技巧适用于单行文字垂直居中效果

```css
div {
  height: 100px;
  background-color: skyblue;

  /* 注意：只能是单行文字垂直居中 */
  line-height: 100px;
}
```

### 字体族

属性名：**font-family**

属性值：字体名

```css
font-family: 楷体;
```

> 拓展：font-family属性值可以书写多个字体名，各个字体名用逗号隔开，执行顺序是从左向右依次查找
>
> *  font-family 属性最后设置一个字体族名，网页开发建议使用无衬线字体

```css
font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
```

### font复合属性

使用场景：设置网页文字公共样式 

复合属性：属性的简写方式，**一个属性对应多个值的写法**，各个属性值之间用**空格**隔开。

**font: 是否倾斜  是否加粗  字号/行高 字体（必须按顺序书写）**

```css
div {
  font: italic 700 30px/2 楷体;
}
```

> 注意：字号和字体值必须书写，否则 font 属性不生效 。

### 文本缩进 

属性名：**text-indent**

属性值：

* 数字 + px
* **数字 + em**（推荐：**1em = 当前标签的字号大小**）

```css
p {
  text-indent: 2em;
}
```

### 文本对齐方式 

作用：控制内容水平对齐方式

属性名：**text-align**

常用属性值：

- left，左对齐，默认
- center，居中对齐
- right，右对齐

```css
text-align: center;
```

> text-align本质是控制内容的对齐方式，属性要设置给内容的父级。 

```html
<style>
  div {
    text-align: center;
  }
</style>

<div>
  <img src="./images/1.jpg" alt="">
</div>
```

### 文本修饰线 

属性名： **text-decoration** 

常用属性值：none，去掉修饰线

其他属性值：

- underline 下划线
- line-though 贯穿线（删除线）
- overline 上划线

### color 文字颜色

| 颜色表示方式 | 属性值        | 说明                                        |
| ------------ | ------------- | ------------------------------------------- |
| 颜色关键字   | 颜色英文单词  | red、orange、green……                        |
| rgb          | rgb(r,g,b)    | rgb表示红绿蓝三原色，取值0-255              |
| rgba         | rgba(r,g,b,a) | a表示透明度，取值0-1，越小越透明            |
| 十六进制表示 | #00000        | 连续两位相同可以简写，如：#00FFEE简写成#0FE |

> 只要属性值为颜色，都可以使用上述四种颜色表示方式，例如：背景色。 

## 06-复合选择器

定义：由两个或多个基础选择器，通过不同的方式组合而成。

作用：更准确、更高效的选择目标元素（标签）。

### 后代选择器

后代选择器：**选中某元素的后代元素**。

选择器写法：父选择器  子选择器 { CSS 属性}，父子选择器之间用**空格**隔开。

```html
<style>
  div span {
    color: red;
  }
</style>
<span> span 标签</span>
<div>
  <span>这是 div 的儿子 span</span >
</div>
```

### 子代选择器

子代选择器：选中某元素的子代元素（**最近的子级**）。

选择器写法：父选择器 > 子选择器 { CSS 属性}，父子选择器之间用 **>** 隔开。

```html
<style>
  div > span {
    color: red;
  }
</style>

<div>
  <span>这是 div 里面的 span</span>
  <p>
    <span>这是 div 里面的 p 里面的 span</span>
  </p>
</div>

```

### 并集选择器

并集选择器：选中**多组标签**设置**相同**的样式。

选择器写法：选择器1, 选择器2, …, 选择器N { CSS 属性}，选择器之间用 **,** 隔开。

```html
<style>
  div,
  p,
  span {
    color: red;
  }
</style>

<div> div 标签</div>
<p>p 标签</p>
<span>span 标签</span>
```

### 交集选择器 

交集选择器：选中**同时满足多个条件**的元素。

选择器写法：选择器1选择器2 { CSS 属性}，选择器之间连写，没有任何符号。 

```html
<style>
  p.box {
  color: red;
}
</style>

<p class="box">p 标签，使用了类选择器 box</p>
<p>p 标签</p>
<div class="box">div 标签，使用了类选择器 box</div>
```

> 注意：如果交集选择器中有标签选择器，标签选择器必须书写在最前面。 

### 伪类选择器 

伪类选择器：伪类表示元素**状态**，选中元素的某个状态设置样式。

鼠标悬停状态：**选择器:hover { CSS 属性 }**

```html
<style>
  a:hover {
    color: red;
  }
  .box:hover {
    color: green;
  }
</style>

<a href="#">a 标签</a>
<div class="box">div 标签</div>
```

#### 超链接伪类

| 选择器     | 作用     |
| ---------- | -------- |
| `:link`    | 访问前   |
| `:visited` | 访问后   |
| `:hover`   | 鼠标经过 |
| `:active`  | 点击     |

> 提示：如果要给超链接设置以上四个状态，需要按 LVHA 的顺序书写。 
>
> 经验：工作中，一个 a 标签选择器设置超链接的样式， hover状态特殊设置 
>
> 除了a元素，其他元素也可以设置链接伪类

```css
a {
  color: red;
}

a:hover {
  color: green;
}
```

### 结构伪类选择器

#### 基本使用

作用：根据元素的**结构关系**查找元素。 

| 选择器           | 说明              |
| ---------------- | ----------------- |
| `E:first-child`  | 查找第一个E元素   |
| `E:last-child`   | 查找最后一个E元素 |
| `E:nth-child(N)` | 查找第N个E元素    |

```css
li:first-child {
  background-color: green;
}
```

#### :nth-child(公式)

| 功能                | 公式                          |
| ------------------- | ----------------------------- |
| 偶数标签            | 2n                            |
| 奇数标签            | 2n+1,2n-1                     |
| 找到M的倍数标签     | Mn，M=5,5n就是找到5的倍数标签 |
| 找到第M个以后得标签 | n+M                           |
| 找到第M个以前的标签 | -n+M                          |

>公式中的n从0开始取值

### 伪元素选择器

作用：创建**虚拟元素**（伪元素），用来**摆放装饰性的内容**。 

| 选择器      | 说明                            |
| ----------- | ------------------------------- |
| `E::before` | 在E元素里面最前面添加一个伪元素 |
| `E::after`  | 在E元素里面最后面添加一个伪元素 |

```css
div::before {
  content: "before 伪元素";
}
div::after {
  content: "after 伪元素";
}
```

注意点：

* 必须设置 **content: ””属性**，用来 设置伪元素的内容，如果没有内容，则**引号留空**即可
* 伪元素默认是**行内**显示模式
* **权重和标签选择器相同**

