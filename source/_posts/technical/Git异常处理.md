---
title: Git异常处理
date: 2023-02-19 14:26:11
category: ["技术"]
tags: ["Git"]
---

#### 本地工作区文件恢复 ####
```git
git checkout <filename/dirname>
```

<!--more-->

#### 远程分支删除后，删除本地分支及关联 ####
```git
git branch --unset-upstream <branchname>

git branch --unset-upstream feature/test
```

#### 修改提交时的备注内容 ####
```git
git commit --amend

git log --pretty=online
```

#### 修改分支名 ####
```git
git branch -m <oldbranch> <newbranch>

git branch -m feature/stor-13711 feature/story-13711
```

#### 撤回提交 ####
```git
git reset --soft [<commit-id>/HEAD~n]

git reset --soft HEAD~1

git reset --mixed HEAD~1

git reset --hard HEAD~1
```

#### 撤销本地分支合并 ####
```git
git revert <commit-id>
```

#### 恢复误删的本地分支 ####
```git
git checkout -b <branch-name> <commit-id>

git checkout -b feature/delete HEAD@{2}
```

#### 不确定哪个根治有自己提交的commit ####
```git
git branch --contains <commit-id>
```