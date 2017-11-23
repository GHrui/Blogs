---
title: Link To Remote Depository
date: 2017-08-16
tags: [Git, GitHub]
category: [Git]
description: 连接远程仓库
---
Link Local Depository(Git) To Remote Depository(Github)
<!--more-->
## 一、检查电脑是否配有SSH密匙
打开Git Bash，输入以下命令尝试进入该路径
```
$ cd  ~/.ssh
```
如果提示：No such file or directory，则说明电脑中没有配置SSH密匙
相反则有，这时输入以下命令，查看.ssh文件下的文件
```
$ ls
```
然后输入以下命令删除该路径下所有文件
```
$ rm *
```
备注：你也可以这些已有的SSH密匙，但是不建议，因为SSH密匙的使用牵扯到服务器地址，密码等。
ssh登录过的服务器的RSA公钥保存在.ssh/known_hosts中，由于更换了服务器，使用了相同IP，这会导致公钥与服务器的私钥配对失败，无法登陆服务器。这时候需要删除旧服务器(192.168.1.254)的公钥才行
## 二、生成SSH密匙
打开Git Bash，输入以下命令,然后根据提示选择密匙存放位置，设置密码
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
然后你就可以打开密匙所在的文件夹，在该文件夹中有id_rsa和id_rsa.pub两个文件，这两个就是SSHKey的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
## 三、以GitHub为例
具体流程如下
打开id_rsa.pub，复制里面所有内容->登陆GitHub->Personal settings->SSH and GPG keys->new SSH key->Title自己定义，Key的方框内黏贴id_rsa.pub里面所有内容。
完成后，测试一下链接情况，输入以下代码
```
$ ssh -T git@github.com
```
第一次连接远程库，它会提示
```
The authenticity of host 'github.com (192.30.252.129)' can't be established.
RSA key fingerprint is xxx.
Are you sure you want to continue connecting (yes/no)?
//译文：服务器‘github.com (192.30.252.129)’还没建立连接。密匙是xxxx。你是否想要连接
//解释：这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器
```
输入'yes',接着提示
```
Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.
```
然后在.ssh文件夹中会生成一个known_hosts文件，该文件记录服务器地址和密匙
## 四、将本地仓库与远程仓库建立连接
要关联一个远程库，使用命令
```
git remote add origin git@server-name:path/repo-name.git
```
在Git Bash窗口，利用cd命令跳转到项目路径下，如：
```
$ cd  C:/Projection
```
然后输入
```
$ git remote add origin git@github.com:githubusername(github用户名)/repertoryname(仓库名).git  
/*
origin为远程库的名字，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。repertoryname(仓库名)是github的叫法。一旦使用上面的命令，origin和repertoryname都指向相同的仓库。
*/
//"git@xxx/xxx"为ssh地址
```
SSH地址，在GitHub仓库界面的Clone or Download按钮弹出的界面，一般来说
```
git@github.com:githubusername(github用户名)/repertoryname(仓库名).git
```
## 五、将本地仓库所有内容推送到远程仓库建立
命令
```
$ git push -u origin master
```
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

如果远程库拥有本地库没有的文件，则会出现以下提示
```
To git@github.com:xxx/xxx.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:xxx/xxx.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
解决方法,先把远程库的文件合并到本地库，在执行
```
$ git pull --rebase origin master //从远程库master分支合并到本地库
$ git push -u origin master
```