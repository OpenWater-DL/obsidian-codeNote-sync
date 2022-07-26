[SASSの超便利な使い方](https://www.youtube.com/watch?v=Dxpl3IKLWaQ)

@charset "UTF-8"


# 1.sass模块的引用方法
## 🦌模块引用@use
https://blog.csdn.net/github_36487770/article/details/103346303


 @use 拥有命名空间，这意味着，源文件的变量不再能直接使用，而是需要加入命名空间（前缀）
 
```scss
【写法1：啥也不写】
@use '../base/colors';
body{ 
	font-size: colors.$red; //要写 colors.
}

【写法2: 假装全局】
@use '../base/colors' as *
body{ 
	font-size: $red;
}

【写法3: 给个昵称】
@use '../base/colors' as c
body{ 
	font-size: c.$red;
}
```
这样做的好处是，你不必把整个文件都写入到最终的styles.css里。对于提取部分颜色很实用。

### 略缩写法
但每次都要写colors.很麻烦，所以可以像python那样用一个代号。
写成 `*` 号就表示不用写前缀。
![[src/img/Pasted image 20220507220217.png]]


### 引用路径
@useで呼び出す時は、style.scssからの相対パスとなります。


### `@use`与`@import`的区别

`@use`和`@import`的区别在于：

1.  不管使用了多少次样式表，@use都只会引入和执行一次。
2.  与全局使用相反，@use是有命名空间的，而且只在当前样式表中生效。
3.  以`—`或者`_`开头的命名空间被认为是私有的，不会被引入其他样式表。
例如
```scss
/* buttons.scss */
$_height: 20px;

/* tryuse.scss */
@use 'buttons';

.my-buttoon {
  background-color: buttons.$color;
  height: buttons.$_height;  <<这里就会报错
}

```
4. 如果一个样式表A包括@extend，那么该扩展的作用域仅包括它本身和被它引入的上游模块中的样式规则，而不是引入了样式表A的下游模块。

### 相关教程资料

[Stop using @import with Sass | @use and @forward explained](https://www.youtube.com/watch?v=CR-a8upNjJ0&t=0s)

## 🦌中转站@forward
![[src/img/Pasted image 20220515223949.png]]
@forward 用来打包转发很多文件，all in one 。
且无重复引用的忧虑。

做法是先建立一个_index.scss，在此写入
```scss
@forward '../abstracts/colors';//路径
@forward '../abstracts/fonts';

```

然后在想要用文件里，例如_cards.scss里使用
```scss
@use '../abstracts'

```


### @forward要注意的点
forward只起到转发作用，罗列出来的文件互相之间不会引用。
例如像这样
```scss
// _index.scss

@forward 'breakpoint';
@forward 'mixin';

```
`_mixin.scss`里有使用到breakpoint里的变量，但是这样写，并不能让mixin用到它。实际上需要到mixin里再去声明一次使用。
```scss
// _mixin.scss
@use 'breakpoint'
...
```



## 文件的全部引用@import（⚠️将被弃用）
- @import 普通地引用文件是用
`@import "_header";`
这个相当于复制粘贴。有一些被覆盖的风险，官方已经不推荐使用并将在未来逐渐启用。

# 2. @extend
相当于继承。

# 3.变量 
$color = ..
$top_margin = ...

使用@use时，要注意命名空间（也就是要不要加前缀）。
例如
```scss
@use 'fonts' as f;

div{
font-size:$f.text-lg;
}

```

# 4.mixin 函数
变量代表一个值，而函数可以起到function的作用。
也可以直接充当某些代码片段的模板。
详情看这篇[[22_122_1013 sass的响应式@media与@mixin @content]]

![[src/img/Pasted image 20220515232644.png]]

这个女生讲得比kevin powell明了。
[Sass入門講座 #03：SassのMixin（ミックスイン）を使ってみよう](https://www.youtube.com/watch?v=24OE5as6cJs)