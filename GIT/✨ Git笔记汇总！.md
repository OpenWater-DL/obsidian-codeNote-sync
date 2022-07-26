# 教程
[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600/900005860592480)

[三分钟入门Git概念+gitkraken](https://www.bilibili.com/video/BV1KD4y1S7FL/?spm_id_from=333.788.recommend_more_video.0)

[边做边学git](https://try.github.io/)


# 教程导航
[git命令速查](https://www.w3cschool.cn/git/git-cheat-sheet.html)
![[src/img/Pasted image 20220726034541.png]]

[[git命令速查表]]



# 将远程仓库克隆至本地
去到要同步的文件夹后
git clone 加上要同步的那个仓库的地址
git pull 从网上的仓库同步下来

`git status `查看状态


`git add index.html ` 添加一个文件
`git add -A` 
`git add . `都是添加所有可以同步的文件


`git commit -m "writte a massege"` 提交到本地版本库（跟网上的没关系）

`git push` 上传，这个才会提交到网上的仓库。


# vim
## 命令模式：

用户刚刚启动 vi/vim，便进入了命令模式。

此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。

以下是常用的几个命令：

-   **i** 切换到输入模式，以输入字符。
-   **x** 删除当前光标所在处的字符。
-   **:** 切换到底线命令模式，以在最底一行输入命令。

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

命令模式只有一些最基本的命令，因此仍要依靠底线命令模式输入更多命令。

切换回来`esc`

在这个状态下可以通过一些命令来操作文本。
`:wq`  退出时保存修改
 `:q` 直接退出是
 `d0` 光标位到这行开头都删掉
 `.` 重复动作
 `u` 撤销（回一步）
 `ctrl r` 重做(进一步)
 [详细](https://www.runoob.com/linux/linux-vim.html)


# 创建branch
`git branch feature1 `创建一个叫feature1的分支
 
 `git checkout -b <your-branch-name>` 
or
 `git switch -c <your-branch-name>`
创建一个新的分支同时切换到新创建的分支(用后面这个语义更科学)



# 切换分支
`git checkout feature1` 
`git switch feature1`
效果一样后面这个语义更科学

# 合并分支
` git merge feature1`
假设现在是在main上。用merge就会把别的分支合并过来。
如果合并时出现了冲突，就要去相关文件里解决冲突，然后重新commit。

# 显示图表
`git log --graph `
`git log --graph --pretty=oneline --abbrev-commit` 好看模式：信息只显示一行
(–graph 图形  –pretty=oneline 一行显示  –abbrev-commit 头部数据减少)


# commit
## 覆盖修改而非增加commit
这样做就可以不增加新的commit ID
```
git commit --amend
# 追加提交，它可以在不增加一个新的commit-id的情况下将新修改的代码追加到前一次的commit-id中

```

## 优雅地合并多个commit
https://github.com/Jisuanke/tech-exp/issues/13

# Rebase 变基
error: 没有父提交的情况下不能 ‘fixup’ 
您可以用`git rebase --edit-todo` 修正，
然后执行`git rebase --continue`。
或者您可以用`git rebase --abort` 终止变基。

是因为在rebase的时候最上层一定要出现保留一个commit,例如：
```
pick f6451e9 add 
fixup 36dc32d add
```


前缀修改为：
-   `squash`：使用该 Commit，但会被合并到前一个 Commit 当中
-   `fixup`：就像 `squash` 那样，但会抛弃这个 Commit 的 Commit message


# 关联远程仓库、push
```git
git remote add https://xxxxxxxxx.git

URL是远程仓库的链接。

git push -u origin main

```



# 解除关联
git remote remove origin


# 解除git状态
```git
find . -name ".git" | xargs rm -Rf

```


# 本地全局设定
git config --global user.email "hdl2100598@126.com"
  git config --global user.name "waterkon"


# 疑难杂症
[[GIT/202110281633 Git 设置全局忽略文件的方法]]
[[GIT/202110290124 Git 使用git-orphan清理git历史]]
[mac git命令按Tab不能自动补全解决方法
](https://blog.csdn.net/qq_43111384/article/details/104331312)