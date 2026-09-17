---
title: （auto-fit，auto-fill）两行代码就能适应任何屏幕？
published: 2026-09-16
image: ./z1.avif
tags: [auto-fit, auto-fill]
category: 技术笔记
draft: false
---

### 1. `auto-fill`
🧱 **尽可能多地填充列，即使没有内容也会“占位”**

+ 会自动创建尽可能多的列轨道（包括空轨道），让网格尽量填满容器。
+ 适合需要“列对齐”或“固定网格数”的场景。

### 2. `auto-fit`
🧱 **自动适应内容，能合并多余空列，不占位**

+ 会自动“折叠”没有内容的轨道，让现有的内容尽量拉伸占满空间。
+ 适合希望内容自适应填满整行的场景。



下面详细解释这行代码的意思：

```css
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

### 1. `grid-template-columns`
+ 作用：定义**网格容器**里有多少列，以及每列的宽度。

### 2. `repeat(auto-fit, ...)`
+ `repeat` 是个**重复函数**，表示后面的模式会被重复多次。
+ `auto-fit` 是一个特殊值，意思是：**自动根据容器宽度，能放下几个就放几个**，每列都用后面的规则。 
    - 容器宽度足够时，能多放就多放，放不下就自动换行。

### 3. `minmax(200px, 1fr)`
+ `minmax` 也是一个函数，意思是：**每列最小200px，最大可以占1fr（剩余空间的平分）**
+ 具体来说： 
    - 当屏幕宽度很窄时，每列**最小宽度是200px**，再窄就会换行。
    - 当屏幕宽度变宽，卡片会自动拉伸，每列**最大可以占据剩余空间的等分**（`1fr`），让内容填满整行。

### 4. 综合起来
+ 这行代码的意思就是： 
    - 网格会自动生成多列，每列最小200px，最大可以平分一行的剩余空间。
    - 屏幕宽了就多显示几列，屏幕窄了就少显示几列，自动换行，自适应各种屏幕！
    - **不需要媒体查询**，布局就能灵活响应。

#### 总结一句话：
`grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));`  
让你的网格卡片**最小200px，最大自动填满一行**，自动适应任何屏幕，布局永远美观！



### 👀直观对比
假设容器宽度能容纳 10 个 200px 的卡片，但你只放了 5 个卡片：

+ `<font style="color:rgb(255, 80, 44);background-color:rgb(255, 245, 245);">auto-fill</font>` 会保留 10 列宽度，5 个卡片在前五列，后面五列是“空轨道”。
+ `<font style="color:rgb(255, 80, 44);background-color:rgb(255, 245, 245);">auto-fit</font>` 会折叠掉后面五列，让这 5 个卡片拉伸填满整行。

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2025/webp/35048440/1754642211669-f6d13861-5e7b-41ce-9df9-7d60b87557e1.webp)



#### 👇 Demo 代码：
```html

<h2>auto-fill</h2>
<div class="grid-fill">
  <div>item1</div>
  <div>item2</div>
  <div>item3</div>
  <div>item4</div>
  <div>item5</div>
</div>

<h2>auto-fit</h2>
<div class="grid-fit">
  <div>item1</div>
  <div>item2</div>
  <div>item3</div>
  <div>item4</div>
  <div>item5</div>
</div>
```

```css
.grid-fill {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 40px;
}
.grid-fit {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
}
.grid-fill div {
  background: #08f700;
}
.grid-fit div {
  background: #f7b500;
}
.grid-fill div,
.grid-fit div {
  padding: 24px;
  font-size: 18px;
  border-radius: 8px;
  text-align: center;
}
```



## 🎯 什么时候用 auto-fill，什么时候用 auto-fit？
+ **希望每行“有多少内容就撑多宽”，用** `auto-fit`  
  适合卡片式布局、相册、响应式按钮等。 
+ **希望“固定列数/有占位”，用** `auto-fill`  
  比如表格、日历，或者你希望网格始终对齐，即使内容不满。

  
原文章：[https://juejin.cn/post/7497895954101403688](https://juejin.cn/post/7497895954101403688)




**完结！**


