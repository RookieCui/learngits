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
