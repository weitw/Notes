## ubuntu激活root

### 1. 问题描述

> 刚装好的ubuntu的root账户是没有被激活的，但是我们依然可以使用sudo来使用一些普通用户受限的命令，但是如果现在要切换到root账户怎么办呢？

### 2. 解决方案

> 使用命令：`sudo password root`，然后会提示你为root用户创建密码，确认密码，完成后root账号就被激活了，现在可以使用命令`su`或者`su root`来切换到root账号下。

