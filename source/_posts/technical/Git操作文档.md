---
title: Git操作文档
date: 2023-02-18 17:15:19
category: ["技术"]
tags: ["Git"]
---

### 提交（Commit） ###

#### 查看HEAD上最近一次的提交（commit） ####
```text
git show

git log -n1 -p
```

<!--more-->

#### 修改提交信息（commit message） ####
```git
git commit --amend --only

git commit --amend --only -m 'xxx'
```

#### 修改提交的用户名和邮箱 ####
```git
git commit --amend --author 'new authorname <authoremail@mydomain.com>'
```

#### 从一个提交移除一个文件 ####
```git
git checkout HEAD^ myfile

git add -A

git commit --amend
```

#### 删除最后一次提交 ####
```git
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
```git
git push -f origin branch
```

#### 硬重置（hard reset）后，找回内容 ####
```git
git reflog

git reset --hard SHA1234
```

### 暂存（Staging） ###

#### 把暂存（staging）的内容添加到上一次的提交 ####
```git
git commit --amend
```

#### 只暂存一个新文件的一部分，不是全部 ####
```git
git add --patch[-p] filename.x

git add -N filename.x
```

#### 把在一个文件里的变化（changes）加到两个提交里 ####
```git
git add -p
```

#### 把暂存的内容变成未暂存，把未暂存的内容暂存 ####
```git
git commit -m "WIP"

git add .

git stash

git reset HEAD^

git stash pop --index 0
```

### 未暂存（Unstaged） ###

#### 把未暂存（unstaged）的内容移动到一个新分支 ####
```git
git checkout -b branch
```

#### 把未暂存的内容移动到另一个已存在的分支 ####
```git
git stash

git checkout branch

git stash pop
```

#### 丢弃本地未提交的变化（uncommitted changes） ####
```git
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
```git
git checkout -p

git stash -p

git reset --hard

git stash pop

git stash drop
```

### 分支（Branches） ###

#### 从错误的分支拉取了内容，或把内容推送到了错误的分支 ####
```git
git reflog

git reset --hard [hash]
```

#### 丢弃本地的提交，以便本地分支与远程保持一致 ####
```git
git status

git reset --hard origin/branch
```

#### 需要提交到一个新分支，但错误的提交到了main ####
```git
git branch my-branch

git reset --hard HEAD^

git reset --hard [hash]
```