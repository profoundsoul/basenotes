# 常用 Git 命令清单

原文：<http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html>

> 我每天使用 Git ，但是很多命令记不住。
一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。

![git基本图](imgs/gitrepository.png)

下面是我整理的常用 Git 命令清单。几个专用名词的译名如下。
* Workspace：工作区
* Index / Stage：暂存区
* Repository：仓库区（或本地仓库）
* Remote：远程仓库

## 1. 新建代码库

```
# 在当前目录新建一个Git代码库
$ git init

# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]

# 下载一个项目和它的整个代码历史
$ git clone [url]

```



