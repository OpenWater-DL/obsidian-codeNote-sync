创建git仓库有两种方法。
1.本地创建一个文件夹，GitHub上创建一个仓库，然后在本地的文件夹中用终端输入git命令来创建本地的git仓库、关联到GitHub上的仓库。

准备工作，在GitHub上创建一个新仓库，然后不要创建任何东西（比如README.md）。
之后跟着GitHub提示的操作走。
在本地的操作要点大概是下面这些：

1. 指定当前所在文件夹是git仓库
```
git init 
``` 

2. 之后就是常规的git操作。


3. 指定对应的远端的git仓库
```
git remote add origin 加上Repo的https链接。

```

4. 第一次要建立对应的上游分支