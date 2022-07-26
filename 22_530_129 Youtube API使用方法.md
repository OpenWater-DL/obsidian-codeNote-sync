[youtube DataAPI](https://developers.google.com/youtube/v3/docs/playlistItems/list?apix_params=%7B%22part%22%3A%5B%22snippet%22%5D%2C%22playlistId%22%3A%22PLcyPc8deg1u4WC1yoZT2qvTOLX_JmkxH4%22%7D#usage)

# 准备工作
[准备工作](https://developers.google.com/youtube/v3/getting-started)
具体操作方法看官方文档。

大意：需要去 Google API Console激活youtube的api。
**YouTube Data API v3**.

 OAuth 2.0 authorization是关于用户授权的，我暂时用不到。
 应该主要是那些要上传修改视频内容才用到。

# 界面基本
![[src/img/Pasted image 20220530133437.png]]
说明文档还是比较好的，可以直接用网站的这个工具。不用自己在本地敲代码。简单快速拿到json。
![[src/img/Pasted image 20220530141736.png]]


# playlist 和 playlistItems的区别
“很多相册”和“一本相册里的内容们”的区别。

**playlist**对应的是频道的“播放列表”，在此调用数据，会得到“列表”的信息。
比如调用就会拿到这个页面的信息，有多少个list，分别叫啥名字等等。
![[src/img/Pasted image 20220530140740.png]]

**playlistItems**顾名思义，就是项目，能拿到具体的某个list里面的视频信息。比如【至高シリズ】里的每一个video的概要栏信息就可以从items拿到。
![[src/img/Pasted image 20220530141018.png]]

# 获取id
直接的方法是看URL，url看不出来的时候就进后台看源码，搜一搜关键词。

## 频道ID
如果想要获得特定视频的信息，需要填入它的ID。

![[src/img/Pasted image 20220530134446.png]]
方法一：一般情况下可以通过频道首页直接看到id。UC开头的。
方法二：在方法一这里不显示出来的情况。比如リュウジ的频道。这种时候就看网站源码，搜索channelid即可看到
![[src/img/Pasted image 20220530134711.png]]

## 播放列表ID
![[src/img/Pasted image 20220530141148.png]]

## 视频ID
点【分享】的时候，链接的最后一部分就是。
![[src/img/Pasted image 20220530134740.png]]