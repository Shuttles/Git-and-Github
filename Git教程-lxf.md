



# 2.版本

## 1.版本回退



## 2.工作区和暂存区



## 3.管理修改





## 4.撤销修改

1. 场景1：

   当你改乱了工作区某个文件的内容，想直接**丢弃工作区的修改**时，用命令?

   `git checkout -- filename`

2. 场景2：

   当你不但改乱了工作区某个文件的内容，还**添加（add）到了暂存区**时，想丢弃修改，重新放回**工作区**，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

3. `git reset`命令既可以**回退版本**，也可以**把暂存区的修改回退到工作区**。当我们用`HEAD`时，表示最新的版本。

4. 场景3：已经提交（commit）了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送（push）到远程库。



PS：

> 1. git restore 是git 2.23版本新增的命令，用来代替身兼数职的git checkout。功能是一样的。
>
> 2. 在回退未add到暂存区的文件时直接用
>
>    git restore <file>
>
>    git checkout --<file>
>
>    效果一样
>
>    当回退暂存区时（此时文件已经add到暂存区，还未进行commit），使用
>
>    git restore --staged <file>
>
>    git reset HEAD <file>
>
>    效果一样





## 5.删除文件

1. 命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本







# 3.远程仓库

## 3.1添加远程库

1. 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

   关联一个远程库时必须给远程库指定一个名字，`origin`是**默认习惯命名**；

2. 关联后，使用命令`git push -u origin master`**第一次推送master分支**的所有内容；

3. 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

4. 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！





# 4.分支管理

## 4.1创建与合并分支

1. 因为创建、合并和删除分支非常快，所以==Git鼓励你<u>使用分支完成某个任务</u>，<u>合并后再删掉分支</u>，这和直接在`master`分支上工作效果是**一样**的，但过程更**安全**==。
2. 查看分支：`git branch`
3. 创建分支：`git branch <name>`
4. 切换分支：`git checkout <name>`或者`git switch <name>`
5. 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`
6. 合并某分支到**当前**分支：`git merge <name>`
7. 删除分支：`git branch -d <name>`



## 4.2解决冲突

1. 当Git无法自动合并分支时，就必须**首先解决冲突**。解决冲突后，再提交，合并完成。
2. **解决冲突**就是**把Git合并失败的文件手动编辑为我们希望的内容，再提交**。
3. 用`git log --graph`命令可以看到分支合并图。



## 4.3分支管理策略

1. 在实际开发中，我们应该按照几个基本原则进行分支管理：

   首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

   那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

   你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

   所以，团队合作的分支看起来就像这样：

   ![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)

小结

1. Git分支十分强大，在团队开发中应该充分应用。
2. 合并分支时，加上`--no-ff`参数就可以用**普通模**式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就**看不出来曾经做过合并**。



## 4.4bug分支

1. 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
2. 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；
3. 在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。



## 4.5Feature分支

1. 开发一个新feature，最好新建一个分支；
2. 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。



## 4.6多人协作

多人协作的工作模式通常是这样的

1. 首先，可以试图用`git push origin <branch-name>`**推送**自己的修改；
2. 如果推送**失败**，则因为远程分支比你的本地更新，需要先用`git pull`试图**合并**；
3. 如果合并有冲突，则**解决冲突**，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`**推送**就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。



小结

1. 查看远程库信息，使用`git remote -v`；
2. 本地新建的分支如果不推送到远程，对其他人就是不可见的；
3. 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`**抓取**远程的新提交；
4. 在本地**创建**和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
5. 建立本地分支和远程分支的**关联**，使用`git branch --set-upstream branch-name origin/branch-name`；
6. 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



# 4.7rebase



小结

1. rebase操作可以把本地未push的分叉提交历史整理成直线；
2. rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。
