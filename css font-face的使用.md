自定义字体等等会使用到fontface。
**fontface本质上就是个变量。**

# 用法
最终去处：
```css

p{
font-family:'myfont';
}


@font-face{
font-family:'myfont';//这里定义名字
src:url()format(),local(); //这里定义使用什么字体文件。
}

```

# font-family
加载是按顺序从左往右加载字体文件。所以要把英文字体放在前面，中文放在后面，这样英文字体才能有效果（不然中文字体里因为有英文，所以就不会给真正的英文字体机会使用）。



