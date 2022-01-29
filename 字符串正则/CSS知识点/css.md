## 1. 盒模型 Box Model
- 所有 html 元素都可以看作一个盒模型
- 盒模型的构成, 4部分
    - margin
    - border
    - padding
    - content
- padding 内边距
    - 内容和边框之间
    - 默认值为 0 不能为负数
- border 边框
    - 围绕元素内容和内边距的一条线
    - border-style 设定样式 dotted dashed solid double groove ridge inset outset
    - border-width 边框宽度
        - 数字
        - thin medium thick
    - border-color: 边框颜色
- margin 外边距
    - margin 值为负数
        - 元素自身无宽度
            - margin-left, margin-right: 变化自身元素宽度, 添加量为数值绝对值
        - 元素自身有宽度
            - 产生位移

        - 上下方向发生位移


    - 两个 div 同时设定 margin 会出现叠加的情况, 间隔取决于最大的那个外边距. 叠加的特性(只适用于块级元素)
    - 处于同一个 BFC 模型的两个相邻的块级元素会发生 margin 叠加的现象
- display:
    - 内联元素相邻中间会存在间隙(大概与是由于代码中的空格换行导致)
    - 小技巧, 设定 body 的字体大小为 0 

## 2. BFC( Block Formatting Contexts )
    #### 常见三种定位方案
    - 普通流
    按照先后位置至上而下布局, 行内元素水平排列, 沾满后换行. 块级元素则会被渲染为完整的新行. 除非另外指定, 否则所有元素默认都是普通流.

    - 浮动
    元素首先按照普通流位置出现, 然后根据浮动方向尽可能向左或者向右偏离, 其效果与印刷排版中的文本环绕相似

    - 绝对定位
    绝对定位布局中, 元素会整体脱离普通流, 因此绝对定位元素不会对其兄弟元素进行影响, 元素具体的位置由绝对定位的坐标决定.

    > Formatting context(格式化上下文) 指的是页面中的一块渲染区域, 决定其子元素如何定位以及相互作用

    BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的普通流。
    具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性

    - 只要元素满足下面任一条件即可触发 BFC 特性：

        - body 根元素
        - 浮动元素：float 除 none 以外的值
        - 绝对定位元素：position (absolute、fixed)
        - display 为 inline-block、table-cells、flex
        - overflow 除了 visible 以外的值 (hidden、auto、scroll)
        - 更多详见 (https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

    - 特性(BFC特性.html):
        - 同一个 BFC 下外边距会发生折叠
        - BFC 清除浮动
        - BFC 可以阻止元素被浮动元素覆盖, 有点类似inline, inline-block 的区别


## 3. 浮动 (最初是为了实现文字环绕的效果)
- 元素首先按照普通流的位置出现，然后根据浮动的方向尽可能的向左边或右边偏移,一直平移直到碰到了所处的容器的边框，或者碰到另外一个浮动的元素。(说白话就是仅对 float 后的元素起作用)
- 设为浮动的元素默认为块级元素, 浮动父元素塌陷
- claer 属性: 禁止元素浮动(防止因元素浮动造成的内容塌陷)
    - none 不进行控制
    - left 左侧不允许浮动
    - right 右侧不允许浮动
    - both 都不允许浮动
    - 清除浮动防止塌陷必须在父元素中最后加一个块级元素,并设定 clear
- 使用 overflow 防止元素浮动塌陷
    - 在父元素上使用 overflow: hidden
- 使用 clearfix 清除浮动
    - 使用伪元素 :after
    - 对伪元素使用 clear: both
    - 必须三大件 content, display, clear
    - 可选 font-size height visibility
- 如何实现三列布局
    - 双飞翼布局
        - 使用 float 让左中右三列浮动
        - 使用负 margin 属性让左右与中间列处在同一水平线
        - 中间列中新建 div, 左右 margin 为左右列宽度
        - 最后清除浮动
        - 优点
            - 中间内容优先加载
            - 使用浮动布局
            - 巧妙利用负 margin 让三列保持水平
            - 兼容性好



## 4. 选择器

- 通配符选择器 (* 表示, 对所有元素生效, 设定公共样式) 
- 元素/标签选择器 
- id 选择器 / 类选择器 
- 属性选择器 E[属性] {}
    - attribute
    - attribute = value 
    - attribute ~= value 包含指定值的元素,空格分隔
    - attribute |= value 用于选取指定开头属性的元素, “-” 分隔
- 伪类选择器
- 后代选择器 格式:父元素 子元素
- 子代元素选择器 格式:父元素>子元素 后代选择器选择的是所有子元素, 子代选择器选择的是第一级后代
- 兄弟选择器 格式:当前元素+兄弟元素 相邻元素一定是同级元素
- 选择器权重
    - 通配符选择器 0
    - 元素/标签选择器 1
    - 类/伪类/属性选择器 10
    - id 选择器 100
    - 内联样式权重 1000
    - 特殊处理 !important

## 5. position 属性包含
- static: 初始属性
- relative: 在当前文档流位置进行 4 向调整
- absolute: 绝对定位, 以上一个(relative || absolute) 进行定位调整
- fixed: 根据屏幕位置进行定位, 始终保持相同位置
- sticky: 当发生滚动操作时, 元素位于 viewport 的位置

## 6. 修饰符
- .stop
    阻止冒泡,对于嵌套的两级,如果子父级元素都存在click事件,点击子级元素会触发父级元素的事件;如果子级元素设置@click.stop的话就不会触发父级的click事件

```html
    <!-- 阻止单击事件继续传播 -->
    <a v-on:click.stop="doThis"></a>
```   

- .prevent
    阻止默认行为,对于如<a href="www.baidu.com" @click.prevent="linkMethod">百度</a>自带事件的,添加prevent事件后,href跳转路径将不会触发
```html
    <!-- 阻止默认行为 -->
    <form v-on:submit.prevent="onSubmit"></form>
```   

- .capture
    对于冒泡事件,且存在多个冒泡事件时,存在该修饰符的会优先执行,如果有多个,则从外到内执行
```html
    <!-- 阻止单击事件继续传播 -->
    <a v-on:click.stop="doThis"></a>
```   

- .self
    仅绑定元素自身触发,防止事件冒泡,对于嵌套的两级,如果子父级元素都存在click事件,点击子级元素会触发父级元素的事件;如果父级元素设置@click.self的话就不会被子级元素的click事件影响

- .once
    事件只触发一次(常用表单提交)
```html
    <!-- 点击事件将只会触发一次 -->
    <a v-on:click.once="doThis"></a>
```   

- .passive
    滚动事件的默认行为 (即滚动行为) 将会立即触发,不能和.prevent 一起使用,浏览器内核线程在每个事件执行时查询 prevent,造成卡顿,使用 passive 将会跳过内核线程查询,进而提升流畅度
```html
    <!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
    <!-- 而不会等待 `onScroll` 完成  -->
    <!-- 这其中包含 `event.preventDefault()` 的情况 -->
    <div v-on:scroll.passive="onScroll">...</div>
```   

- .native
    将vue组件转换为一个普通的HTML标签,如果该修饰符用在普通html标签上是不起任何作用的

## 重绘 (reflow), 重排 (repaint)
![HTML 渲染流程](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/3/6/170af501e710ce67~tplv-t2oaga2asx-watermark.awebp)

- 重绘：某些元素的外观被改变，例如：元素的填充颜色

- 重排：重新生成布局，重新排列元素。

> 重绘不一定导致重排, 但是重排一定导致重绘

### 减少重排次数
1. 样式集中改变
```javascript
// bad
var left = 10;
var top = 10;
el.style.left = left + "px";
el.style.top = top + "px";

// 当top和left的值是动态计算而成时...
// better 
el.style.cssText += "; left: " + left + "px; top: " + top + "px;";

// better
el.className += " className";
```

2. 分离读写操作
- 获取元素的几何属性时, 会导致重排, 所以应该尽可能保证读写分离

```javascript
// bad 强制刷新 触发四次重排+重绘
div.style.left = div.offsetLeft + 1 + 'px';
div.style.top = div.offsetTop + 1 + 'px';
div.style.right = div.offsetRight + 1 + 'px';
div.style.bottom = div.offsetBottom + 1 + 'px';


// good 缓存布局信息 相当于读写分离 触发一次重排+重绘
var curLeft = div.offsetLeft;
var curTop = div.offsetTop;
var curRight = div.offsetRight;
var curBottom = div.offsetBottom;

div.style.left = curLeft + 1 + 'px';
div.style.top = curTop + 1 + 'px';
div.style.right = curRight + 1 + 'px';
div.style.bottom = curBottom + 1 + 'px';
```

3. 将 DOM 离线
- 使用 display: none. 一旦给元素设置 display: none (触发一次重排重绘), 元素就不再存在渲染树中, 之后对其操作就不会出发重排重绘. 完成后再次使用 display 显示(再次出发重排重绘). 这样即使是大量修改也是触发两次重排重绘. 另外 visibility: hidden 只对重绘有影响, 不影响重排

- 通过 documentFragment 创建一个 dom 碎片, 在上面批量操作 dom, 操作完成后再添加到文档中, 这样只出发一次重排.

- 复制节点, 在副本上工作, 最后替换

4. 使用绝对定位会使的该元素单独成为渲染树中 body 的一个子元素，重排开销比较小，不会对其它节点造成太多影响。当你在这些节点上放置这个元素时，一些其它在这个区域内的节点可能需要重绘，但是不需要重排。

5. 优化动画
可以把动画效果应用到 position属性为 absolute 或 fixed 的元素上，这样对其他元素影响较小。
动画效果还应牺牲一些平滑，来换取速度，这中间的度自己衡量：
比如实现一个动画，以1个像素为单位移动这样最平滑，但是Layout就会过于频繁，大量消耗CPU资源，如果以3个像素为单位移动则会好很多


启用GPU加速
GPU 硬件加速是指应用 GPU 的图形性能对浏览器中的一些图形操作交给 GPU 来完成，因为 GPU 是专门为处理图形而设计，所以它在速度和能耗上更有效率。
GPU 加速通常包括以下几个部分：Canvas2D，布局合成, CSS3转换（transitions），CSS3 3D变换（transforms），WebGL和视频(video)。

```
  /*
  * 根据上面的结论
  * 将 2d transform 换成 3d
  * 就可以强制开启 GPU 加速
  * 提高动画性能
  */
  div {
    transform: translate3d(10px, 10px, 0);
  }

```