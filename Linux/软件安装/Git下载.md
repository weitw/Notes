## Git下载

### 1. Git的安装

> - 第一步。执行命令`sudo apt-get update`。
> - 第二步。执行命令`sudo apt-get install git`

### 2. 配置git

输入`ssh-keygen –t rsa –C "邮箱地址"`，之后会让你输入秘钥保存路径，直接回车，它会默认让在当前用户目录下(~/.ssh/)。然后会让你输入密码，也可以直接回车，表示不设置。将~/.ssh/id_rsa.pub里面的内容复制，添加进github的ssh key中即可。

### 3. 验证

在git bash输入命令 `ssh -T git@github.com`，第一次配置会让你输入yes/no，输入yes。

### 4. 配置用户名和邮箱

```git
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

更详细的可以参考：[https://zhuanlan.zhihu.com/p/23167699](https://zhuanlan.zhihu.com/p/23167699)