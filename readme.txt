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


