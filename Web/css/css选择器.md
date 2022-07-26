1. 嵌套层级（空格） section div {  }
	就是指，section下面的div
2. 列举（逗号）  section , a{ } 
	相当于``` <a> ```标签的也被应用这个样式
3. class 
	```html
	<section class="feature-box">
	</section>
	```
	类名的引号中间有空格，意味着有两个名字。
	引用时，类名前要加"."	
```css
.tofu div { //选择tofu类里的div
border-radius: 50px;}
```
	
4. ID
	```html
	<section ID="hdl">
	</section>
	```
	ID值在页面中只有唯一一个，注意规范。