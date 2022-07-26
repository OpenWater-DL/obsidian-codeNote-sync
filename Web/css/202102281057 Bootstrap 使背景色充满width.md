
-   [HTML](https://codepen.io/JacobLett/embed/YpZbqY/?height=300&theme-id=21777&default-tab=html,result#html-box)
 -   [CSS](https://codepen.io/JacobLett/embed/YpZbqY/?height=300&theme-id=21777&default-tab=html,result#css-box)

-   [Result](https://codepen.io/JacobLett/embed/YpZbqY/?height=300&theme-id=21777&default-tab=html,result#result-box)
 -   [Skip Results Iframe](https://codepen.io/JacobLett/embed/YpZbqY/?height=300&theme-id=21777&default-tab=html,result#resources-link)

[EDIT ON](https://codepen.io/JacobLett/pen/YpZbqY "Edit on CodePen")

思路很简洁，就是在container外面包一个section，设置这个section的颜色。

```html
	<h1>Section background colors</h1>

	<section class="bg-primary text-center">
	   <div class="container">


		  <h2>Design is improvement. Design is improvement.</h2>


	   </div>
	   <!-- /.container-->
	</section>

```


```css
section {padding:2rem;}
.bg-primary {background-color:#007aeb;color:#fff;}
.bg-gray {background-color:#cccccc;}

```
