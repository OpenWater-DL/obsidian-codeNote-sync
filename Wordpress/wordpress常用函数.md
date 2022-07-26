[官方Theme Handbook](https://developer.wordpress.org/themes/)

[youtube手把手从0开始写WordPress主题](https://www.youtube.com/watch?v=FVqzKAUsM68)
# HTML控制
## 获取组件
`get_template_part('inc/front-widgets-top');`

## 读取路径
`<?php echo get_theme_file_uri('/images/library-hero.jpg') ?>`

## 更可靠的创建链接的方式✨
使用这个`<?php echo site_url('/about');?>`来指向页面，这样即使在本地开发，或是上传到服务器，都能用。
`<a href="<?php echo site_url('/about');?>">About Us</a>`


## 菜单制作
### 取得Pages
`wp_list_pages();`
有很多更细致的用法，可以指定child page等等，参考官方doc。
```php

wp_list_pages(array(

'sort_column' => 'menu_order'

));

```


## 显示文章
`the_post()` 返回文章内容（标题、时间、tag、评论等，但要接着写更细致的指令）
	the_content()显示post的内容，
	the_title()显示标题，
	the_time()显示时间等WordPress的Template Tags。

**get_the_title()与the_title()的不同在于get，get里面指定一个id，就能获取那篇文章的标题。**
get_parmelink同理

`have_posts()` 返回真假，判断是否存在post

### 常用调取文章卡片the Loop!
```php
<?php while (have_posts()) : the_post(); ?>

<?php get_template_part('content'); ?>

<?php endwhile; ?>

```

[关于while (have_posts()) : the_post()的详细解释](https://php1st.com/1202)
while就是“如果满足条件，就不断执行”
相当于如果have posts，就不断执行 the_post().

[关于 the_post()的解释](https://blog.csdn.net/weixin_45143481/article/details/108884076)
**the_post()解析：**
the_post函数则调用`$wp_query->the_post()`成员函数前移循环计数器，并且创建一个全局变量`$post`(不是`posts`) ，把当前的post的所有信息都填进这个post变量中，以备接下来使用。
因为`$post`是全局的，所以即便不在循环里，只要在这个页面里（这个html里）都能直接引用到该篇post相关的属性。如the_content()直接显式post的内容，the_title()显式帖子的标题，the_time()显示帖子的时间等WordPress的Template Tags。


## 读取站点信息
`bloginfo('name')`
name可替换成其他词


## 读取自定义属性
`get_theme_mod('heading-enable', 'off')`

'heading-enable' 是 (_必填_) 自定义选项的名称(类型 _string_).

'off'是(_可选_)，(_boolean|string_) 
默认值: false





\
\
\
	
	
---

# function.php常用

## add_action()
告诉wp要挂起一个东西，所以你要告诉wp 挂在哪里，挂什么function——这就是那两个要填入add_action()的变量。

```php

1.定义function
function my_files(){

在这里面写要调用的文件。
wp_enqueue_style('my_main_styles',get_stylesheet_uri())

}

2.把function添加到队列（enqueue）
add_action('wp_enqueue_scripts','my_files');

	tips:后面的my_files没有带括号，是因为它不是立即在这里执行。而是只告诉程序，“嘿，我的function叫这个名字，你到时候去找它吧。”

```
`wp_enqueue_scripts`是一种hook（钩子），它指向了我们写在HTML里wp_head()所在的位置。

### wp_enqueue_style
相当于 <link href='' rel="stylesheet"/>
同理，wp_enqueue_script就是js。
引用网上的库时，可以这样写,http:不写，直接写//
```php
wp_enqueue_style('font-awesome','//maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css');
```


### wp_head()  wp_footer()
wp_head()和wp_footer()像是一种位置坐标。配合function.php里的add_action(  )，它会在里面加载一些我们原本写在纯HTML里的"背景文件",例如css，js。

**而WordPress的头部menu是要加载了wp_footer()才会显示出来的。**



### 挂载css和js
在functions.php文件里，加入下面的代码。注意这个文件的内容也要用php标签包起来。
步骤就是 定义function+把function通过add_action()挂载到某个程序执行时。
```php

//css
function waterInt_regsiter_styles(){
	$version = wp_get_theme()->get('Version');
	wp_enqueue_style('waterInt-style', get_template_directory_uri() . "/style.css", array(),$version,'all'); 
}
 

add_action('wp_enqueue_scripts', 'waterInt_regsiter_styles');


//js
function waterInt_regsiter_scripts()   
    wp_enqueue_script('waterInt-jquery',"https://code.jquery.com/jquery-3.4.1.slim.min.js" ,array(),'3.4.1',true);
}

add_action('wp_enqueue_scripts', 'waterInt_regsiter_scripts');



```

### 当前主题的路径
`get_template_directory_uri()`
连接字符串用点连，例如
```
get_template_directory_uri() . "/style.css"
```

也可以写成
`get_template_directory() . '/functions/theme-options.php'`


## site features
```php
  
function dumpling_features(){
add_theme_support( 'title-tag');
}

add_action('after_setup_theme','dumpling_features');

```




# 继承主题
[子主题](https://codex.wordpress.org/zh-cn:%E5%AD%90%E4%B8%BB%E9%A2%98)



---
# 其他
### 蜜汁占位符 [%3$s] 这类的作用
第一次遇到是在写menu的时候要用ul把多个li包裹住。
所以在items_warp里就遇到了问题，如果只写`<ul ...></ul>`渲染出来将不会包裹住任何东西，空有一对ul。
这就是占位符派上用场的地方：告诉程序，应该在这个位置插入元素。
```php
<?php
wp_nav_menu(
	array(

		'menu' => 'primary',
		'controller' => '',
		'theme_location' => 'primary',
		'items_wrap' => '<ul id=" " class="navbar-nav flex-column text-sm-center text-md-left">%3$s</ul>',
		'depth' => '0'
	)

)
?>

```