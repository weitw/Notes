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



### 2. RandomAccessFile类
#### 2.1 可以用来修改或者操作文件的内容

+ 以byte(字节,8个bit位)为单位处理文件
+ 使用文件指针(下标)读写文件内容,一次读写一个byte
+ 当读写文件内容的时候,文件指针自动加1,为了方便下次的读写操作
+ 为了方便读写基本类型的数据,提供了基本数据类型的读写方法,底层就是以byte为单位进行读写操作的

#### 2.2 RandomAccessFile的常用方法:

+ 构造器
  打开的文件,状态"r"/"rw"(创建该类对象时,会自动的打开该文件,文件有两种状态),如果是写的时候,文件不存在就自动的创建文件,打开文件的时候,默认文件的指针位置为0,如果打开已经存在的文件,立即写,就是对文件的覆盖操作,如果将文件指针调到length()处,就是追加写操作
+ read()  write()
  read()是读取一个byte字节(读取到的结果填充到低8位)
  write()是写出一个byte字节(写出数据的低8位)
+ seek()移动文件的读写指针
+ close()文件读写操作结束后都要关闭文件
+ length()返回文件的长度(字节量)

### 3. Java IO流(Input/Output stream)
#### 3.1 流根据功能划分:输入流和输出流
输入流:用于读取数据
输出流:用于写出数据
输入输出流的参照对象时基于我们程序而言的

#### 3.2 流根据处理单位划分:字节流和字符流
字节流:以字节为单位读写数据
字符流:以字符为单位读写数据

#### 3.3 流根据级别划分为:高级流和低级流
高级流:不能独立的存在,必须基于另外一个流工作
低级流:数据有明确的来源或者去向

#### 3.4 字节输入输出流的父类:
InputStream:字节输入流的父类
OutputStream:字节输出流的父类
以上两个流都是抽象类,不能直接实例化

#### 3.5 FIS和FOS:用于读写文件的流
FileInputStream:文件字节输入流
FileOutputStream:文件字节输出流

#### 3.6 BIS和BOS:这两个是高级流
BufferedInputStream:缓存字节输入流
BufferedOutputStream:缓存字节输出流
高级流:会带来一些额外的功能,通常用于简化我们的读写操作

#### 3.7 DIS和DOS:这两个也是高级流
DataInputStream:可以方便读取基本类型数据的流
DataOutputStream:可以方便写出基本类型数据的流

#### 3.8 字符流:Reader和Writer
Reader:所有字符输入流的父类
Writer:所有字符输出流的父类
字符流处理单位为字符,一次处理一个字符,字符流的底层本质上还是用的读写字节

#### 3.9 ISR和OSW
InputStreamReader:字符输入流
OutputStreamWriter:字符输出流

#### 3.10 BR和BW

可以按行读写字符串。

BufferedRreader：缓存字符输入流

`String readLine()`

BufferedWriter：缓存字符输出流

`bw.newLine();  // 换行`



Reader(abstract)

BufferedReader, InputStreamRreader

Writer(abstract)

BufferedWriter, InputStreamWriter



InputStream(abstract)

FileInputStream, FiterInputStream

OutputStream(abstract)

FileOutputStream, FilterOutputStream

#### 3.11 字符流

直接读写文本文件的字符流。FW和FR就默认许可使用当前系统默认的字符集进行读写

FileWriter

FileReader

#### 3.12 带自动行刷新的缓冲字符输出流

PrintWriter

+ 构造器
  + PrintWriter(File file)
  + PrintWriter(String filename)
  + PrintWriter(OutputStream out)
  + PrintWriter(Writer writer)

### 4. 各种流之间的关系

```java
InputStream
    FileInputStream
    FilterInputStream
    
```

### 5. 序列化和反序列化的流

数据->字节序列：对象的序列化，一般对应文件操作的写操作，通常序列化对象时用于保存对象和传输对象

ObjectInputStream（对象的反序列化流）：

ObjectOutputStream（对象的序列化流）：























