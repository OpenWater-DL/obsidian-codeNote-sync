#总结笔记
**一篇搞定！**

[阮一峰css定位详解](https://www.ruanyifeng.com/blog/2019/11/css-position.html)

# 基本作用
display ”显示",控制元素身体的状态——个体自身
position“位置”，控制元素在哪里——环境

# 个体有多少种display状态？
最基本的两种：block（块元素），inline（行内元素）。
小强版；inline-block
加强版： flex

### block
**div默认是block。**
block默认就是占满一整行，所以自然是从上到下排布。
行高取决于内容。
加多少个div，页面就不断往下增加（而不是往右边增加）。
[[Web/css/202102242119 块元素 block]]
### inline
- 紧身の不便
inline不能指定高度，就像一个紧身包裹,有很多不便的地方，所以**几乎不会特别将别的指定成inline**。反而是会将原本是inline的 span之类的指定成block或inlineblock。
- 默认值是inline的：span，**img**
- inline的特征可以想象成文本，文本都是“黏住左边”的。所以想要inline元素居中，就要用文本的处理方式——对父级使用text-align:center;

### inline-block
inline-block相当于把block放到行内。
- 可以指定宽高，撑满了还能自动换行。
- 常用场景：导航一排的按钮。
- 实质上算是inline元素。比如对他使用magin: 0 auto 就不会对内生效。
[[Web/css/202102242140 inline-block行块问题]]
	
\
\

# 常见标签初始
inline：a,span,br,i,em,strong,label,q,var,cite,code

inline-block：img,input

block：p，div,p,h1...h6,ol,ul,dl,table,address,blockquote,form
	

# ----position----
## 固定组
- fixed  相对于窗口，固定定位
- absolute  绝对定位(脱离文档流)，可以指定四周的距离（基于父容器），但该元素的宽度就由自己的内容宽度来决定了。

使用了absolute的子元素，虽然会脱离正常的文档流，但是会落到紧贴自己父元素的左下方

[[22_120_748 css absolute详细辨析。]]

## 相对组
- relative：相对于自己的正常位置定位（不脱离文档流）
	例如:"left:20" 会向元素的 LEFT 位置添加 20 像素。
	
- inherit ：继承父元素：

- static 默认，没有定位，不受上下左右影响，正常随着文本流出现




	
---
# ---设定对齐的方法---
## 水平居中
### inline元素的对齐：在父级指定
[もうCSSの真ん中寄せで悩まない！横向き編](https://www.youtube.com/watch?v=v4UbH2jqbgg)
涵盖标签：span,img
使用属性：text-align:center （水平居中）
设定位置：**元素的父级。親要素に指定**
- 因为程序需要知道，对于谁水平居中。	
- 单独对p使用也会生效是因为p其实是block要素，但是对img不生效，所以好习惯还是对父级用。

### block元素的对齐：对自己指定
使用属性：margin：0 auto （ゼロ　オット）

## 垂直居中
[もうCSSの真ん中寄せで悩まない！縦向き編](https://www.youtube.com/watch?v=FjJMlqj2_Qo)
### 单行文本
- 可使用magin来设定。
### inline元素
使用属性：vertical-align：center
设定位置：**元素置自身**

### block元素
- 方法一：绝对配置法
```css
position：absolute；//or相对relative
top：50%； //相对于屏幕顶端的50%位置
transform:translateY(-50%);  
//transform的作用：
//元素自身，在Y方向上，以【自己高度】的50%的距离，移动。
//作用相当于让方形往上移，自己的腰就在自己的原点上。

```

```css
position：absolute；
top：50%；
left：50%; //如果如果想要左右也居中，加上这行。
transform:translate(-50%,-50%); 
```

-方法二：flex法(也是可横可竖)

---
# ---Flex大法---
[10分でわかるFlexbox講座](https://www.youtube.com/watch?v=PZsvFYfyWw0)
最精简的几个属性。
## 容器（flexbox）需要设定的东西
```css

.c{
display:flex;  //没有它就不能开始flex
flex-wrap:wrap;		//换行。不写的话就一直横向生长。

justify-content:center; //水平居中
justify-content:space-between;//两端对齐，间隙自动平均分。

align-items:center; // 垂直居中

}

```

## 对齐属性精细理解：
口诀：先定轴向和分布-再来交叉align它。
解释：先定轴向(direction)和分布(justify)-再来交叉align它(items)。

### flex-direction
flex的方向？
这是设定对齐的第一步，**定“主轴”**

```css
flex-direction: row | row-reverse | column | column-reverse;
```
![[src/img/Pasted image 20220114155242.png]]
`column` 柱 → 所以是竖向。

### justify-content
justify-整理版面，content-内容。
如何整理内容？比方说我有一行内容且是row方向，但是他们是左对齐，还是右对齐，或者是别的？
```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```


	![[src/img/Pasted image 20220114155643.png]]

### align-items
当我也知道他们在轴上如何分布了，就还剩下一个问题：在交叉轴方向上放在哪里？
比如横向的分布弄清楚了，纵向是顶对齐还是底对齐？or中间对齐?
```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

![[src/img/Pasted image 20220114160607.png]]


### 间距 gap
#### row-gap
用来设置行元素之间的间隙(gutter) 大小。
#### column-gap
用来设置元素列之间的间隔 (gutter) 大小。
#### gap
用来设置网格行与列之间的间隙（gutters），该属性是 row-gap and column-gap 的简写形式。
```css
div{
display:flex;
flex-wrap: wrap;
gap: 5rem ;
}
```


## 特别需求：按占比分配空间
方法一：比如说下面这样，就是左右分别再写个容器包住div，并分别指定width:50%
![[src/img/Pasted image 20211213223726.png]]
方法二：对子元素设置权重 
```	
.item1{
	 flex:1;
	}
	.item2{
	 flex:2;
	}
```

## 父元素display:[flex](https://so.csdn.net/so/search?q=flex&spm=1001.2101.3001.7020)布局下的子元素宽度无效


# ---图片大小调整---
[[Web/css/21_1213_1049  css总结笔记 关于width,图片大小]]


---

# 相关资料
[[Web/css/202104081412 CSS display布局基本]]

[# How to Create Responsive Image Gallery with Lightbox using Html and Bootstrap4 | Lightbox Gallery](https://www.youtube.com/watch?v=h5v2LVFmbMY)

【flex】
[文本，flex详解](https://www.cnblogs.com/hellocd/p/10443237.html)
[文本，阮一峰的讲解](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
[视频，flex B站](https://www.bilibili.com/video/BV19f4y1x75Q?from=search&seid=15447134268167610251)
[视频，doyoudo的讲解，比较干净](https://www.bilibili.com/video/BV1nW411A713?from=search&seid=16982869682438714952)

[视频，CSS 快速简明教程 ｜ 盒子模型/文档流/定位/布局/响应式设计](https://www.youtube.com/watch?v=-yqlP0HWP94)
这个教程对于flex的用法演示得非常清楚。
图片响应在26:56