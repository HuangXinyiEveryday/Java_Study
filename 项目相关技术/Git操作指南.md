Git操作指南

1.git公钥配置

想要本地推送到远程仓库或者克隆仓库，需要ssh密钥

**查看ssh**

```
查看电脑是否存在id_rsa.pub
cd ~/.ssh
如果不存在则会提示 No such file or directory，否则会自动进入目录 用ls就可以看到
ls
id_rsa  id_rsa.pub
```

**创建ssh**

```
ssh-keygen -t rsa -C "****"//***为注释文字
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa)://可以指定目录也可以不指定目录。直接回车
Enter passphrase (empty for no passphrase):
Enter same passphrase again://可以不输入密码，直接回车，以后每次push就不用输入密码
Your identification has been saved in /c/Users/user/.ssh/id_rsa.
Your public key has been saved in /c/Users/user/.ssh/id_rsa.pub.
The key fingerprint is:
这里是生成的key fingerprint
The key's randomart image is:
这里是生成的key's randomart image
此时创建ssh成功
```

**添加ssh到git**

```
找到文件id_rsa.pub文件，拷贝ssh
在git用户设置中，找到ssh密钥，添加即可
可以克隆或者push一个仓库测试是否成功
```

2.git常用命令

**创建版本库**

```markdown
git init
git add <file_name>
git commit -m "***"//说明修改内容
```

**仓库克隆**

```markdown
git clone <git上面SSH/HTTP地址 **.git>//默认是master分支
git clone -b <branch_name> <git上面SSH/HTTP地址 **.git>//克隆特定分支
```

**远程推送**

```markdown
git remote add origin <git上面SSH/HTTP地址 **.git>
git push -u origin <branch_name>
```

注释：我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

```markdown
git push origin <branch_name>
```

**删除远程分支**

```markdown
git push origin -d <branch_name>
```

**删除本地分支**

```markdown
git branch -D <branch_name>
```

**恢复本地被删除的分支**

```markdown
git branch <branch_name> <hash_val>
```

**查看本地分支和远程分支**

```
git branch//查看本地分支
git branch -a//查看远程仓库和本地所有分支
```

**创建分支**

```
$ git checkout -b <branch_name> //创建并切换到当前分支
等同于
$ git branch <branch_name>
$ git checkout <branch_name>
就可以在当前分支执行增加文件的工作
```

**切换当前分支**

```markdown
git checkout <branch_name>
```

**推送本地分支到远程分支**

```
//远程已有remote_branch分支并且已经关联本地分支local_branch且本地已经切换到local_branch
git push
//远程已有remote_branch分支但未关联本地分支local_branch且本地已经切换到local_branch
git push -u origin/remote_branch
//远程没有remote_branch分支并，本地已经切换到local_branch
git push origin local_branch:remote_branch
```

