### 2. Spring+SpringMVC+SpringJdbc应用

#### 2.1 创建工程，搭建SpringMVC和SpringJDBC技术环境

创建一个WEB工程，添加JDBC相关技术环境

引入数据库驱动包

引入DBCP连接池开发包

添加Spring相关技术环境

引入SpringIOC，web, webmvc, jdbc, tx开发包

在src下添加applicationContext.xml配置文件

在web.xml中配置DispatcherServlet主控制器

在web.xml中配置中文乱码过滤器CharacterEncodingFilter

#### 2.2 基于SpringJDBC实现DAO组件

根据数据表编写实体类

编写DAO组件

在Spring配置文件中配置JDBCTemplate组件

在DAO组件中注入JDBCTemplate对象

#### 2.3 编写和配置SpringMVC主要组件

编写Controller和请求处理方法

配置`<mvc:annotation-driven>`支持@RequestMapping

配置Controller

开启注解扫描，讲Controller组件扫描到容器中

需要DAO组件采用注入方式注入

在请求处理方法上使用@RequestMapping指定对应请求

配置ViewResoler

#### 2.4 编写JSP视图组件，利用JSTL标签和EL表达式显示数据







卷积神经网络（Convolutional Neural Network, CNN）是一种前馈神经网络，它的人工神经元可以响应一部分覆盖范围内的周围单元, 对于大型图像处理有出色表现。卷积神经网络由一个或多个卷积层和顶端的全连通层（对应经典的神经网络）组成，同时也包括关联权重和池化层（pooling layer）。这一结构使得卷积神经网络能够利用输入数据的二维结构。与其他深度学习结构相比，卷积神经网络在图像和语音识别方面能够给出更好的结果。这一模型也可以使用反向传播算法进行训练。相比较其他深度、前馈神经网络，卷积神经网络需要考量的参数更少，使之成为一种颇具吸引力的深度学习结构。

图像处理，根本上讲是基于一定假设条件下的信号重建。这个重建不是3-D结构重建，是指恢复信号的原始信息，比如去噪声。这本身是一个逆问题，所以没有约束或者假设条件是无解的，比如去噪最常见的假设就是高斯噪声。

图像去噪是指减少数字图像中噪声的过程。现实中的数字图像在数字化和传输过程中常受到成像设备与外部环境噪声干扰等影响，称为含噪图像或噪声图像。噪声是图象干扰的重要原因（噪声包括加性噪声、乘性噪声、量化噪声）。一幅图象在实际应用中可能存在各种各样的噪声,这些噪声可能在传输中产生,也可能在量化等处理中产生。

如今，已经有很多基于深度学习的模型应用于图像去噪，例如有BM3D、WNNM、MLP、CSF、DnCNN等。本课题主要是利用DnCNN模型来进行图像去噪。

DnCNN是2017年提出的用较深层的CNN网络（DnCNN）实现去噪模型，为了解决网络层数加深导致的梯度弥散效应，DnCNN并不对图像进行学习，而是以输出与噪声的l2范数为损失函数来训练网络。DnCNN网络可以视为一个残差学习的过程，这样可以较好的训练。在该网络中利用了BN层（Batch Normalization），实验表明BN层与残差学习共同使用可以提高模型的性能，DnCNN在不同噪声水平上训练，得到的结果要优于现在的最优结果，如BM3D等。



















































