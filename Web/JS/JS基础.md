可以在浏览器的开发者工具里，打开JavaScript控制台。
>快捷键cmd+apt+J

[JS-keyCode](http://www.javascriptkeycode.com/)

**声明**
var 来声明变量
x=1 数字型
x="30" String

**一些单词**
previous 先前的
ElementSibling兄弟元素
parentNode 父节点



**打印**
console.log()

**弹出提醒**
alert();
prompt() 可以让用户输入值，可作为一个变量用。
```js

var name = prompt()

alert(name);

```

文本用单引号 ' '
```js
var prompt('what is your first name')
```

如果文本中出现了单引号，可以通过两种方式解决：
1.外面用双引号包住。
2.要显示的单引号前加一个反斜杠```/```


* 可以在控制台通过上下键来自动补完要运行之前的哪段代码。就不用再手动复制。
* 大于小于和Processing是一样的表示方法。

* 加载是有顺序的，所以先放js脚本的话，就会先执行完脚本，再加载出页面。

function
如果要返回值，用return

## 数组
JS的数组可以混放入任意类型的变量,甚至是再塞一个数组。
```js
function go(){  
alert('hi');
}

var myList=['apple',12,go.['will','laura']];
```
数组编号和Processing一样。myList[0]是Apple。

### 数组操作
==“切出”数据==

**shift**
会将数组的第一项，从原始数组中切出来。原始数组中的第一项将会被删除。
例如
```js
var myList=[1,2];
var test=myList.shift();

> test : 1
>myList:[2]
```
**pop**
切出最后一项。其他同上。

### 循环

==forEach==
```js
var myList=[1,2];
myList.forEach(
function(value,index)){console.log(value,index);}
);

//function那一堆，相当于执行这个function里的命令 这个意思。

```

==while==

==for==

```js

//和Processing很像。
// 数组长度也是 myList.length
for (var i=0; i<10;i++){
console.log('i is',i);
}
```


### DOM操作
获取了某个标签内容后，可以这么干
.innerHTML="新的更改内容"
```js
firstPTag.innerHTML='new p'
```

.className = " "  可以指定到类名

### 监听事件
```js
变量名.addEventListener("事件",执行命令);


变量名.addEventListener("click",function(){
console.log("hi");}
)
```
"click"是鼠标事件
mouseenter 鼠标移入
mouseleave
mousedown
mouseup
mousemove
keydown
keyup
focus 聚焦
blur 失焦
input ^3348e2

可以查文档。