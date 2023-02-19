---
title: Git操作文档
date: 2023-02-18 17:15:19
category: ["技术"]
tags: ["Git"]
---

### 提交（Commit） ###

#### 查看HEAD上最近一次的提交（commit） ####
```git
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
git commit --amend --author 'new authorname email'
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
git push -f origin my-branch
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
git checkout -b my-branch
```

#### 把未暂存的内容移动到另一个已存在的分支 ####
```git
git stash

git checkout my-branch

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

#### 保留来自另一个ref-ish的整体文件 ####
```git
git add -A && git commit -m "commit message"

git checkout solution -- file.txt
```

#### 删除上游（upstream）分支被删除了的本地分支 ####
```git
git fetch -p
```

#### 不小心删除了分支 ####
```git
git checkout -b my-branch

git branch

git reflog

git checkout -b my-branch
```

#### 删除一个远程分支 ####
```git
git push origin --delete my-branch

git push origin :my-branch
```

#### 删除一个本地分支 ####
```git
git branch -D my-branch
```

#### 从别人正在工作的远程分支迁出（checkout）一个分支 ####
```git
git fetch --all

git checkout --track origin/[branch]
```

### Rebasing和合并（Merging） ###

#### 撤销rebase/merge ####
```git
git reset --hard ORIG_HEAD
```

#### 已经rebase，但不想强推（force push） ####
```git
git checkout my-branch

git rebase -i main

git checkout main

git merge --ff-only my-branch
```

#### 需要组合（combine）几个提交 ####
```git
git reset --soft main

git commit -am "new awesome feature"

git rebase -i main

git rebase -i HEAD~2
```

#### 安全合并（merging）策略 ####
```git
git merge --no-ff --no-commit my-branch
```

#### 将一个分支合并成一个提交 ####
```git
git merge --squash my-branch
```

#### 组合（combine）未推的提交 ####
```git
git rebase -i @{u}
```

#### 检查是否分支上的所有提交都已经合并 ####
```git
git log --graph --left-right --cherry-pick --outline HEAD...feature/120-on-scroll

git log main ^feature/120-on-scroll --no-merges
```

#### 暂存所有改动 ####
```git
git stash

git stash -u
```

#### 暂存指定文件 ####
```git
git stash push working-directory-path/filename.ext

git stash push working-directory-path/filename1.ext working-directory-path/filename2.ext
```

#### 暂存时记录消息 ####
```git
git stash save <message>

git stash push -m <message>
```

#### 使用某个指定暂存 ####
```git
git stash list

git stash apply "stash@{n}"

git stash apply "stash@{2.hours.ago}"
```

#### 暂存时保留未暂存的内容 ####
```git
git stash create

git stash store -m "commit message" CREATED_SHA1
```

### 杂项 ###

#### 克隆所有子模块 ####
```git
git clone --recursive git://github.com/foo/bar.git

git submodule update --init --recursive
```

#### 删除标签（tag） ####
```git
git tag -d <tag_name>

git push <remote> :refs/tags/<tag_name>
```

#### 恢复已删除标签 ####
```git
git fsck --uncreachable | grep tag

git update-ref refs/tags/<tag_name> <hash>
```

### 跟踪文件（Tracking Files） ###

#### 只改变一个文件名字，不修改内容 ####
```git
git mv --force myfile MyFile
```

#### 从Git删除一个文件，但保留该文件 ####
```git
git rm --cached log.txt
```

### 配置（Configuration） ###

#### 缓存一个仓库（repository）的用户名和密码 ####
```git
git config --global credential.helper cache

git config --global credential.helper 'cache --timeout=3600'
```

