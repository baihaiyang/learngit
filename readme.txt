Git Bash 操作命令
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
（前两个命令自报家门，是哪台机器，哪个账号和邮箱）
$ mkdir learngit
（创建文件）
$ cd learngit
（打开文件）
$ pwd
（查看当期目录）
$ git init
（把当前目录编程git可以管理的仓库）
$ git add readme.txt
（创建文件以后，将文件添加到仓库）
$ git commit -m "wrote a readme file"
（将添加的文件提交到仓库，双引号里边是关于此次修改或新建的描述）
$ git status
（查看当前仓库的状态）
$ git diff readme.txt
（查看readme.txt有哪些改动）
$ git log
（查看历史记录）
$ git log --pretty=oneline
（查看简化的历史记录）
$ git reset --hard HEAD^或者HEAD^^等等
（版本回退）
$ git reset --hard 123sfdd
（回退到指定序号的版本）
$ cat readme.txt
（查看文件内容）
$ git reflog
（记录每一次的命令）

我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支

$ git checkout -- readme.txt
（命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。总之，就是让这个文件回到最近一次git commit或git add时的状态。）
$ git reset HEAD readme.txt
（Git同样告诉我们，用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区）

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库

$ git remote add origin git@github.com:whiteoceans/learngit.git
（关联一个远程库）
$ git push -u origin master
（第一次推送master分支的所有内容，此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改）
$ git clone git@github.com:whiteoceans/gitskills.git
（从远程库克隆岛本地库）








