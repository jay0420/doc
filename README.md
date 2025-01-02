# doc
文档资料


（说明：本流程描述为命令行。源码管理工具的使用方法类似。）
一，创建gib仓库的流程：
1.在gitLab或github上创建一个远程仓库，默认创建master分支

2. 创建本地仓库，创建本地文件README.md，并关联远程仓库
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin https://gitee.com/yaodao666/git-merge-requet.git
git push -u origin master   #git push -u的作用就是关联并推送内容到上远程仓库的master分支，当没有远程分支时还会创建该分支！

3. 创建dev分支方法一。
在gitLab网页上以master分支为起点创建一个dev分支

3.1 本地创建dev分支，并关联远程dev分支
git checkout -b dev   创建一个dev的本地分支。
git branch --set-upstream-to=origin/dev  关联上远程仓库的dev分支


3.2 或者直接使用：
git checkout -b test origin/test
创建本地test分支的同时又链接到远程的test分支上。




4 创建dev分支方法二。
与上面创建dev的方式相同，不过我们这次不先在远程仓库创建分支了，而是在本地直接创建分支后，再将该分支推送到远程。
git checkout dev
git pull
git checkout -b test
在test分支上开发，修改readme.md文件，并推送到远程：
git add -A
git commit -m "这是我第一次在test分支上提交。"
git push -u origin test   #git push -u的作用不仅仅是关联并推送内容到上远程仓库的分支，当没有远程分支时还会创建该分支！


5. test分支合并到dev上。
git checkout dev     #切换到dev分之
git pull    # 在合并前同样先pull一下dev
git merge test    # 这里的合并是本地合并，将test中的内容合并到dev中
git push    # 将本地内容推送到远程仓库

6. 删除本地test分支和远程分支
删除本地分支
git checkout dev      # 先切换非test分支，才能删除
git pull
git branch -d test  或者 git branch –delete test

如果这个命令报错，往往是
一、很有可能是你正处于该分支上。
二、该分支包含了还未合并的工作，可以先合并或者使用 -D参数强制删除。这样写可以在不检查merge状态的情况下删除分支

删除远程分支，可以使用：
git push origin --delete test
也可以登录到Gitlab的网页上删除远程分支。


Some Questions
1. 如果本地dev有修改内容且没有提交，切换分支后，是否可以把这些修改内容带到新分支上
因为：git中存在工作区和暂存区，这两个区都是被所有本地分支共享的。
2，待补充：



二， git的版本控制 使用流程和常用命令：
    1，查看所有分支。
        git branch -a   

      2. 创建dev分支。
        在gitLab网页上以master分支为起点创建一个dev分支

        2.1 方法一：本地创建dev分支，并关联远程dev分支
            git checkout -b dev   #创建一个dev的本地分支。
            git branch --set-upstream-to=origin/dev  #关联上远程仓库的dev分支
        2.2 方法二：直接使用：
            git checkout -b test origin/test
            #创建本地test分支的同时又链接到远程的test分支上。

      3，切换到dev分支
        git checkout dev

      4，更新dev分支代码
        git pull

      5，在dev分支的基础上，检出新分支test
        git checkout -b test

      6，进行开发并提交你的代码
        git add -A
        git commit -m"xxxxxx"

      7，将本地test分支推送到远程
        git push -u origin test # 会创建一个远程test分支
        git push                #如果不是第一次推送，可以直接使用。

      8，合并分支
        git checkout dev  #检出到dev分支
        git pull          # 在合并前同样先pull一下dev
        git merge test    # 这里的合并是本地合并，将test中的内容合并到dev中
        git push          # 将本地内容推送到远程仓库


三， 项目分支定义：
      release分支：发布版本时候，把dev分支合并到release分支。
      master分支：线上实际运行版本。
      dev分支（目前是company分支）：每个人的开发分支，每天合并到此dev分支。
      每个人有个自己单独的分支：自己日常开发提交。
      
四， 提交规范  
   git commit -m"xxxxxx"， 
   提交内容"xxxxxx"，需要清楚明确提交的功能，和解决的bug，不能写的太简单或者不明确。



