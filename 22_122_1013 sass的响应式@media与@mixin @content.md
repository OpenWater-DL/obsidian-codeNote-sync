[官方基本用法](https://www.sass.hk/docs/)

这个女生讲得比kevin powell明了。
[Sass入門講座 #03：SassのMixin（ミックスイン）を使ってみよう](https://www.youtube.com/watch?v=24OE5as6cJs)

# 基本用法
![[src/img/Pasted image 20220515232644.png]]


sass里，媒体查询的写法和css一样，但它可以更便利的地方在于：能够嵌套写进`div{ 里面来 }`，而在真正的css文件里会被渲染到外部去。
以及可以使用sass的变量函数等进行更全局的控制。

例如
```css
div{
font-size:14px;

	@media screen and (max-width: 300px) {
	font-size:12
	}
}

```

会被编译成
```css
div{
font-size:14px;
}

@media screen and (max-width: 300px) {
	div{
	font-size:12px;
	}
}

```

# sass的函数@mixin 基本概念
[进阶用法，嵌套在函数里](https://qiita.com/shizen-shin/items/1910bd9c1c42ff3c6f32)

## sass里的function ：@mixin 
定义的语法结构和js的function一样的,不过在参数里多了个初期值指定。
如果引用的时候不指定，就自动编译成初期值。

定义用 `@mixin`
引用用 `@include`

```css
// mixinを定義
@mixin colorfont($color: yellow, $fsize: 32px) { 
						↑这里的yellow,32px就是初期值
	color: $color; 
	font-size: $fsize; 
} 

// mixinを呼び出す（呼び出し方法は３種類） 

//不指定数值。（就会用默认） 
.class { 
	@include test; 
	font-weight: bold; 
} 

//直接填数值。
.class2 { 
	@include test(blue, 18px); 
	font-weight: bold; 
} 

//变量名：数值
（我一般应该不会这么用。不过变量多的时候可以用它来避免填写顺序导致的问题）
.class3 { 
	@include test($fsize: 18px, $color: green); 
	font-weight: bold; 
}

```

编译结果：
```css
.class { color: yellow; font-size: 32px; font-weight: bold; } .class2 { color: blue; font-size: 18px; font-weight: bold; } .class3 { color: green; font-size: 18px; font-weight: bold; }

```


## mixin的自由度增强：@content
@content 的作用是，在mixin的构造里提供一个弹性位置，让你引用定义好的函数时，还能自行添加一些内容进去。
例如
```css
@mixin mycolor($color:yellow){
	color:$color;
	@content; ←然后这个位置就可以随意扩展
}

.class{
	@include mycolor{
	max-width:50%;  ←这个就是@content
	}
}

```

编译结果
```css
.class{
	color:yellow;
	max-width:50%;	←来自于@content
}


```

## 默认候补备胎：!default
如果在变量的屁股后面写!default,就会调低优先级，
仅在没有定义过这个变量的地方是使用它。

## 字符串用法#{string}
[sass-interpolation](https://sass-lang.com/documentation/interpolation)
![[src/img/Pasted image 20220122110327.png]]

## 数组键值对 map-get($map, $key)
来看一个简单的示例，假设定义了一个 $social-colors 的 map:
```css
$social-colors: (
    dribble: #ea4c89,
    facebook: #3b5998,
    github: #171515,
    google: #db4437,
    twitter: #55acee
);

假设要获取 facebook 键值对应的值 #3b5998，我们就可以使用 map-get() 函数来实现：

.btn-dribble{ color: map-get($social-colors,facebook);
}

编译出来的CSS：

.btn-dribble { color: #3b5998;
}
```

# 更灵活的响应式写法实践

### 简易版
```css
$sm:'max-width:630px';←这样以后只要改这里，所有的都可以改。
@media screen and ($sm) {
	display: block;
}
}

```


### 复杂版
如果不想写那一长串media screen and ()....那就可以试试这个思路。

用目标倒推定义结构。
目标：
```css
@media screen and (max-width: 900px){


};

```

为了让它变得有复用性，那么就需要对括号里的max-width: 900px进行预先定义,让它变成一个可以被调用的字符串` 'max-width: 900px'  `
为了方便叫出这个字符串，还需要一个名字（变量名）
所以就是  `'sm' : 'max-width: 900px'`。
下一步，就是创建一个数组装起他们。

```scss
//$sizes: xl, lg, md, sm, xs;   这里只是为了好懂？不写感觉也不影响功能

$breakpoint-array: ( 
'xs': 'screen and (min-width: 321px)', 
'sm': 'screen and (min-width: 376px)', 
'md': 'screen and (min-width: 501px)', 
'lg': 'screen and (min-width: 961px)',
'xl': 'screen and (min-width: 1201px)', 
) !default; 
```

```scss
//定义function
@mixin in-media($breakpoint: md) {

	@media #{ map-get($breakpoint-array, $breakpoint)} { 
		@content; ←在里面创建一个预留位给写自定义样式。
	} 

}

```

```scss

//使用function
.class { 
font-size: 12px; 
	@include in-media('sm') {  
	font-size: 18px;  ← =@content
	} 

}
```

最后编译成：
```css
.class { 
font-size: 12px; 
} 

@media screen and (min-width: 376px) {
.class { font-size: 18px; } 
}
```

