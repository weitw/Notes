> ## 安装QQ/TIM/微信
>
> 2019/10/24日，腾讯发布了Linux版的QQ了，虽然功能不是很多，界面也很简单，不过想必之后会慢慢优化的，QQ for Linux去[这儿](https://im.qq.com/linuxqq/index.html)下载
>
> 下面讲的内容是以前在wine环境下安装的QQ/微信
>
> ### 1. 安装TIM
>
> > - 第一步。安装deepin-wine环境。
>>
> > 在[https://github.com/wszqkzqk/deepin-wine-ubuntu](https://github.com/wszqkzqk/deepin-wine-ubuntu)中下载zip包，我使用的是Git clone到本地
> >
> > ![TIM下载](./img/TIM_donwnload.png)
> >
> > 如图，复制地址之后，使用命令：`git clone https://github.com/wszqkzqk/deepin-wine-ubuntu.git`，这样就会将该项目下载到本地
> >
> > - 第二步。安装相关应用容器
> >
> > 打开网址[http://mirrors.aliyun.com/deepin/pool/non-free/d/](http://mirrors.aliyun.com/deepin/pool/non-free/d/)，这里面有很多的容器可以下载，如果你找不到TIM对应的容器，你也可以直接打开下面的网址，然后下载deb文件就可以了。
> >
> > > - TIM：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.office/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.office/)
> > > - QQ：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im/)
> > > - QQ轻聊版：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im.light/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.qq.im.light/)
> > > - 微信：[http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/](http://mirrors.aliyun.com/deepin/pool/non-free/d/deepin.com.wechat/)
> > >
> > > ![TIM的deb包](./img/TIM_deb.png)
> 
> - 第三步。安装TIM
>
>   > 进入deb文件下载路径，然后执行命令：`sudo dpkg -i xxxxx.deb`就可以了。之后就可以在所有程序中找到TIM了。
>
> ### 2. 安装微信
>
> > ubuntu安装完成后，会有一个“微信ubuntu版”，这个我试过扫码后不能登录，所以还是自己重新装一个吧
>>
> > - 第一步。从上面给的链接中下载微信的deb包。
> > - 第二步。进入这个deb包所在的路径，执行命令：`sudo dpkg -i xxxxx.deb`，你也可以把这个包移动到其他目录，因为执行完这条命令之后，就会将软件安装到当前路径了。
> > - 但是我执行过程出错了，错误信息如下图
> >
> > ![命令安装出错](./img/wechatError.png)
> >
> > 这是什么原因呢？因为之前我的TIM也是安装到该目录下的，我进入TIM所在的路径，发现微信竟然安装好了。如下图
> >
> > ![微信和TIM在同一路径下](./img/runWechat.png)
> >
> > 注意在/opt/deepinwine/apps/下，TIM和微信都在，所以我才如果你安装QQ的话，也会是自动安装到该目录下的。那么到底有没有安装成功呢？我去所有程序里找一下
> >
> > ![微信安装成功了](./img/wechat.jpg)
> >
> > 双击打开扫码，登录成功。