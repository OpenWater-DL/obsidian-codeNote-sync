

[Wordpress](https://cn.wordpress.org/support/)
[油管一个两个半小时的教程](https://www.youtube.com/watch?v=-h7gOJbIpmo)

[[Wordpress/21_1121_248  wordpress+阿里云+宝塔]]






# 如何在本地部署运行WordPress
[参考](http://www.rrdaj.com/wzllyy/2852.html)
因为要在本地用编辑器来开发，所以当然要在本地运行。

1. 打开MAMP，运行本地服务器。
2. 点击webStart，查看MAMP自带的php和MySQL信息。
  ![[src/img/Pasted image 20211121195933.png]]
3. 点击phpMyAdmin，创建一个新的数据库。
 ![[src/img/Pasted image 20211121200011.png]]
4. 把从官网上下载的WordPress文件夹，拉到MAMP的目录下。
（在这里可以看到具体是哪个位置）
 ![[src/img/Pasted image 20211121194911.png]]
 然后在浏览器里就能通过 localhost/wordpress访问到了。
 然后WordPress要填的数据库名称，就填刚才创建的那个。用户名密码都是root。
 
 # 使用vscode编辑，初步创建各种文件
 主题文件位于`wordpress/wp-content/themes/你的主题文件夹`里，从这里进入vscode。
 ![[src/img/Pasted image 20211122003746.png]]
 
 php的作用就相当于用来处理html的模板组件。纯html是硬编码，而php则能够动态链接。
 
 ## 基本文件结构
 [[Wordpress/wordpress主题文件基本结构]]
 
 ```
front-page.php
 		-header.php(通过 get_header();获取)
			-wp_head() 用来有条理地载入css
		内容
		-footer.php（通过 get_footer();获取）
			-wp_footer() 用来有条理地载入js
			
funtions.php

```
## 几个关键的php文件解释
page.php => 单个“页面page”,比如about，contact
single.php => 单篇文章post
index.php => 索引页，即post的目录页,与page同级。
-->archive.php =>index.php页面里的container
--->content-archive.php =>一个一个文章的“卡片” part

下面这张图整个页面是index.php
		![[src/img/Pasted image 20211126221057.png]]

---
 
 # 常用代码
 ## php基本
 ```php
 <?php

$x = 3;

function myfunction(){}



 ?>
 ```

有待深入学习
[[Web/详解php占位符 printf()函数]]
[What does the value of '%5$s' mean within Wordpress category listing?](https://stackoverflow.com/questions/32600160/what-does-the-value-of-5s-mean-within-wordpress-category-listing)

[[wordpress常用函数]]