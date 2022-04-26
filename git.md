### Git 基本指令使用
```bash
git status add . 
git commit -m ""
git remote add origin xxx
git push -u origin master
git remote rm origin
https://www.jianshu.com/p/b5ef57106ff9(依赖重装)
```

#### 仓库无法推送的解决方案
```bash
首先运行拉取命令
git pull --rebase origin master
最后再执行推送命令
git push -u origin master
```
#### 将一个分支合并到当前分支，创建一个合并提交
- 用于git checkout <target-branch>切换到要合并的分支.
- 用于git merge --no-ff -m <message> <source-branch>将分支合并到当前分支，使用指定的<message>.
```bash

git checkout -b dev 新建并切换到本地dev分支

git checkout <target-branch>
git merge --no-ff -m <message> <source-branch>

git checkout master
git merge --no-ff -m "Merge patch-1" patch-1
# Merges the `patch-1` branch into `master` and creates a commit
# with the message "Merge patch-1"
```
### 实现多人开发的过程
https://www.cnblogs.com/onelikeone/p/6857910.html

