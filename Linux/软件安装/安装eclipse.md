## 安装eclipse

1. 安装JDK

   `sudo apt install openjdk-8-jdk`，JDK版本自行选择，命令执行完，执行`java -version`，出现了java的信息的话就说明成功安装了。
   
2. 下载eclipse [下载链接](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/),

2. 将下载的xxxxx.tar.gz文件移动到/opt

   `sudo mv xxxx.tar.gz /opt`

3. 安装

   `sudo tar -zxvf xxxx.tar.gz`

   等待安装完成后就可以打开了

4. 配置编码

   这个看个人吧，如果你已经有的项目就和现在eclipse的编码格式一样，那就不用改了，这个判定的最简单的方法就是看你项目中的中文是不是乱码。

   如果要修改的话，途径是Window->preferences->General->Workspace，右边显示的就有修改编码的选项。

   **注意：可能修改编码的下拉框没有GBK或者其他的一些编码，你直接在输入框中输入你要的编码也可以*

5. 查看源码

   对于开发人员来说，查看源码是必须要的。如果你要查看某个类或者方法，使用Ctrl+鼠标左击，弹不出源码的话，那就需要配置一下。

   > 1. 配置JRES
   >
   > 依次点击Window->preferences->Java->Install JRES，在右边弹出来的窗口中，如果显示的有你的JDK安装路径，那么就不用管。否则要点击右边的Add，将JDK路径导进去(我的在/usr/lib/jvm/java-8-openjdk-amd64)
   >
   > 2. 加载源码src.zip
   >
   > 在你要查看源码所弹出来的界面中，根据提示点击进入，然后需要将你的src.zip文件路径add进去。但是在我选择好文件之后，居然报错
   >
   > `the path 'usr/lib/jvm/java-8-openjdk-amd64/src.zip' does not exist`
   >
   > 3. 解决办法
   >
   >    然后我看了一下，这个文件是一个失效的链接文件，所以我们可以重新下载一个。使用命令
   >
   > `sudo apt install openjdk-8-source `来下载(这个地方根据你的jdk版本来下载相应的源码文件)，等执行完之后，这个src.zip会自动去替换之前的那么无效的文件。这时再尝试add就可以了。
   >
   > 可以参考这个连接[解决src.zip does not exist的问题](https://askubuntu.com/questions/755853/how-to-install-jdk-sources)