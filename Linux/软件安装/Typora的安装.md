## Typora的安装

1. 这种方法（不建议）在`sudo update`时会出现警告:`W: 冲突的发行版：https://typora.io ./linux/ InRelease (期望 ./linux/ 但得到 )`

   - `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE`
   - `sudo add-apt-repository 'deb https://typora.io linux/'`
   - `sudo apt-get update`
   - `sudo apt-get install typora`

2. 后来自己去typora官网（建议）看了，人家已经把安装方法告诉我们了。官方的安装方法如图。

   ![ypora官网安装教程](./img/typora官网安装教程.png)