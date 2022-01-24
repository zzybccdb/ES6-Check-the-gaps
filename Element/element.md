# Element 接口


## Element.getBoundingClientRect() 

如果是标准盒子模型，元素的尺寸等于width/height + padding + border-width的总和。如果box-sizing: border-box，元素的的尺寸等于 width/height。

以视窗左上角为原点(0,0), 水平左到右, 竖直上到下 

- x: 距离原点水平距离
- y: 距离原点竖直距离
- top: 元素上边到视窗顶部距离
- bottom: 元素下边到视窗顶部距离
- left: 元素左边到视窗左侧距离
- right: 元素右边到视窗右侧距离