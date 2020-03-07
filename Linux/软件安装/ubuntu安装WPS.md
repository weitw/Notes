ubuntu自带的office软件并不好用，现在我们可以安装WPS来替代office。

### 1. 卸载原有的office软件(可选)

这个看个人吧，反正以后都用WPS了，office不用了就卸载了。

卸载命令：`sudo apt remov libreoffice-common`

### 2. 下载WPS的包

去[这儿](https://www.wps.com/download/)下载，我下载的是wps-office_11.1.0.9126.XA_amd64.deb

### 3. 安装

进入wps-office_11.1.0.9126.XA_amd64.deb所在目录，执行命令：`sudo dpkg -i wps-office_11.1.0.9126.XA_amd64.deb`