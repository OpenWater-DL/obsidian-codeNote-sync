# 1. 文件结构
## 整体文件结构
![[src/img/Pasted image 20220506170546.png]]

## 主题文件关系
![[src/img/Pasted image 20220506173452.png]]
【编辑更新这个图片的方法】
1. 去[excalidraw](https://excalidraw.com/)
2.  载入`/Users/waterkon/Desktop/项目TEM/obsidian/CODE NOTE/Hexo文件图解.excalidraw`这个文件。


---
<div style="width:100%;height:30px;background:yellow;"></div>

# 2. 血泪经验
## 设计的注意点
### rem=16px
默认情况下是16px。
但如果在html{}里设置了font-size:14px;那么rem就是14px。

### 完全包裹住img不留边
img是一种类似text的inline元素，
在结束的时候，会在末尾加上一个空白符，所以就会多出3px。
解决方法有两种：
-   设置img元素`display:block` 或者 `vertical-align: middle;`
-   设置div元素`display:flex`


## 自定义功能
通常需要条件判断
但是使用原生的参数很难找到规则，不如直接自己在.md的font里自定义参数。
![[src/img/Pasted image 20220506233535.png]]

调用example
```ejs

<% if (page.ifcate === 'project'){ %>
<a href="">go to project。</a>
<% } %>

```

分割变量名用下划线_   用-会报错。



## 工具方法、技巧
### css定位 css peek
按住cmd悬停在类名上，点击就能跳转。
或者把光标移到上面之后，用f12直接跳转。


---

# 3.常用ejs代码
[[Web/JS/202102281124 EJS <%-%> <%=%>的区别]]

### 调用模板文件
```ejs
<%- partial('_partial/loader') %>
```
`partial/loader` 是路径。
实际上引用的是` loader.ejs `这个文件。


### 日期格式
```ejs
<%= moment(item.date).format( config.date\_format)%>
```




## 常用判断条件
[hexo辅助函数](https://hexo.io/zh-cn/docs/helpers.html)
包含了常用的一些调用方法。

### 如果是首页
```ejs
<% if(is_home()){ %>
```

### 如果是works页
```ejs
<% if (page.title == "projects"){ %>
```






# 更新上传到服务器

1. 登录宝塔  [[阿里云·腾讯云/宝塔使用方法]]
2. 找到openwater.ink的文件夹，把public备份到本地
3. 上传新的public