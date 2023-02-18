---
title: Git操作文档
date: 2023-02-18 17:15:19
category: ["技术"]
tags: ["Git"]
---

#### 查看HEAD上最近一次的提交（commit） ####
```
git show

git log -n1 -p
```

#### 修改提交信息（commit message） ####
```text
git commit --amend --only

git commit --amend --only -m 'xxx'
```

#### 修改提交（message）的用户名和邮箱 ####
```
git commit --amend --author 'new authorname <authoremail@mydomain.com>'
```

#### 从一个提交（commit）移除一个文件 ####
```
git checkout HEAD^ myfile

git add -A

git commit --amend
```

#### 删除最后一次提交（commit） ####
```
git reset HEAD^ --hard

git push -f [remote][branch]

git reset --soft HEAD@{1}
```
<!--more-->
