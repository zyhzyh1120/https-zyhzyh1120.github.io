---
title: flex布局
date: 2022-11-22 19:38:22
tags: flex
categories: Flex
excerpt: Flex备忘
---

# Flex 布局

父元素设置为 Flex 后 , 子元素根据内容撑开, 如果宽度不够, 没有内容的会被挤压

#### 应用场景: 横向滚动

[情况分析:]()

子元素有宽度 , 但是子元素数量多, 并且子元素内的元素宽度小于自己宽度, 滚动效果出现, 子元素中没有内容的剩余空间被挤压, 没有达到预期效果

[解决方案:]() 在子元素中继续添加元素, 设置宽度跟上一级相同, 撑开子元素内的内容 , 解决!!!

### 1 flex-direction 属性(主轴)

- row（默认值）：主轴为水平方向，起点在左端。
  row-reverse：主轴为水平方向，起点在右端。
  column：主轴为垂直方向，起点在上沿。
  column-reverse：主轴为垂直方向，起点在下沿。

### 2 flex-wrap 属性(子)

（1）nowrap（默认）：不换行。

（2）wrap：换行，第一行在上方。

（3）wrap-reverse：换行，第一行在下方。

### 3 flex-flow

flex-flow 属性是 flex-direction 属性和 flex-wrap 属性的简写形式 。

默认值为 row nowrap。

### 4 justify-content 属性(主轴)

justify-content 属性定义了项目在主轴上的对齐方式。

- flex-start（默认值）：左对齐

- flex-end：右对齐

- center： 居中

- space-between：两端对齐，项目之间的间隔都相等。

- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### 5 align-items 属性

align-items 属性定义项目在交叉轴上如何对齐。

- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为 auto，将占满整个容器的高度.

### 6 align-content 属性

align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用

- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。

### 7 flex-grow 属性

如果所有项目的 flex-grow 属性都为 1，则它们将等分剩余空间（如果有的话）。

如果一个项目的 flex-grow 属性为 2，其他项目都为 1，则前者占据的剩余空间将比其他项多一倍。

![比例分布](F:\资料文件夹\uni-app\typora\images\比例分布.png)

### 父项

1- 设置主轴子项的对齐方式: **justify-content**
flex-start 左对齐
flex-end 右对齐
center 中间对齐
space-between 先两边再平分空间
space-around 平分空间

2- 设置侧轴子项的对齐方式: **align-self**
flex-start 上对齐
flex-end 下对齐
center 居中

3- 设置子项占父项的剩余宽度的份数
flex : 1
flex: 2

4- 设置子项的排列顺序  
 **order**
默认值 为 0
值越小越靠前

5- 换行:
flex-wrap: wrap
默认不换行: nowrap

### 子项

1- 设置侧轴的对齐方式( 设置单行 ) : align-items
flex-start 上对齐
flex-end 下对齐
center 中间

2- 设置侧轴的对齐方式( 设置多行 ) : align-content
flex-start 左对齐
flex-end 右对齐
center 中间
space-between 先两边 ,再平分空间
