---
title: Git操作文档
date: 2023-02-18 17:15:19
category: ["技术"]
tags: ["Git"]
---

### 提交（Commit） ###

#### 查看HEAD上最近一次的提交（commit） ####
```
git show

git log -n1 -p
```

<!--more-->

#### 修改提交信息（commit message） ####
```
git commit --amend --only

git commit --amend --only -m 'xxx'
```

#### 修改提交的用户名和邮箱 ####
```
git commit --amend --author 'new authorname email'
```

#### 从一个提交移除一个文件 ####
```
git checkout HEAD^ myfile

git add -A

git commit --amend
```

#### 删除最后一次提交 ####
```
git reset HEAD^ --hard

git push -f [remote][branch]

git reset --soft HEAD@{1}
```

#### 删除任意提交 ####
```git
git rebase --onto SHA1_OF_BAD_COMMIT^ SHA1_OF_BAD_COMMIT

git push -f [remote][branch]
```

#### 强推到远端 ####
```
git push -f origin my-branch
```

#### 硬重置（hard reset）后，找回内容 ####
```
git reflog

git reset --hard SHA1234
```

### 暂存（Staging） ###

#### 把暂存（staging）的内容添加到上一次的提交 ####
```
git commit --amend
```

#### 只暂存一个新文件的一部分，不是全部 ####
```
git add --patch[-p] filename.x

git add -N filename.x
```

#### 把在一个文件里的变化（changes）加到两个提交里 ####
```
git add -p
```

#### 把暂存的内容变成未暂存，把未暂存的内容暂存 ####
```
git commit -m "WIP"

git add .

git stash

git reset HEAD^

git stash pop --index 0
```

### 未暂存（Unstaged） ###

#### 把未暂存（unstaged）的内容移动到一个新分支 ####
```
git checkout -b my-branch
```

#### 把未暂存的内容移动到另一个已存在的分支 ####
```
git stash

git checkout my-branch

git stash pop
```

#### 丢弃本地未提交的变化（uncommitted changes） ####
```
// one commit
git reset --hard HEAD^

// two commits
git reset --hard HEAD^^

// four commits
git reset --hard HEAD~4

git checkout -f

git reset filename
```

#### 丢弃某些未暂存的内容 ####
```
git checkout -p

git stash -p

git reset --hard

git stash pop

git stash drop
```

### 分支（Branches） ###

#### 从错误的分支拉取了内容，或把内容推送到了错误的分支 ####
```
git reflog

git reset --hard [hash]
```

#### 丢弃本地的提交，以便本地分支与远程保持一致 ####
```
git status

git reset --hard origin/branch
```

#### 需要提交到一个新分支，但错误的提交到了main ####
```
git branch my-branch

git reset --hard HEAD^

git reset --hard [hash]
```

#### 保留来自另一个ref-ish的整体文件 ####
```
git add -A && git commit -m "commit message"

git checkout solution -- file.txt
```

#### 删除上游（upstream）分支被删除了的本地分支 ####
```
git fetch -p
```

#### 不小心删除了分支 ####
```
git checkout -b my-branch

git branch

git reflog

git checkout -b my-branch
```

#### 删除一个远程分支 ####
```
git push origin --delete my-branch

git push origin :my-branch
```

#### 删除一个本地分支 ####
```
git branch -D my-branch
```

#### 从别人正在工作的远程分支迁出（checkout）一个分支 ####
```
git fetch --all

git checkout --track origin/[branch]
```

### Rebasing和合并（Merging） ###

#### 撤销rebase/merge ####
```
git reset --hard ORIG_HEAD
```

#### 已经rebase，但不想强推（force push） ####
```
git checkout my-branch

git rebase -i main

git checkout main

git merge --ff-only my-branch
```

#### 需要组合（combine）几个提交 ####
```
git reset --soft main

git commit -am "new awesome feature"

git rebase -i main

git rebase -i HEAD~2
```