1. 在github上创建一个项目：

2. 在本地创建一个文件夹

3. 将githbub克隆下来，然后进入git bash

1. 查看有哪些分支：

    git branch
    
2. 删除哪些分支：

    git branch -D (分支名)
    
3. 创建分支（切换分支就没有-b）:

    git checkout -b (分支名)
    
4. 查看分支状态

    git status
    
5. 写描述内容

    vim README.md

6. 添加修改的数据到缓存区

    git add .
    
    git add 修改的文件名

7. 提交修改到本地分支

    git commit -m '注解'
    
8. 提交本地分支到远程分支上：

    git push origin 文件名
    
9. 设置全局变量：

    git config --global user.email "邮箱"
    
    git config --global user.name "用户名"
    
10. 创建秘钥：

    ssh-keygen -t rsa -C 账号
    
11. 比较两个分支之间的不同：

    git diff 分支1 分支2
    
12. 合并:

    git merge 分支
    
13. 打tag标签：

    git tag -a 版本号 -m 注解
    
14. 推送版本：

    git push origin 版本号
    
15. 删除远程分支：

    git push origin --delete 分支
    
16. 查看tag号

    git tag

