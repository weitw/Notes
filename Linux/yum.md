### yum命令
1. **描述**: yum(Yello dog Updater, Modified)是一个在Fedora和RedHat以及SUSE中的shell前端软件包管理器。基于RPM包管理，能够从指定的服务器自动下载RPM包并安装，可以自动处理依赖性关系，并且一次性安装所有的依赖的软件包。
2. yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，
3. yum语法：`yum [options] [command] [package ....]`
   - options: 可选，选项包括-h(帮助),-y(当安装过程提示选择全部为"y"), q(不显示安装过程)等
   - command: 要进行的操作
   - package: 要操作的对象

### yum常用命令
1. `yum check-update`: 列出所有可更新的软件清单
2. `yum update`: 更新所有软件
3. `yum install <package_name>`: 仅安装指定的软件
4. `yum update <package_name>`: 仅更新指定的软件
5. `yum list`: 列出所有可安装的软件清单
6. `yum remove <package_name>`: 删除软件包
7. `yum search <keyword>`: 查找软件包
8. 清除缓存命令
   > 1. `yum clean packages`: 清除缓存目录下的软件包
   > 2. `yum clean headers`: 清除缓存目录下的headers
   > 3. `yum clean oldheaders`: 清除缓存目录下旧的headers
   > 4. `yum clean, yum clean all`
9. 例如
![yum list *mysql](yum_list_mysql.png "yum list *mysql示例")

### 国内yum源
1. 网易（163）yum源是国内最好的yum源之一 ，无论是速度还是软件版本，都非常的不错。
将yum源设置为163 yum，可以提升软件包安装和更新的速度，同时避免一些常见软件版本无法找到。
2. 具体安装方法百度。
