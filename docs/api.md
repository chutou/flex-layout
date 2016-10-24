## css-flex-layout

css-flex-layout基于12个栅格布局，与传统栅格化的使用方式类同，但提供了更直观、丰富的布局方式。

```
<div class="demo demo1">
	<div class="flex-column">
		<div class="flex-item-12">flex-item-12</div>
	</div>
	<div class="flex-column">
		<div class="flex-item-6">flex-item-6</div>
		<div class="flex-item-6">flex-item-6</div>
	</div>
	<div class="flex-column">
		<div class="flex-item-4">flex-item-4</div>
		<div class="flex-item">flex-item 自动填充宽度</div>
		<div class="flex-item-4">flex-item-4</div>
	</div>
	<div class="flex-column">
		<div class="flex-item-4">flex-item-4</div>
		<div class="flex-item-4 flex-offset-4">flex-item-4 , flex-offset-4</div>
	</div>
</div>
```
## 概述

与传统的栅格化一样，css-flex-layout基于[容器] (相当于Bootstrap的row) 和[栅格] (相当于Bootstrap的column) 来布局:

1. [容器]有两种：

   flex-column: 容器里的[栅格]以横向排列，与传统栅格化的row一样
   flex-row: 容器里的[栅格]以竖向排列，就像header、content、footer的排列一样

2. 通常，只有[栅格]可以直接放在[容器]中，而你的内容应该放在[栅格]里。但这不是必须的，直接把内容放在[容器]里也没问题。

3. 如果一个[容器]里包含的[栅格]超过12格，多出的部分将另起一行。

