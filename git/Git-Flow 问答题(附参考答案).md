# Git常用操作重点

### 一、如何合并多余 commit？

```shell
#请写出 git 命令
git rebase -i HEAD~n
```

### 二、如何更新主分支?

```shell
#请写出 git 命令
#切换到master主分支或者切换到develop之后
git pull --rebase
```

### 三、Leader 交给你一个任务，需要为某个模块添加新功能，请写出主要的 git 操作。（本地已经存在仓库）

```shell
#请写出 git 命令
git checkout develop
git pull --rebase #更新到最新状态创建新分支
git checkout -b feature/task-xxx
# 一通编码
git add XXX...
git commit -m "message"
# 加入开了一个新的分支，强制push
git push --set-upstream origin feature/task-xxx
```

### 四、测试人员向你反馈了一个在生产版的产品上发现的缺陷，你要修复此漏洞时的主要 git 操作。（本地已经存在仓库）

```shell
#请写出 git 命令
git checkout master
git pull --rebase #更新到最新状态创建新分支
git checkout -b hotfix/bug-xxx
# 一同编码
git add XXX...
git commit -m "message"
git push --set-upstream origin hotfix/bug-xxx
```

### 五、如何更新当前的工作分支（feature/task-2233）以保持与 develop 分支的进度一致？

```shell
#请写出 git 命令
git add xxx...
git commit -m "message"
git rebase develop
```



### 六：恢复初始节点状态，容错处理

```shell
# 回滚提交的commit
git reset + 目标commit的哈希值
# 上面回滚提交以后，文件的内容变成暂存区的内容，暂存区内容也回退到对应commit目标节点
git checkout + 目标文件名字
# 明白结果，复制相应的节点到对应的分支。
git cherry-pick + 要复制的节点的哈希值（可以填写多个）。

```

