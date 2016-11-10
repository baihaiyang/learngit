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
Git分支
	首先，我们创建dev分支，然后切换到dev分支：
	$ git checkout -b dev
	Switched to a new branch 'dev'
	git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：

	$ git branch dev
	$ git checkout dev
	Switched to branch 'dev'
	然后，用git branch命令查看当前分支：

	$ git branch
	* dev
	  master
	git branch命令会列出所有分支，当前分支前面会标一个*号。

	然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改，加上一行：

	Creating a new branch is quick.
	然后提交：

	$ git add readme.txt 
	$ git commit -m "branch test"
	[dev fec145a] branch test
	 1 file changed, 1 insertion(+)
	现在，dev分支的工作完成，我们就可以切换回master分支：

	$ git checkout master
	Switched to branch 'master'
	切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：

	git-br-on-master

	现在，我们把dev分支的工作成果合并到master分支上：

	$ git merge dev
	Updating d17efd8..fec145a
	Fast-forward
	 readme.txt |    1 +
	 1 file changed, 1 insertion(+)
	git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。

	注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

	当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。

	合并完成后，就可以放心地删除dev分支了：

	$ git branch -d dev
	Deleted branch dev (was fec145a).
	删除后，查看branch，就只剩下master分支了：

	$ git branch
	* master
	因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。
	Git鼓励大量使用分支：

	查看分支：git branch

	创建分支：git branch <name>

	切换分支：git checkout <name>

	创建+切换分支：git checkout -b <name>

	合并某分支到当前分支：git merge <name>

	删除分支：git branch -d <name>
3、两个分支都有修改提交冲突以后的解决办法
	准备新的feature1分支，继续我们的新分支开发：

	$ git checkout -b feature1
	Switched to a new branch 'feature1'
	修改readme.txt最后一行，改为：

	Creating a new branch is quick AND simple.
	在feature1分支上提交：

	$ git add readme.txt 
	$ git commit -m "AND simple"
	[feature1 75a857c] AND simple
	 1 file changed, 1 insertion(+), 1 deletion(-)
	切换到master分支：

	$ git checkout master
	Switched to branch 'master'
	Your branch is ahead of 'origin/master' by 1 commit.
	Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。

	在master分支上把readme.txt文件的最后一行改为：

	Creating a new branch is quick & simple.
	提交：

	$ git add readme.txt 
	$ git commit -m "& simple"
	[master 400b400] & simple
	 1 file changed, 1 insertion(+), 1 deletion(-)
	现在，master分支和feature1分支各自都分别有新的提交，变成了这样：

	git-br-feature1

	这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，我们试试看：

	$ git merge feature1
	Auto-merging readme.txt
	CONFLICT (content): Merge conflict in readme.txt
	Automatic merge failed; fix conflicts and then commit the result.
	果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。git status也可以告诉我们冲突的文件：

	$ git status
	# On branch master
	# Your branch is ahead of 'origin/master' by 2 commits.
	#
	# Unmerged paths:
	#   (use "git add/rm <file>..." as appropriate to mark resolution)
	#
	#       both modified:      readme.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")




