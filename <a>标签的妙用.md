# <a>
HTML <a> 元素（或称锚元素）可以通过它的 href 属性创建通向其他网页、文件、同一页面内的位置、电子邮件地址或任何其他 URL 的超链接。<a> 中的内容应该应该指明链接的意图。如果存在 href 属性，当 <a> 元素聚焦时按下回车键就会激活它。

啥也不写的情况下, 会默认刷新页面, 如果不希望页面刷新, 只能通过 href = Javascript: 伪协议处理

## 补充内容 void
void 作为一个标识符, 作用是执行后续表达式, 但是永远返回 undefined. 由于 undefined 在 javascript 中不是保留字. 所以我们没法保证每一次的使用都是安全的. 那么使用 void 0 作为获取 undefined 的方式是一个不错的选择.

## 属性
### download

### href

链接到外部地址 

```html
<!-- anchor linking to external file -->
<a href="http://www.mozilla.com/">
    External Link
</a>
```

链接到内部
```html
<!-- links to element on this page with id="attr-href" -->
<a href="#属性">
    Description of Same-Page Links
</a>

<!-- 返回顶部 -->
<a href="#">
    Description of Same-Page Links
</a>
```

执行 JS 伪协议
```html
<!-- 无操作, 页面也不会发生跳转 -->
<a href="javascript:void(0)">
    External Link
</a>

<!-- 或者这样, 效果一致 -->
<a href="javascript:;">
    External Link
</a>
```



### target

### ping
