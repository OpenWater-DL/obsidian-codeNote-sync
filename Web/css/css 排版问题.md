#css 
#排版 

### 如何排2x2的图片矩阵？
```html
html结构是这样的：
<section class\="manga"\>

	<ul\>

		<li\> <img src\="img/img\_funatabi02.jpg" alt\="title"\></li\>

		<li\> <img src\="img/img\_funatabi03.jpg" alt\="title"\></li\>

		<li\> <img src\="img/img\_funatabi05.jpg" alt\="title"\></li\>

		<li\><img src\="img/img\_funatabi04.jpg" alt\="title"\></li\>

	</ul\>
</section\>
```


矩阵排列要点：
1. 让li的宽度变为父级ul的50% （这样就会填满 ul不留边距，且会随着ul的width灵活变化）
2. 让作为块的li 变成float:left （这样就能换行，不留左右间隙）
3. 让父级的ul  ，margin:0 auto; 便是相对于更父级的块居中。
```css 
.manga ul {
width: 500px;
background-color: red;
margin: 0 auto;
}
 
 .manga li {
float: left;
width: 50%;} 

.manga img {
width: 100%;
}
```
![[css22矩阵图片排列.png]]
*另外使用inline-block是会存在间隙的，所以这里用了float。*


---

### 如何自动根据宽度调整图片的换行？
```
flex-wrap: wrap;
```


### 如何居中？
子对象控制间距，组对象控制大位置，和ai逻辑一样。
```css
 main ul{
            background-color: ivory;
            width: fit-content; //边距自适应
            margin: 0 auto; //父级对象控制居中
        }
        main li{
        display: inline-block; 
        margin-inline: 10px; //对象间各自边缘有10px的区域。
        }
```

-   2021-01-07  -   22:30
- #### 让列表对象变横排。
```css
.class ul li{

list-style-type: none;

display:inline-block;
}

或者用

float: left;

```

-   2021-01-07  -   22:37
- #### 指针
变手指
```css
cursor: pointer;
```

悬浮发生样式的变化hover
```css
.tab ul li:hover{
color:red;

}
```