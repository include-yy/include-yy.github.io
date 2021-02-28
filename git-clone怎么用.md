当我们在 github 上面看到好玩的项目时，我们会想要把它下载下来实际操作一下。github 提供了 zip 打包下载，当然我们也可以选择 git clone 来下载，这样更加方便。

>  git-clone - Clone a repository into a new directory

这条指令的作用是将仓库克隆下来到一个新的目录中。参照【1】中的原文可以知道它的功能：

> Clones a repository into a newly created directory, creates remote-tracking branches for each branch in the cloned repository (visible using `git branch --remotes`), and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.



# git clone 的参数

在命令行中运行 `git help clone`，就可以在弹出的网页中看到下面的内容。

```shell
git clone [--template=<template_directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git dir>]
	  [--depth <depth>] [--[no-]single-branch] [--no-tags]
	  [--recurse-submodules[=<pathspec>]] [--[no-]shallow-submodules]
	  [--[no-]remote-submodules] [--jobs <n>] [--sparse]
	  [--filter=<filter>] [--] <repository>
	  [<directory>]
```

我还从来没有用过带参数版本的 `clone` 命令。本文中我参考官方文档和网上的各路文章，对上面的一些比较常用和有用的命令来做一个简单的总结。









# 参考资料

【1】[Git - git-clone Documentation (git-scm.com)](https://git-scm.com/docs/git-clone/en)

【2】[Git clone命令用法_w3cschool](https://www.w3cschool.cn/git/git-uroc2pow.html)


