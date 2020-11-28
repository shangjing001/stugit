### git笔记

##### 创建版本库

1.新建一个空目录，最好不要有中文 （cd进入目录，pwd 显示当前目录）

2.进入这个目录，使用git init  命令创建版本库

常用命令

```
### 配置所有 Git 仓库的 用户名 和 email 
$ git config --global user.name "Your Name"
$ git config --global user.email "youremail@example.com"

### 配置当前 Git 仓库的 用户名 和 email
$ git config user.name "Your Name"
$ git config user.email "youremail@example.com"

### 查看全局配置的 用户名 和 email 
$ git config --global user.name     查看用户名
$ git config --global user.email     查看邮箱地址

### 查看当前仓库配置的 用户名 和 email 
$ git config user.name     查看用户名
$ git config user.email     查看邮箱地址

# Git 是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址
# git config 命令的 --global 参数，用了这个参数，表示你这台机器上所有的 Git 仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址(不加 --global)。

$ git config --list --show-origin 查看所有的配置以及它们所在的文件

(所有命令都在 Git Bash 中运行)
$ git                           查看 git 的相关命令 (git --help)
$ git --version                 查看 git 的版本
$ git config                    查看 git config 的相关命令
$ git pull origin develop       从远程(origin) 的 develop 分支拉取代码
```



##### 文件添加进入版本库

```
1.在目录下新建文档，以纯文本内容编辑文档

2.使用git add  新建的文档名.txt 将文件添加到仓库

3.使用 git commit 命令，讲文件提交到仓库
git commit命令参数解释：
	git commit -m "填入此次提交文本的说明"
注意： git add 命令可以多次使用，添加多个文本，然后一次提交

```

##### 查看文件修改

```
git status  命令，查看仓库状态
git diff 命令，查看你修改的内容
git log 显示最近到最远的提交日志
git log参数解释
	git log --pretty=oneline  简化提交日志
$ git log
$ git log --oneline     #美化输出信息,每个记录显示为一行,显示 commit_id 前几位数
$ git log --pretty=oneline     #美化输出信息,每个记录显示为一行,显示完整的 commit_id
```

##### 版本回退

```
使用HEAD标注版本版本 head 表示当前版本 head^表示上一个版本，head^^表示上两个版本  head~100 表示前一百个版本，以此类推
git reset --hard HEAD^  来回退到上一个版本
git reset --hard HEAD号  前往一个指定版本，HEAD不需要写完整，提供前几位即可

git reflog 查看命令历史，记录之前的操作，可以通过这个命令查找到操作的记录
假如我们依次提交了三个版本 a->b->c,然后昨天我们从版本 c 回退到了版本 b,今天我们又想要回到版本 c,此时就可以使用 reflog 命令来查找 c 版本的 commit_id,然后使用 reset 命令来进行版本回退
```

##### 工作区和暂存区

工作区是电脑里面能够看到的目录

暂存区是存放提交但是未上传到分支的文件

##### 撤销修改和删除文件

```
git checkout --file 可以丢弃工作区的修改，修改有两种情况

	一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
	一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态
	
命令git reset HEAD file 可以把暂存区的修改撤销掉（unstage），重新放回工作区

从版本库删除文件：git rm 然后git commit
文件已经从电脑中删除，但是没有从版本库中删除 使用git checkout file 来讲文件恢复

```

##### 创建远程库和关联本地库

```
将git和github关联起来：
	1.在本地使用命令： ssh-keygen -t rsa -C "youremail@example.com"创建ssh秘钥，youremail@example.com替换为自己的邮件地址，邮件地址就是你创建git仓库的时候输入的邮件地址
	2.创建成功之后，在自己的目录下会找到.ssh文件夹，文件夹中会有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
	3.在自己的github上新建自己的sshkey ，点击add ssh key,将id_rsa.pub中的内容粘贴到新建sshkey的key栏中并输入title，点击新建，就可以在本地仓库和github服务器关联起来

创建远程库
	1.在github上创建自己的仓库，输入对应的名字即可
	2.在本地的git 中运行命令：$ git remote add origin git@github.com:your gitname/仓库名.git
	3.尝试将自己本地的分支推送到github上，使用  git push origin master  命令，可以一次性将自己电脑上的分支推送到远程仓库，第一次推送的时候要使用 git push -u origin master 命令，其他推送不需要加-u 参数
	
```

##### 从远程仓库克隆 (先有远程库)

```
$ git clone git@github.com:renyuns/gitskills.git   renyuns/gitskills 要修改为自己的git用户名和库名
# GitHub 支持多种协议,上面是 ssh 协议,还有 https 协议
可以先把代码从别人的github仓库中fork到自己的github仓库中，然后再拉取到本地

```

##### 将自己github的代码推送到别人的仓库

```
先将仓库fork到自己的github仓库中，然后拉取到本地，在本地将代码修改完成之后，push到自己的github仓库中，然后在GitHub上将代码Pull requset到别人的仓库中
```

