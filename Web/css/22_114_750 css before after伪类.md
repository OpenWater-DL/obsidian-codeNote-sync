
[::before官方详解](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::before)
before after伪类用于创建div，并给这个创建的div一些特征：

```html
<mydiv> 我是内容。 </mydiv>

```

```css
mydiv :: before{
conten:'我是增加在前面的内容。'
}
```

结果：
```
我是增加在前面的内容。我是内容。
```

# hover效果应用
[油管btn css动效实例教程](https://www.youtube.com/watch?v=cH0TC9gWiAg)


# 宽度继承问题
https://www.02405.com/ui/html_css/1985.html

**解决办法：**
设置side的position: relative;这样side::before会相对于side定位，宽度就会一样了。