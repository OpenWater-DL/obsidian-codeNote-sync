git 使用一段时间后 .git 文件夹会非常大，尤其是提交了大文件，当把大文件删除后，仓库大小依旧不变小。这里使用 `git checkout --orphan branch_name` 把 git 的所有 commit 记录清理掉来缩减仓库，相当于重建一个新的仓库了。如果在意历史记录的话这个方法就不太适用了。

```
# 新分支
git checkout --orphan branch_name
# 添加文件
git add -A
# 提交commit
git commit -am "commit message"
# 删除原来分支
git branch -D master
# 重命名分支
git branch -m master
# 提交到远程
git push -f origin master
```

如果有多个分支的话，每个分支都需要按照上面的步骤操作一下。