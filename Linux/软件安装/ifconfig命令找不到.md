## 提示ifconfig命令找不到

### 1. 问题描述

> 在终端输入ifconfig之后，还是显示找不到命令

### 2. 解决方案

> - 第一步。更新apt-get，使用命令：`sudo apt-get update`
> - 第二步。使用命令：`sudo apt-get install net-tools`下载net-tools。如果过程没有报错的话，输入命令`ifconfig`就没有问题了。