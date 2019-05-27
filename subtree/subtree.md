# git 管理子项目

## 用[git subtree](https://git-scm.com/book/en/v1/Git-Tools-Subtree-Merging) 实现子项目嵌套 

### 1.添加另一个项目的地址

  ```git
  $ git remote add subtree_remote git@github.com:schacon/subtree.git
  $ git fetch subtree_remote
  warning: no common commits
  remote: Counting objects: 3184, done.
  remote: Compressing objects: 100% (1465/1465), done.
  remote: Total 3184 (delta 1952), reused 2770 (delta 1675)
  Receiving objects: 100% (3184/3184), 677.42 KiB | 4 KiB/s, done.
  Resolving deltas: 100% (1952/1952), done.
  From git@github.com:schacon/subtree
  * [new branch]      build      -> subtree_remote/build
  * [new branch]      master     -> subtree_remote/master
  $ git checkout -b subtree_branch subtree_remote/master
  Branch subtree_branch set up to track remote branch refs/remotes/subtree_remote/master.
  Switched to a new branch "subtree_branch"
  ```

> 在subtree_branch分支就可以看到subtree项目的master分支的文件，但是这样subtree子项目只是作为当前项目的一个分支。

```shell
# subtree_branch分支的文件
$ ls
README.md   subtree.txt
# 切换到master分支，查看文件
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
$ ls
LICENSE    readme.txt test.txt
```

### 2.用`git read-tree`将另一个项目变成该项目的一个子文件夹

  ``` shell
  $ git read-tree --prefix=subtree/ -u subtree_branch
  # 项目subtree的文件保存在新创建的subtree文件夹中
  $ ls
  LICENSE    readme.txt subtree    test.txt
  ```