4. IE的话只兼容IE10+，其他主流浏览器都支持，具体可以看：[兼容性](http://caniuse.com/#search=flex)

5. Flexbox有主轴，副轴的概念，css-flex-layout已经封装好了，你不需要懂得flexbox，也无需针对不同轴使用不同的class。
   不过，如果你对Flexbox有所了解的话，用起来会更顺手，推荐阮一峰的[Flex 布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

6. 与Bootstrap等栅格化不同的是：css-flex-layout不需要container，栅格本身不自带padding。

## 优势

css-flex-layout解决了css布局的不少问题，这里所说的大多在下面的Example里可以看到:

1. 应用一个class就可以垂直居中。
2. 轻松实现多栏同高。
3. 自动计算间距，实现等宽布局，不需要再计算margin。
4. 支持自动填充剩余宽度，以往我们需要通过触发BFC来实现。
5. 支持自动填充剩余高度，比如将footer置于底部。
6. 随意调整[栅格]顺序，比如让main比sidebar提前渲染出来。
7. 丰富的对齐方式：上、下、左、右、左上、右上、左下、右下。

## 用法

### flex-middle 垂直居中 flex-center 水平居中

这两个class应用在[容器]上时，所有子flex-item都会垂直或水平居中。也可以单独应用在[栅格]上，使特定栅格居中对齐。

```
<div class="demo flex-row flex-middle flex-center" style="min-height: 180px">
	<div class="flex-item-4" style="margin-bottom: 10px">无论是多行还是单行，都可以垂直居中</div>
	<div class="flex-item-4">无论是多行还是单行，都可以垂直居中</div>
</div>
```

### flex-offset-* 向左偏移

这个class应用在[栅格]上，指定[栅格]向左偏移多少格。

```
<div class="demo flex-column">
	<div class="flex-item-4">flex-item-4</div>
</div>
<div class="demo flex-column">
	<div class="flex-item-4 flex-offset-4">flex-item-4, flex-offset-4</div>
</div>
<div class="demo flex-column">
	<div class="flex-item-4 flex-offset-4">flex-item-4, flex-offset-4</div>
</div>
```

### flex-order-* 排序 

这个class应用在[栅格]上，order越小排在越前面。

```
<div class="demo flex-column">
  <div class="flex-item-3 flex-order-4">flex-order-4</div>
  <div class="flex-item-3 flex-order-3">flex-order-3</div>
  <div class="flex-item-3 flex-order-2">flex-order-2</div>
  <div class="flex-item-3 flex-order-1">flex-order-1</div>
</div>
```

### flex-left 左对齐 flex-right 右对齐

这两个class应用在[容器]上时，所有子flex-item都会左右对其。也可以单独应用在[栅格]上。

```
<div class="demo flex-column flex-left">
  <div class="flex-item-3">左对齐</div>
  <div class="flex-item-3">左对齐</div>
  <div class="flex-item-3">左对齐</div>
</div>
<div class="demo flex-column flex-right">
  <div class="flex-item-3">右对齐</div>
  <div class="flex-item-3">右对齐</div>
  <div class="flex-item-3">右对齐</div>
</div>
<div class="demo flex-row flex-left">
  <div class="flex-item-3">左对齐</div>
  <div class="flex-item-3 flex-right">右对齐</div>
  <div class="flex-item-3">左对齐</div>
</div>
<div class="demo flex-row flex-right">
  <div class="flex-item-3">右对齐</div>
  <div class="flex-item-3 flex-left">左对齐</div>
  <div class="flex-item-3">右对齐</div>
</div>
```

### flex-top 顶部对齐 flex-bottom 底部对齐

这两个class应用在[容器]上时，所有子flex-item都会上下对其。也可以单独应用在[栅格]上。

```
<div class="demo flex-column flex-top" style="height: 80px">
  <div class="flex-item-3">顶部对齐</div>
  <div class="flex-item-3">底部对齐</div>
  <div class="flex-item-3">顶部对齐</div>
</div>
<div class="demo flex-column flex-bottom" style="height: 80px">
  <div class="flex-item-3">底部对齐</div>
  <div class="flex-item-3">顶部对齐</div>
  <div class="flex-item-3">底部对齐</div>
</div>
<div class="demo flex-row flex-top" style="height: 140px">
  <div class="flex-item-3">顶部对齐</div>
  <div class="flex-item-3">顶部对齐</div>
  <div class="flex-item-3 flex-bottom">底部对齐</div>
</div>
<div class="demo flex-row flex-bottom flex-right" style="height: 140px">
  <div class="flex-item-3 flex-top">顶部对齐</div>
  <div class="flex-item-3">底部对齐</div>
  <div class="flex-item-3">底部对齐</div>
</div>
```

### flex-between 等宽对齐

这个class应用在[容器]上，自动调整栅格间距，保持两边间距相同。

```
<div class="demo flex-column flex-between">
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
</div>
<div class="demo flex-row flex-between flex-center" style="height: 250px">
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
  <div class="flex-item-3">等宽对齐</div>
</div>
```

### flex-around 分散排列

这个class应用在[容器]上，与等宽对齐相同，但最左、最右、最上、最下的间距比[栅格]之间的间距大一倍。

```
<div class="demo flex-column flex-around">
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
</div>
<div class="demo flex-row flex-around flex-center" style="height: 300px">
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
  <div class="flex-item-3">分散排列</div>
</div>
```

### 嵌套布局

```
<div class="demo flex-column flex-center">
  <div class="flex-item-6 flex-row">
    <div class="flex-item">flex-item</div>
    <div class="flex-item">flex-item</div>
  </div>
  <div class="flex-item-4 flex-row">
    <div class="flex-item">flex-item</div>
    <div class="flex-item">flex-item</div>
    <div class="flex-item">flex-item</div>
  </div>
</div>
```

## 响应式

css-flex-layout提供了基础的响应式功能，当分辨率小于某个阈值时，你可以指定：

1.  [容器]从横向排列变为竖向排列，并且[栅格]宽度为100%

2.  隐藏指定[栅格]

3.  显示指定[栅格]

    ### flex-md

    这个class应用在[容器]上，当分辨率低于992px的时候，使[容器]变为竖向排列

    ```
    <div class="demo flex-column flex-md">
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
    </div>
    ```

    ### flex-sm

    这个class应用在[容器]上，当分辨率低于768px的时候，使[容器]变为竖向排列

    ```
    <div class="demo flex-column flex-sm">
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
    </div>
    ```

    ### flex-md-hide

    这个class应用在[容器]或[栅格]上，当分辨率低于992px的时候，隐藏[栅格]或[容器]

    ```
    <div class="demo flex-column">
      <div class="flex-item">flex-item</div>
      <div class="flex-item flex-md-hide">低于992px则隐藏该栅格</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
    </div>
    <div class="demo flex-column flex-md-hide">
      <div class="flex-item">低于992px则隐藏整个容器</div>
      <div class="flex-item">低于992px则隐藏整个容器</div>
    </div>
    ```

    ### flex-sm-hide

    这个class应用在[容器]或[栅格]上，当分辨率低于768px的时候，隐藏[栅格]或[容器]

    ```
    <div class="demo flex-column">
      <div class="flex-item">flex-item</div>
      <div class="flex-item flex-sm-hide">低于768px则隐藏该栅格</div>
      <div class="flex-item">flex-item</div>
      <div class="flex-item">flex-item</div>
    </div>
    <div class="demo flex-column flex-sm-hide">
      <div class="flex-item">低于768px则隐藏整个容器</div>
      <div class="flex-item">低于768px则隐藏整个容器</div>
    </div>
    ```

    ### flex-md-show

    这个class应用在[容器]或[栅格]上，当分辨率低于992px的时候，显示[栅格]或[容器]

    ```
    <div class="demo flex-column">
      <div class="flex-item-12">把浏览器窗口调小试试</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
    </div>
    ```

    ### flex-sm-show

    这个class应用在[容器]或[栅格]上，当分辨率低于7682px的时候，显示[栅格]或[容器]

    ```
    <div class="demo flex-column">
      <div class="flex-item-12">把浏览器窗口调小试试</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
      <div class="flex-item flex-md-show">低于992px的时候出现</div>
    </div>
    ```

## 实例

### 响应式圣杯布局

```
<div class="demo flex-row">
  <div class="flex-item">header</div>
  <div class="flex-column flex-md" style="min-height: 100px">
    <div class="flex-item-7 flex-order-2">main</div>
    <div class="flex-item flex-order-1 flex-md-hide">side-left</div>
    <div class="flex-item flex-order-3">side-right</div>
  </div>
  <div class="flex-item">footer</div>
</div>
```

### 多栏同高，flex-column默认便是。

```
<div class="demo flex-column">
  <div class="flex-item-4">sidebar</div>
  <div class="flex-item-8" style="height: 400px">main</div>
</div>
```

