# git学习笔记

## 1. 安装完成初始化设置 
    git config --giobal user.name "RookieCui"
    git config --global user.email "1195791948@qq.com"

## 2. 基本操作创建版本空仓库（在某个空文件夹中）

    git init 
将新建的文件添加到暂存区stage（可以多次使用）

    git add xxx
将添加到暂存区stage的所有文件提交到仓库master

    git commit -m "add message"
## 3. 修改、查看并再次提交查看仓库当前状态

    git status
查看修改过的未提交的文件中具体修改的内容
(注意:查看时是以vim编辑器的状态查看，上下键翻页，查看完成退出输入q)

    git diff readme.txt
再次提交

    git add readme.txt
    git commit -m "add 1111"
## 4. 版本回退查看提交历史记录（命令窗口没关时才行）

    git log 最近到最远
    git log --pretty=oline 精简版本
查看命令历史记录

    git reflog

* 版本号 commit id 一串数，用于版本回退之类的
* 当前版本 HEAD
* 上一个版本 HEAD^
* 上上个版本 HEAD^^
* 往前100个版本 HEAD~100
回退到上一个版本

    git reset --hard HEAD^
回退到某个版本
    git reset --hard (commit id前几位即可)
工作区 -->git add-->{stage（暂存区）-->git commit-->master(仓库)}大括号内合称版本库

工作区新增文件，未add入暂存区，其状态是untracked
git commit完成后，stage处于空状态

## 5. 管理修改
git只是跟踪和提交修改部分的内容，修改后必须按程序先将修改加到暂存区，再将其提交到仓库，修改部分才能提交到仓库，如果修改后未提交到暂存区是无法直接将修改提交到仓库的

查看工作区和版本库里面最新版本的区别

    git diff HEAD --readme.txt

## 6. 撤销修改撤销修改让这个文件回到最近一次git commit或git add时的状态

    git checkout -- <file>

如果要撤销暂存区尚未commit的修改，应该先将暂存区版本回退到仓库中的最近的版本，然后将工作区checkout回去即可

    git reset HEAD <file>
    git checkout -- <file>

## 7. 删除文件删除文件，与add类似

    git rm <flie>
同步删除到仓库

    git commit -m ""
从仓库恢复被删除文件(删除文件，与add类似

    git rm <flie>
同步删除到仓库

    git commit -m "")
    git checkout -- <file>
## 8. github远程仓库托管创建SSH Key

    ssh-keygen -t rsa -C "youremail@example.com"
        
用户主目录里生成.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥
github上添加公钥即可上传代码，任何一台电脑想上传程序都需要将其SSH公钥添加到github中

## 9. 添加远程仓库在github中创建新的远程仓库,将本地仓库与远程仓库关联起来

    git remote add origin https://github.com/RookieCui/learngits.git
远程仓库的名字origin

    git branch -M main
第一次将本地仓库推送到远程仓库

    git push -u origin main
由于远程库是空的，我们第一次推送main分支时，加上了-u参数，Git不但会把本地的main分支内容推送的远程新的main分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。后续push

    git push origin main
查看远程库信息

    git remote -v
删除远程库与本地仓库之间的关联

    git remote rm origin

## 10. 从远程库克隆从0开始开发最好县创建远程库然后从远程库克隆

    git clone git@github.com:RookieCui/gitskills.git
## 11. 创建与合并分支分支管理的理解
 可以创建属于自己的分支进行开发，开发过程中可以随时push，开发完与主分支进行合并即可，不会影响别人工作。
* HEAD-->master（主分支）-->最新的提交(每次提交master向前移动一步)
* 创建新分支dev HEAD-->dev -->可以提交(理解:HEAD始终指向当前可以操作的分支)
* 合并分支dev到master master --> dev 即可

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
分支合并可能存在的向冲突问题
'''

Creating a new branch is quick & simple.
'''

在主分支手动修改这部分内容后保存提交查看合并情况

    git log --graph --pretty=oneline --abbrev-commit
## 12. 分支管理策略
分支合并时的Fast forward模式，删除分支后回丢掉分支信息，可以强制禁止这种模式，禁止后merge时git会生成一个新的commit禁用Fast forward模式合并分支

    git merge --no-ff -m "merge with no-ff"
查看合并后的历史

    git log --graph --pretty=oneline --abbrev-commit

## 13. bug分支
临时有bug需要修复时可以将当前工作储藏起来等解决完bug在继续恢复工作
把当前工作存起来

    git stash
切换到main分支

    git switch main
创建issue分支

    git switch -c issue-101
修复完成提交bug

    git add <file>
    git commit -m "fix bug 101"
修复完成回到main分支并合并分支

    git switch main
    git merge --no-ff -m "merge bug fix 101" issue-101
修复完成回到dev分支干活

    git switch dev
    git status
查看并恢复工作区内容

    git stash list
    git stash apply / git stash apply stash@{0}
完成恢复

另外一种情况，bug101刚刚存在于main分支，而dev分支时main分支早些时候分出去的，bug101也存在于dev分支故需要将main分支修复好的bug不知道dev分支
只需要将提交的

切换到dev分支

    git switch dev
复制bug提交

    git cherry-pick <commit>

## 14. Feature分支
开发新功能时的创建这个分支，然后开发完成后将这个分支和主分支合并然后将该分支删除就行

创建新分支

    git switch -c feature-vulcan
开发完成新功能并提交

    git add <file>
    git commit -m "add feature vulcan"
切回dev分支并合并

    git merge --no-ff feature-vulcan
如果要撤销并删除分支

    git branch -d feature-vulcan
强制删除分支

    git branch -D feature-vulcan

## 16. 多人协作
查看远程信息库

    git remote (-v) 加-v可以显示更加详细的信息
推送分支,要指出本地的分支，或者其他想要推送的分支

    git push oring main/dev

* master分支是主分支，因此要时刻与远程同步；
* dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
* bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
* feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发

抓取分支

    git clone git@github.com:RookieCui/learngit.git
当你从远程clone下来代码只有main分支需要重新创建dev分支

    git checkout -b dev oring/dev
开发提交

    git add env.txt
    git commit -m "add env"
将dev分支push到远程端

    git push origin dev
如果和别人的文件冲突，需要将远程端的文件抓下来然后解决冲突再推送

    git pull
没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
    
    git branch --set-upstream-to=origin/dev dev
    git pull
手动解决冲突并合并
推送远程分支后分支一坨一坨的，通过git rebase可以优化

## 17. 标签管理
发布新版本时在版本库中打一个标签，与commit息息相关

在main分支下打标签

    git tag v1.0
将之前提交的commit打标签

    git tag v0.9 <commit id>
    git tag (按照字母顺序查看标签)
查看标签信息

    git show <tagname>
创建带有说明的标签，用-a指定标签名，-m指定说明文字

    git tag -a v0.1 -m "version 0.1 released" 1094adb
删除标签

    git tag -d v0.1
推送标签到远程

    git push origin <tagname>
一次性推送全部尚未推送到远程的本地标签

    git push origin --tags
删除远程标签

    git push origin :refs/tags/tagname
打完收工