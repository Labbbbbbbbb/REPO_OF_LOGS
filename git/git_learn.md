***本文档用于记录git和github使用中的各种实际需求和对应操作***

### 新建git本地仓库

```
git init
```

### 绑定远程仓库以及推送

```
$git remote add origin [remote address]  #常用于将本地仓库与远程仓库进行链接，以便可以同步远程仓库的内容。
$git branch -M main  
#git branch -M main 命令会将本地分支 main 重命名为 main,相当于在本地分支 main 上执行了一个 git branch 命令，这个命令会将当前分支名称设置为 main,并将本地分支 main 与远程分支 main 保持一致。#
$git push -u origin main
#用于将本地分支 main 的更新推送到远程分支 origin/main。在这个命令中，-u 参数指定了推送的分支，origin/main 是远程分支的名称。#
```


如果出现

```
! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/Labbbbbbbbb/REPO_OF_LOGS.git'

```

可能是因为在push之前忘了pull ，使用 ` git pull origin main --allow-unrelated-histories`

再 `push` 即可

`push`的时候可能会出现怎么都连不上网的问题，先检查代理有没有开，如果已经开了还是连接不上`github`服务器，参考：

![image-20240427192948521](C:/Users/86189/AppData/Roaming/Typora/typora-user-images/image-20240427192948521.png)

查看自己的代理端口号，然后更改git的端口配置

```
git config --global http.proxy http://127.0.0.1:7890 
git config --global https.proxy http://127.0.0.1:7890
```

done.

补充：：

```bash
# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

# 查看代理
git config --global --get http.proxy
git config --global --get https.proxy
```


### 回退

```
git checkout <git_log_ID>
```

即可回退到过去的某个节点(如果回退两个节点及以上会出现head detached)，如果想回到过去某个版本并在此基础上来继续编写，一定要记得在checkout回来之后立刻新建分支：

```
git checkout -b <branch_name>
```

否则新做的修改不会保存。并且保险起见，最好在每次工作完成后都push一下，以防出现一些令人b溃的事情。

一旦回退几个版本之间的关系就变成了分支与分支之间的关系，如果回退到过去的某个节点后又想重新回到原先的进度，使用命令

```
git checkout main
```

**如果遇到报错：**

```
The following untracked working tree files would be overwritten by checkout:balabala
```

对于那些在当前分支存在而目标分支不存在的文件，如果你想保存它们---->使用`git stash`暂存文件，切换之后使用`git stash pop`恢复暂存的工作

如果你已经不需要这些文件了，就直接让git复写好了--->

```
git checkout -f <branch>
```





### 融合分支

在某一分支上 `git merge <another_branch_name>`即将另一分支所作的更改融合到本分支上

可能会出现 `conflict`导致 `unmerged`

![1706305105044](image/git_learn/1706305105044.png)

此时可以自行选择要采用哪一方的更改，或者共同比较更改之后再写入

注意这里的merge只是会将所选择的改动写入当前分支并成为新的 `uncommitted changes`，并不会影响那个 <`another_branch_name`>，后续也仍然可以通过 `checkout`来到那个分支



### 子模块submodule

在git仓库中添加内含git仓库的文件时会出现：

![image-20240411232030153](image/git_learn/image-20240411232030153.png)

git允许子模块的嵌套，但是如果是误加的话可以按它的指示删掉

```
 git rm --cached CODE/WTR_Chassis/WTR_Chassis -f
```

其中中间的路径是要删除的文件





### Git ignore

https://blog.csdn.net/Dontla/article/details/131936999
