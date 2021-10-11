## 盒模型 Box Model
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

## BFC
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
    - BFC 可以阻止元素被浮动元素覆盖



## 浮动 (最初是为了实现文字环绕的效果)
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



## 选择器

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


##