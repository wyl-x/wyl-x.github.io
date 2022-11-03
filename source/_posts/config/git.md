---
title: Git分享
date: 2017/9/10 21:11:56
tags: Config
categories: Config
---

## git
* 版本控制
    * 集中式版本控制
       * 需要联网
       * 数据不安全
       * subversion SVN
    * 分布式版本控制
        * 不用联网
        * 安全
        * 分支管理
 
#### 配置   
ssh-keygen -t rsa

$ git config --global user.name "Your Name" 

$ git config --global user.email "email@example.com"

---
## rebase
## cherrypick

```
    git push origin wyl:develop
```

```
    git checkout -b wyl origin/wyl
    
    # 合并两个提交，可以按照下面过程
    git rebase -i HEAD~2
    
```

### 删除远程文件夹
方法一
这里以删除 test文件夹为案例
```
git rm -r --cached test //--cached不会把本地的test删除
git commit -m 'delete test dir'
git push -u origin master
```

方法二
如果误提交的文件夹比较多，方法一也较繁琐
直接修改.gitignore文件,将不需要的文件过滤掉，然后执行命令:

```
git rm -r --cached .
git add .
git commit
git push  -u origin master
```
