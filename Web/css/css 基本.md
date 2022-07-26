#css

[[css选择器]]
[学习css布局](https://zh.learnlayout.com/margin-auto.html)

---

### 调整边距的方法
margin 外边距
padding 内边距

写法细节
```html
padding: 20px ; 四边
 	padding: 10px 20px ; //上下，左右
	padding: 10px 20px 30px 40px ;顺时针，↑→↓← 
	


```

display： block和inline;flex
*	inline是所有的元素都跑到同一行里，宽度由其内容决定。无法人工指定宽度了。
* inline-block可以设置宽度
* flex要去父级指定。例如要给div设定，你要去父级的section的选择器里设定。
	* 然后设置flex-direction ：row 或者别的，用来设定排列的方向。
	* 然后再div里设置margin:auto，就会 自动平均分布。
	#弹性布局

* div本身就是块级(block)。

### 调用css样式表
```html
	<link rel\="stylesheet" href\="styles.css"\>
```

[[css选择器]]

[[响应式设计]]