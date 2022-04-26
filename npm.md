### 依赖重装
```bash
npm install -g rimraf
rimraf node_modules
npm install -g cnpm --registry=https://registry.npmmirror.com
rimraf package-lock.json
npm cache clear --force
npm install
```

### 合并分支并创建合并提交

- 用于`git checkout <target-branch>`切换到要合并的分支。
- 用于`git merge --no-ff -m <message> <source-branch>`将分支合并到当前分支，使用指定的`<message>`.

``` bash
git checkout <target-branch>
git merge --no-ff -m <message> <source-branch>

git checkout master
git merge --no-ff -m "Merge patch-1" patch-1
# Merges the `patch-1` branch into `master` and creates a commit
# with the message "Merge patch-1"
```

