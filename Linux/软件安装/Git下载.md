## Git下载

### 1. Git的安装

> - 第一步。执行命令`sudo apt-get update`。
> - 第二步。执行命令`sudo apt-get install git`

### 2. Git的使用

> - 第一步。执行两条命令
>
> > sudo config --global user.name "your github username"
> >
> > sudo config --global user.email "email"
>
> - 第二步。执行命令`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE`，得到密钥和公钥。
> - 第三步。复制~/.ssh/id_rsa.pub中的内容，然后在你github设置中添加.
>
> ![添加](/home/exile/project/Notes/Linux/软件安装/img/SSHkeys.png)
>
> 如图，点击右上角的**New SSH key**，然后将复制的公钥内容粘贴进去即可。之后就可以按照Git常规的用法去用了。