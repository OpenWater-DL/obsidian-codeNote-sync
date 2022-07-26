https://www.youtube.com/watch?v=jV8B24rSN5o
[kevin-Learn CSS Grid the easy way](https://www.youtube.com/watch?v=rg7Fvvl3taU)

[csdn-grid详解](https://blog.csdn.net/battersun/article/details/99823151?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-1-99823151.pc_agg_new_rank&utm_term=css+grid+%E5%8D%A0%E6%BB%A1+%E5%AD%90%E9%A1%B9&spm=1000.2123.3001.4430)

# 基本使用
## 容器-声明grid
```css
.container{
display:grid
grid-gap:10px;//间距
}

```

## 容器-定义列数
```css

.container{
display:grid;

grid-template-columns:repeat(3,1fr);  //表示三列，1fr就是自动均分1分。

}

```


## 综合在一起定义 grid-template
这个属性也接受一个更复杂但非常方便的语法来指定三个上诉属性。这里有一个例子：
CSS 代码:
```
.container {
  grid-template:
    [row1-start] "header header header" 25px [row1-end]
    [row2-start] "footer footer footer" 25px [row2-end]
    / auto 50px auto;
}
```
`[row1-start]`这样的写法是定义网格线的名称。

# 对齐
## 在容器中设定的对齐justify-items
沿着 **inline**（行）轴线对齐网格项(grid items)
（相反的属性是 【align-items】 沿着 **block**（列）轴线对齐）。
此值适用于容器内的所有**网格项**。(注意不是子项)
```
.container { justify-items: start | end | center | stretch; }

-   start：将网格项对齐到其单元格的左侧起始边缘（左侧对齐）
-   end：将网格项对齐到其单元格的右侧结束边缘（右侧对齐）
-   center：将网格项对齐到其单元格的水平中间位置（水平居中对齐）
-   stretch：填满单元格的宽度（默认值）
```

![[src/img/Pasted image 20220124154442.png]]

## 在项目中设定的对齐
这些行为也可以通过每个单独网格项(grid items) 的 `align-self` 属性设置。

# 项目 Grid item
网格容器（Grid Container）的子元素（例如直接子元素）。这里【 item 】元素就是网格项(Grid Item)，但是 【sub-item】 不是。

HTML代码：

```
<div class="container">
  <div class="item"></div> 
  <div class="item">
    <p class="sub-item"></p>
  </div>
  <div class="item"></div>
</div>
```

## 项目-跨列跨行
```css
.grid-item{

grid-column:span 2; // 占用两列宽度。

grid-row:span 2; // 占用两行高度。

}

```

## 项目-指定位置
注意这里
```css
.grid-item{

grid-column:3; // 指定位置在第三个网格线后开始
grid-column-end:5; //在第五根列线结束

//效果来说，就是占用了3，4 两列

或者使用速记：

grid-column:3/5;

}
```




# 间距
`grid-row-gap`属性设置行与行的间隔（行间距），
`grid-column-gap`属性设置列与列的间隔（列间距）。
	```css
 .container {
>   grid-row-gap: 20px;
>   grid-column-gap: 20px;
> }
> ```

对于单个item如果想要设置间距：



# 响应式大招：grid-template-areas
  .（点号） ：代表一个空的网格单元.
  你可以使用任意数量的相邻的 点. 来声明单个空单元格。 
  只要这些点.之间没有空隙隔开，他们就代表一个单独的单元格。

```css
.container { 
grid-template-columns: 50px 50px 50px 50px; 

grid-template-rows: auto; grid-template-areas: 
"header header header header" 
"main main ... sidebar" 
"footer footer footer footer"
; }


```
![[src/img/Pasted image 20220124153904.png]]


 ```

用在响应式设计里最好用。
## 1.先在容器里设定好模板。
```css
.container{

display:grid;

grid-template-areas:
" one two "
"three two"
}

```

## 2.在子项目里设定分别放到哪里去即可
`grid-area`用来指定放到template的哪个区域。

```css
.grid-item1{
grid-area:one;//不用引号
} 
.grid-item2{
grid-area:two; 
}

.grid-item3{
grid-area:three; 
}

```

这样就可以自动变成一个这样的网格layout。
![[src/img/Pasted image 20220116163212.png]]

而如果你设定了响应式
```css
@media(max-width:30em){

	.container{
	
	grid-template-areas:
	"one"
	"two"
	"three";
	
	}
}

```
就可以直接自适应啦！好棒！
![[src/img/Pasted image 20220116163440.png]]

