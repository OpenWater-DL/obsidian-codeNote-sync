# 按钮的不同状态图片
```html
<input
type="Button" 
onMouseOver="this.className='btnOver'"
onMouseOut="this.className='btnNormal'"
onMouseDown="this.className='btnDown'"
onMouseUp="this.className='btnOver'"
class="btnNormal"
value="未点击的按钮"
onclick="this.value='被点击的按钮'" 
name="button"
>
 
 
.btnNormal { ... }
.btnOver { ... }
.btnDown { ... }

>
```


# button事件
### 基本使用，在HTML里使用
```html
<button onclick="doSomething()"> click me </button>


<script>
function doSomething(){
	document.getElementById("test").innerHtml= 'goodbye' ;

}

</script>

```

#### jquery事件监听
	.on('事件名', function)
```js

$slider.on('mouseenter',stopSlider).on('mouseleave',startSlider);

```

悬停事件，需要填写进入和离开的function。
`$(_selector_).hover(_inFunction,outFunction_)`
用例：
```js
$("p").hover(function(){ $("p").css("background-color","yellow"); },function(){ $("p").css("background-color","pink"); });
```

[jQuery设置html](https://www.runoob.com/jquery/jquery-dom-set.html)
```js
$("button").click(function(){ $("#runoob").attr("href","http://www.runoob.com/jquery"); });
```

# 无效自查
- 有没有放对顺序。要先加载jQuery库才能使用jQuery脚本。
-


# 点击空白区域关闭model
在弹窗和所有页面其他内容之间放一个透明层，点那个层的时候关闭。

```html
<!-- popup -->
<div id="gift-container" style="display:none">

	<div id="gift-content-mask" style="display:none"></div>  
	↑mask要和内容同级。不能为父级，不然就点哪里都会关了。
	
	<img id='gift-content' src="images/lisijiao.png" alt="">
	↑model popup的内容。

</div>
```



```jquery
$(document).mouseup(function(e){
  var area = $(' 目标区域 ');   // 设置model的区域
  if(!area.is(e.target) && area.has(e.target).length === 0){ // Mark 1
    some code...   // 功能代码
  }
});
/* Mark 1 的原理：
判断点击事件发生在区域外的条件是：
1. 点击事件的对象不是目标区域本身
2. 事件对象同时也不是目标区域的子元素
*/
```

