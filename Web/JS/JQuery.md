2021-01-07
#### 开始使用JQ
	引用的方法
```js
<script src="scripts/jquery.min.js"></script>
<script>

$(document).ready(function(){
    
});

或者

$(function(){
    
});


</script>

```


---

2021-01-09  -   23:25
#### 类名，ID名的引用法
	#JQuery语法
```
$(.class)
$(#ID)

$JQueryObject = $(.class) //可以创建jQuery变量来表示。

```


---


2021-01-07
#### 消失隐藏
	\#checklist是引用ID，链式使用就是用 . 相连
```js
$("#checklist").hide(300).show(1000);

$("#checklist").slideUp(1000).delay(1000).slideDown(1000);//上下滑动消失显示

$("#checklist").fadeToggle(1000).fadeToggle(1000);//自动进行显示隐藏的切换

$("#checklist").slideToggle(1000).slideToggle(1000);

```


---

2021-01-07     12:02
#### 在JQuery中修改css
#JQuery语法 
```js
$("#test1").css({
color:'red',
fontWeight:'bold'
opacity:'0.5'

});
})
```

---


2021-01-07   12:25
#### 注意ID加在哪
	注意自己加ID的是哪个标签，如果原本是\<li ID=’btn1‘>包住了\<button>,那么被JS改动后，里面的\<button>都会被改掉成普通的文本内容。
```
$(function() {

$('#btn1').html('内容改成我');

})
```
![[ID加在哪里 20210107122923.png]]


---

2021-01-09  -   23:22
#### 事件监听
	.on('事件名', function)
```

$slider.on('mouseenter',stopSlider).on('mouseleave',startSlider);

```
[[JS基础#监听事件]]


# 动画效果要点
众所周知，动画需要
A→A'的变化。
而事前写好的css，就是A。
在jQuery设置的animation，就是一个目标效果 A'。

🌰  ：**比如说按了按钮后，p被显示出来。**
要做
- 把p的透明度改成0.
- 把p隐藏。display:none;
- 通过js，先show(),再animate()。

```html

<button id="btn">click me</button>

<p sytle='display:none;' > 我就会用1秒完成显示。 </p>

```


```js


$('#btn').click( function(){

	$('p').show().animate({
	opasity:'1'
	},1000); //1000指动画播放总时长，也就是决定了速度。


});



```

jquery也支持变量数值。

```js


$('#btn').click( function(){

	$('p').show().animate({
	width:'+=200px'
	},1000); //1000指动画播放总时长，也就是决定了速度。


});



```

# 改变浏览器Tab的title
```js
$('title').text('李四饺SIJIAO')
```
