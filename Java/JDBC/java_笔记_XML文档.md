## XML文档
XML:可扩展的标记语言
用途: xml独立于软硬件的信息传输工具,常用于简化数据存储和共享
### xml处理指令
​			指挥解析引擎如何解析xml文档内容
```xml
<?xml version="1.0" encoding="utf-8"?>
```
#### xml文档包含:
​			xml元素(标签):
​				1,从开始到结束的一组标签的部分,元素中可以包含其他元素,文本等
​				2,元素有属性,属性用来提供关于元素的额外信息
例如:
```xml
<dataSource>
<property name="user">root</property>
</dataSource>
```
#### 注意:
​		1,xml文档只有一个根元素
​		2,元素必须有开始标签和结束标签(都是双标记)
​		3,xml对大小写敏感(严格区分大小写)
​		4,xml属性值必须加引号
​		5,必须正确嵌套元素

### xml的解析方式:
#### 1)DOM解析:
​		Document Object Model即文档对象模型
​		在解析xml文档时,会将文档中的全部元素,按照元素出现的层次结构关系
​		解析成一个个对象节点
优点: 把xml文档在内存中解析形成一个属性结构,可以遍历和修改
缺点：若文档较大时,内存压力较大,解析时间较长
​	

#### 2)SAX解析
​		Simple APIs for XML 即简单应用程序接口
​		相比于DOM,SAX是一种速度快,更为有效的解析方式
​		SAX解析逐行扫描文件,一边扫描一边解析,可以在文档任意时刻停止解析
优点: 可以即可开始,速度快,内存压力小
缺点: 不能对节点进行修改	

#### 3)JDOM解析
​		 Java Document Object Model
 		特性: 
​			 1,仅使用具体类,而不是接口
​			 2,API大量使用了Collection类
#### 4)DOM4j解析
​		 特性:
​				开源的基于java的库来解析XML文档
​				具有性能好,灵活性好,功能强大,易使用等特点
​		 架包:
​				dom4j-full.jar;

##### 应用:

######    1,读取XML

```java
	//创建对象
	SAXReader reader=new SAXReader();
	//读XML文档
	Document document=reader.read(new File(""));
	//Document对象:表示文档树的根,提供对文档数据最初的访问入口
	//获取根元素
	Element root= document.getRootElement();
	//Element对象: XML文档中元素可以包含其他元素,属性,文本等内容
	//获取根元素下面的全部子元素
	List<Element> elements= root.elements();
	//获取当前元素的指定name的属性
	Attribute(返回类型)   attribute(String name);
	//Attribute对象: 用于描述一个元素中的属性信息
	//获取当前元素的属性值
	String(返回类型)  getValue();
	//获取当前元素的文本内容
	String(返回类型)  elementText(String name);
```
######   2,写入XML

```java
	//创建并返回Document对象
    Document document = DocumenHelper.createDocument();
	//添加根元素 并返回根元素(此方法只能调用一次即只能添加一个根元素)
	Element root= document.addElement("root");
	//在根元素下添加子元素
	Element p1=root.addElement("child");
	//给当前元素添加属性
	p1.addAttribute(String AttName,String value);
	//给当前元素添加文本内容
	p1.addText(String str);
	//写入XML文档(通过XMLWriter对象将内容输出生成XML文档)
	//创建输出流并生成XML文档
	XMLWriter writer=new XMLWriter();
	FileOutputStream fos = new FileOutputStream(new 			File("url"));
	writer.setOutputStream(fos);
	//将内容(document对象)写入XML文档
	writer.write(document);
	//关闭流
	writer.close();
```


​	

​	









