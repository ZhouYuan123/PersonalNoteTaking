# Git

## 1. 介绍

​    创始人：Linux创始人。
​    2005年，BitKeeper 不再免费。
​    拥有难以置信的非线性分支管理系统。
​    集中式版本控制系统（DVCS), 分布式版本控制系统（DVCS）.

### 1.1 GIT, GitHub 与 GitLab

* Git是一个版本控制软件

* GitHub与GitLab都是用于管理版本的服务端软件

* GitHub提供免费服务(代码需公开)及付费服务(代码为私有)

* GitLab用于在企业内部管理Git版本库,功能上类似于GitHub

### 1.2 为何？

  本地建立版本库。会有一个全量变化而不是增量(SVN)的变化。
  SVN只有一个版本库(commit ID 可以自增), Git有多个版本库 （commit ID是一个摘要值，这个值通过sha1计算出出来的）。

### 1.3 安装

地址： https://git-scm.com/downloads

## 2. 创建Git库

  which git：git在什么地方。

1. 新建一个文件夹。

2. git init: 创建了当前文件夹的git仓库。
   **.get目录下：管理了git。**

## 3. Git 常用命令

   user.name与user.email的设置。

1. /etc/gitconfig （电脑）, git config --system
2. ~/.gitconfig (用户) , git config --global
3. .git/config  (特定项目) , git config --local

| git init                                                                  | 初始化一个空的git库在当前目录。（如果.git被删除，就不是一个GIT管理的仓库）<br />工作区域：工作区。<br />状态：untracked or modified |
|:------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| git add                                                                   | 进入staged : <br />工作区域：暂存区。<br />状态：staged                                               |
| git commit                                                                | 进入版本库：<br />工作区域：Git 版本库<br />状态：committed                                              |
| git config -l <br/>git config user.name                                   | 看config所有信息<br />看config中的user.name的值                                                   |
| git config --local user.name '李四'<br />git config --local unset user.name |                                                                                         |
| git config                                                                | 打开使用方式说明                                                                                |
| git rm <br />rm                                                           | 删除文件，在暂存区<br />删除文件，在工作区                                                                |
| git mv 原文件名 新文件名 / mv                                                     |                                                                                         |
| git log -n                                                                | 看最近n条提交                                                                                 |
| git log --pretty=oneline                                                  | 每个commit显示到一行                                                                           |
| git log --pretty=format ....                                              | 自定义格式                                                                                   |

## 4. .gitignore

自己新建一个.gitignore  --> 提交这个文件进库

```.gitignore
setting.properties //不追踪这个文件了
*.b // 忽略所有.b结尾的
!a.b // a.b 除外
/TODO // 只忽略根目录下TODO文件
/**/ab // 一个星表示一层目录，两个星表示所有层的目录
```

## 5. 分支

SVN分支是重量级，git分支只是创建了指针。
分支：一个commit对象链。每个commit有个parent commit。
HEAD: 指向当前分支，并指向最新一次提交。
master：指向的是提交。

| git branch                                                  | 查看所有分支。                                                                                    |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| git branch brname                                           | 创建分支。只是更新指针的指向，轻量级。                                                                        |
| git checkout brname                                         | 切换分支。也可以git checkout -, 回刚刚的分支                                                             |
| git checkout -b brname                                      | 创建并且切换。                                                                                    |
| git branch -d brname                                        | 删除分支。只能删除另一个分支。没有merge无法删除。<br/>-D：强制删除。                                                   |
| git merge 另一个分支                                             | 把另一个分支的内容合并过来。自动merge时，fast-forward, 删除分支时会丢掉分支信息。                                         |
| git branch -v                                               | 显示最近一条commit。                                                                              |
| git status --graph                                          | 。                                                                                          |
| git reset HEAD^<br/>git reset HEAD~1<br/>git reset commitID | ^代表回退版本个数。<br/>1: 代表第一个提交<br/>git checkout commitID: 可以创建一个游离的分支。                          |
| git reflog                                                  | git的操作日志。                                                                                  |
| git stash                                                   | 将当前工作区和stage的修改保存起来了。<br/>git stash list. 查看。<br/>git stash pop和git stash apply。一个删除一个不删除。 |

## 6. 标签

`git tag v1.0.1 [-m '内容']` ：新建标签。
`git tag` : 查看标签。
`git tag -d v1.0.1` ：删除标签。

## 7. diff

`git blame 文件名` ：快速查看文件是被谁修改的。

| git diff                      | 工作区和暂存区 |
| ----------------------------- | ------- |
| git diff HEAD                 | 工作区和版本库 |
| git diff --cached [commit_ID] | 暂存区和版本库 |
|                               |         |

`git remote add origin 地址` : origin是默认名字，代表后面紧接着的地址。
`git push -u origin master`: 加了参数-u后，以后即可直接用git push代替git push origin master。


