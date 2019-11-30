## IO流(Input/Output stream)

在变量、数组和对象中存储的数据是暂时的，程序结束之后，他们就会丢失。为了能够永久的保存程序里面创建的数据，需要将其保存在磁盘的文件当中。这样就可以在其他程序中使用这些数据。Java的I/O技术可以将数据保存到文本文件、二进制文件或者ZIP压缩文件中。

### 1. File类

该类用于文件或者目录，其实例是用于描述文件系统的一个文件或者目录的，程序员通过file类在程序中可以操作硬盘上的文件或者目录。

注意

file类只能用于表达文件的信息（文件名、大小、格式等），不能对文件的内容进行访问，表示文件系统对文件、目录的管理操作（增删改查）。

#### 1.1 常用的方法

|             方法              |                             描述                             |
| :---------------------------: | :----------------------------------------------------------: |
|     File(String fileName)     |                      指定文件名的构造器                      |
| File(File dir, File fileName) |                  以目录和文件名创建File对象                  |
|         long length()         |                   获取文件的长度（字节量）                   |
|      long lastModified()      |                  获取文件最后一次修改的时间                  |
|       String getName()        |                          获取文件名                          |
|       String getPath()        |                      获取文件的相对路径                      |
|       boolean exists()        |                     判断当前文件是否存在                     |
|       boolean isFile()        |                      判断file是否是文件                      |
|     boolean isDirectory()     |                      判断dir是否为目录                       |
|       boolean canRead()       |                       判断文件是否可读                       |
|      boolean canWrite()       |                       判断文件是否可写                       |
|        boolean mkdir()        |                           创建目录                           |
|       boolean mkdirs()        |                        递归的创建目录                        |
|    boolean createNewFile()    |                   创建file对象所描述的文件                   |
|       getAbsolutePath()       | 获取绝对路径（这个方法会在项目之后多一个**.**），建议用下面这个方法 |
|      getCanonicalPath()       |                    获取系统标准的绝对路径                    |
|        String[] list()        |              返回当前File对象下所有的子项的名字              |
|      File[] listFiles()       |             返回当前File对象下所有子项的File对象             |

#### 1.2 总结

+ File类代表文件或文件夹
+ 可以实现文件系统的操作，没有提供递归处理（mkdirs()除外）
+ new File() 不是创建文件夹、文件，仅仅是创建内存对象，是描述一个文件或者目录的
+ File类不能操作文件里的内容

文件：一个byte有序序列





























