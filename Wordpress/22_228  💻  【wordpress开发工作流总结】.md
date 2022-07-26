[[Wordpress/wordpress 如何本地部署和开发主题]]

[WordPress模板开发文档](https://www.wpzhiku.com/document/template-files/)

# 阻力背景：怎样开始工作？
这篇笔记的存在是因为改善这个情况而存在的：
因为我不是像ai那样高频使用WordPress，所以常常会忘记“怎样开始工作”。
故整理一个流程方便指导自己“复健”。


# 一、找到位置：
## 网站项目在电脑的哪里？
- 一个网站的所有文件，就装在一个文件夹里。hexo和WordPress都是这样的。
- 而这个“网站文件夹”，为了方便开发测试，目前我会放在MAMP的doc目录下。
如图，在MAMP的【htdocs】文件夹里，装着3个本地网站文件夹。
![[src/img/Pasted image 20220228145115.png]]

## 访问本地网站的方法
根目录`htdocs`对应`http://localhost:8888/`
所以，如果要访问4dumpling，`http://localhost:8888/4dumpling/ `

## 主题文件夹的位置
大多数时候，只要关注【主题文件夹在哪里】，即可上手开发。
WordPress的主题文件夹位于
`wordpress网站文件夹/wp-content/themes/自己的主题`
![[src/img/Pasted image 20220228150505.png]]

# 二、进入开发工作区
## 个人做法
右键themes， “进入vscode”
![[src/img/Pasted image 20220228150830.png]]

## 网站的页面由哪些文件组成？
[[Wordpress/wordpress主题文件基本结构]]
![[src/img/Pasted image 20220111133921.png]]
注意，上面这张图还缺了个“**front-page.php**”代表主页。

## WordPress的页面生成原理
![[src/img/Pasted image 20220301115824.png]]
### main query 和 sub query的作用：
- main是直接根据当前页面的URL来判断。
- sub 是获得跟当前页面URL没有关系的内容。那怎么获取？就要通过`new WP_Query($args)`,通过传入的`$args`来指定查询条件。它会返回一个查询结果object，下方的例子就是通过这个查询结果，来获得各种需要的信息。例如 `$the_query->have_posts()`
![[src/img/Pasted image 20220301131014.png]]

[メインクエリ、サブクエリ解説！WordPressで自由自在に投稿情報を出力する！（連結講座#5）](https://www.youtube.com/watch?v=03ZSooJCB1Q)



# 三、开发
## 根据你的需要去找到文件
一般的页面不难确认，比如footer之类的。
迷思的是主页和目录页的关系，往下看↓

## 主页设置
这会影响到main query的使用。
### 【最新文章】模式
只有选这个，在主页里使用get_posts才会拿到所有的文章。因为这时候，主循环去查询的是所有的文章。

### 【静态页面】模式
在这个模式里，主页被认为是一个单一的页面。即便get posts,主循环也只能拿到自己的那一页。
① 前提：在admin编辑模式里**指定**主页、文章页。
这一层次可以控制的是，有时候你可能想要加一些话在主页，比如这里我写了“天気がいいから散歩しましょう。”,如果我的模板代码又引入这个部分的变量，则可以配合用户的更改更新内容。
![[src/img/Pasted image 20220228152716.png|300]]

② GUI里的“文章页” →对应→ index.php
“主页”→“front-page.php”

把哪个页面设定为“文章页”，那个页面将会被**覆盖配置**成index.php模板文件里的样子。

>最关键的模板文件是 `index.php` ，如果在模板层次结构中找不到更具体的模板，那么所有请求最终都会被发送到这个模板上。虽然只有 `index.php` 模板就可以工作，但是主题通常会包含一些其他模板，以便在不同的上下文中环境中显示不同的内容。



[☆讲人话的WordPress主题开发教程](https://www.seozen.top/wordpress-theme-development-basic.html)

## 函数
[能看懂☆wpdocs.osdn-文档](https://wpdocs.osdn.jp/%E9%96%A2%E6%95%B0%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9)


函数有两种大的功能分类：表示、取得。
![[src/img/Pasted image 20220228222508.png]]

【表示】就是直接在HTML里显示出来。
【取得】是获得一些数据，但是你不说要怎么用的话，不会有什么可以看到的结果。前缀是get的都是。如果要显示， 用echo打印出来。
【确认】确认现在的页面是什么状态，返回真假。
![[src/img/Pasted image 20220228225647.png]]






# 四、本地开发如何部署到服务器

最简单的方法：装插件 All in one
[# How to Move Wordpress from Local Server to Live Website](https://www.youtube.com/watch?v=E9YTRLm9SQs)
导出为【文件】
然后到服务器端的WordPress里也安装插件，导入文件即可。

如果遇到文章页404，有可能是伪静态出问题了。去宝塔面板的网站-伪静态，选择WordPress即可。[[Web/22_306_110 伪静态是什么]]

# 五、直接在宝塔上部署一个WordPress的方法

# 六、手动更新的办法
https://www.vpsss.net/25355.htm
所有操作的前提是，先备份好！

1.下载最新的WordPress包
2.解压，然后删掉“不需要覆盖的文件”
	![[src/img/Pasted image 20220714224525.png]]
3.**压缩**这个处理好的wp包，上传到宝塔
4.在宝塔里**解压**，然后复制粘贴到原网站目录里（覆盖原本的内容）。
5. http://xxxx/wp-admin/upgrade.php 执行升级命令
6. 到处转转，

# 杂项
## 媒体上传限制
跟php的php.ini配置有关系。
里面会写post_max_size，至于文件去哪里找，还要根据实际的情况去搜索解决方案。
例如MAMP的情况下，要去：
`/Applications/MAMP/bin/php/php8.0.8/conf/php.ini`
这个位置。当然，这是我用的php是8.0.8的版本的情况下。


## hook钩子
[function.php的说人话带图示🇯🇵人讲解](https://www.youtube.com/watch?v=SmiLFgJcLa0&list=PLdnm9ltmuSUkPbKcghap33C-bOoy_95He&index=8)

hook是タイミング


## slug
可以理解为固定链接。slug是指[wordpress](https://so.csdn.net/so/search?q=wordpress&spm=1001.2101.3001.7020)在启用了伪静态后，你的文章(post)与页面(page)、标签(tag)、分类(Category)在访问的时候显示在浏览器地址栏上域名后面的地址。

[渲染的文件使用顺序14秒左右讲到](https://www.youtube.com/watch?v=y9kvRWu8rE4&list=PLdnm9ltmuSUkPbKcghap33C-bOoy_95He&index=10)

## taxonomies,terms
taxonomies{
ttaxonomy是比“分类”更高一级的“神分类”。
	category,
	tag
}

![[src/img/Pasted image 20220228230707.png]]


## 后台增加新的“类文章”选项。
[[Wordpress/wordpress 增加新的文章类]]
![[src/img/Pasted image 20220301211217.png|200]]



# 上传的媒体存到OSS
[WordPress使用阿里云OSS作为媒体库提升网站速度及配置教程](https://www.ly522.com/2252.html)

1. 最好在和服务器同样的一个地区，创建一个“公共读”bucket
2. 获取阿里云账户的accesskey
	1. 进入accesskey管理
	2. 创建一个新的accesskey
	3. 记录下来这个key。
3. WordPress安装插件，搜索 OSS
	有多个选择，我最后选用了WPOSS（阿里云对象储存）
	按上面的提示去填写即可。
	之后再上传，东西便会同步储存到oss。若删除，也会同步把oss里的删除。


# 我的服务器上的用户信息
**wpDemoSite**
visitor
havealook123~