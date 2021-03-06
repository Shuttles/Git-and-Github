# Github教程（by少年宇2019.7.22）

## 在本地建库：

1. 用```git config``` 配置Git，要做的第一件事就是设置名字和邮箱地址（用来设置你提交的时候用的信息）（不用记住命令，会有提示）（且只需第一次使用时配置，后续不必配置）

   代码```git config --list``` 可以查看本地进行的配置

   

2. 创建一个工作目录专门管理这个仓库。

3. 初始化项目，创建新的git仓库

   `git init` 

4. 回到工作目录。（./git相当于一个缓存区、索引）

   ![img](https://wx3.sinaimg.cn/mw690/005LasY6gy1gc9x9yexb9j30k007tt8t.jpg)

   在这个工作目录里可以随意创建文件，比如代码。

5. 将本地这个项目与远端Github进行关联（这有很多行命令，但是在网页上创建库的时候都会有，所以不必记，包括了README.md文件）==注意网页上选地址的时候选SSH的，那个不用免密登录==

6. 写了一些文件后把这些文件添加到缓存区、索引（git）

   `git add <filename>` Or `git add *`

   

   

7. 从缓存区放到HEAD

   `git commit -m "description"`

   

8. 最后推送到github远端

   `git push ` 

   PS:泽哥说，第一次提交 后面要加 -u origin master

   

9. 如果第九步报错可能是远端已有更新，所以需要

   `git pull`

   

### 常用操作

| 命令                            | 操作                             |
| ------------------------------- | -------------------------------- |
| git --help                      | 顾名思义                         |
| git status                      | 查看当前本地git状态              |
| git rm <filename>==不要轻易用== | 删除工作目录里的文件和缓存信息   |
| git checkout <filename>         | 如果错误删除了某文件可以这样恢复 |







## 远端建库

克隆到本地的一个工作目录即可

`git clone +xxx`

(xxx可由github网站上的库里取得)
