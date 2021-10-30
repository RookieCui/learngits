## git学习笔记

学习链接：https://www.liaoxuefeng.com/wiki/896043488029600/896827951938304
1. 安装完成初始化设置 
git config --giobal user.name "RookieCui"
git config --global user.email "1195791948@qq.com"

2. 基本操作
创建版本空仓库（在某个空文件夹中）
git init 
将新建的文件添加到暂存区stage（可以多次使用）
git add xxx
将添加到暂存区stage的所有文件提交到仓库master
git commit -m "add message"
至此完成首次提交

3. 修改、查看并再次提交
查看仓库当前状态
git status
查看修改过的未提交的文件中具体修改的内容
(注意:查看时是以vim编辑器的状态查看，上下键翻页，查看完成退出输入q)
git diff readme.txt
再次提交
git add readme.txt
git commit -m "add 1111"

4. 版本回退
查看提交信息和commit id
    查看提交历史记录（命令窗口没关时才行）
    git log 最近到最远
    git log --pretty=oline 精简版本

    查看命令历史记录
    git reflog

版本号 commit id 一串数，用于版本回退之类的
当前版本 HEAD
上一个版本 HEAD^
上上个版本 HEAD^^
往前100个版本 HEAD~100

回退到上一个版本
git reset --hard HEAD^
回退到某个版本
git reset --hard (commit id前几位即可)

时间：20211029

下次学习起始链接：https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576

5. 工作区 -->git add-->{stage（暂存区）-->git commit-->master(仓库)}大括号内合称版本库
工作区新增文件，未add入暂存区，其状态是untracked
git commit完成后，stage处于空状态

6. 管理修改
git只是跟踪和提交修改部分的内容，修改后必须按程序先将修改加到暂存区，再将其提交到仓库，修改部分才能提交到仓库，如果修改后未提交到暂存区是无法直接将修改提交到仓库的

查看工作区和版本库里面最新版本的区别
git diff HEAD --readme.txt

7. 撤销修改
撤销修改让这个文件回到最近一次git commit或git add时的状态
git checkout -- <file>

如果要撤销暂存区尚未commit的修改，应该先将暂存区版本回退到仓库中的最近的版本，
然后将工作区checkout回去即可
git reset HEAD <file>
git checkout -- <file>

8. 删除文件
rm <file>是会被git跟踪的
从仓库恢复被删除文件
git checkout -- <file>

删除文件，与add类似
git rm <flie>
同步删除到仓库
git commit -m ""

9. github远程仓库托管
创建SSH Key
ssh-keygen -t rsa -C "youremail@example.com"
用户主目录里生成.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥
github上添加公钥即可上传代码，任何一台电脑想上传程序都需要将其SSH公钥添加到github中

时间：20211029

明天学习链接：https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440

10. 添加远程仓库
在github中创建新的远程仓库
将本地仓库与远程仓库关联起来
    git remote add origin https://github.com/RookieCui/learngits.git
远程仓库的名字origin
    git branch -M main
第一次将本地仓库推送到远程仓库
    git push -u origin main
    由于远程库是空的，我们第一次推送main分支时，加上了-u参数，Git不但会把本地的main分支内容推送的远程新的main分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
后续push
    git push origin main
查看远程库信息
    git remote -v
删除远程库与本地仓库之间的关联
    git remote rm origin

11. 从远程库克隆
从0开始开发最好县创建远程库然后从远程库克隆
git clone git@github.com:RookieCui/gitskills.git
git://使用ssh速度快，还可以用https

12. 创建与合并分支
分支管理的理解
可以创建属于自己的分支进行开发，开发过程中可以随时push，开发完与主分支进行合并即可，不会影响
别人工作。
HEAD-->master（主分支）-->最新的提交
每次提交master向前移动一步
创建新分支dev HEAD-->dev -->可以提交
理解:HEAD始终指向当前可以操作的分支
合并分支dev到master master --> dev 即可

具体操作:

创建dev分支并切换到该分支
git checkout -b dev = git switch -c dev
相当于两句命令
git branch dev 创建dev分支
git checkout dev 切换到dev分支 = git switch dev
查看分支
git branch (*指向当前分支)
将dev分支合并到master分支
git merge dev
删除dev分支
git branch -d dev
合并完成

分支合并可能存在的向冲突问题
<<<<<<< HEAD
Creating a new branch is quick & simple.
=======
Creating a new branch is quick AND simple.
>>>>>>> feature1
在主分支手动修改这部分内容后保存提交
查看合并情况
git log --graph --pretty=oneline --abbrev-commit

时间：20211031
下次学习链接：https://www.liaoxuefeng.com/wiki/896043488029600/900005860592480