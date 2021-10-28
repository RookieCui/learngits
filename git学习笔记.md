git学习笔记

1. 安装完成初始化设置 
git config --giobal user.name "RookieCui"
git config --global user.email "1195791948@qq.com"

2. 基本操作
创建版本空仓库（在某个空文件夹中）
git init 
将新建的文件添加到仓库（可以多次使用）
git add xxx
将添加到仓库的文件提交到仓库
git commit -m "add message"
至此完成首次提交

3. 修改、查看并再次提交
查看仓库当前状态
git status
查看修改过的未提交的文件中具体修改的内容
git diff readme.txt
git add readme.txt
git commit -m "add 1111"

4.版本回退
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
