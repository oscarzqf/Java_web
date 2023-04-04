# Tomcat

#### 1.JavaWeb的概念

- JavaWeb

JavaWeb 是指，所有通过 Java 语言编写可以通过浏览器访问的程序的总称，叫 JavaWeb。 JavaWeb 是基于请求和响应来开发的。

- 请求

  请求是指客户端给服务器发送数据，叫请求 Request。

- 响应

  响应是指服务器给客户端回传数据，叫响应 Response。

- 请求与响应的关系

  请求和响应是成对出现的，有请求就有响应

![](D:\java\imagesrecord\QQ截图20211005221308.png)



#### 2.Web资源的分类

web 资源按实现的技术和呈现的效果的不同，又分为静态资源和动态资源两种。

静态资源： html、css、js、txt、mp4 视频 , jpg 图片 

动态资源： jsp页面、Servlet程序



#### 3.常用的Web服务器

- Tomcat：由 Apache 组织提供的一种 Web 服务器，提供对 jsp 和 Servlet 的支持。它是一种轻量级的 javaWeb 容器（服务器），也是当前应用最广的 JavaWeb 服务器（免费）。
- Jboss：是一个遵从 JavaEE 规范的、开放源代码的、纯 Java 的 EJB 服务器，它支持所有的 JavaEE 规范（免费）。
- GlassFish： 由 Oracle 公司开发的一款 JavaWeb 服务器，是一款强健的商业服务器，达到产品级质量（应用很少）。
- Resin：是 CAUCHO 公司的产品，是一个非常流行的服务器，对 servlet 和 JSP 提供了良好的支持， 性能也比较优良，resin 自身采用 JAVA 语言开发（收费，应用比较多）
- WebLogic：是 Oracle 公司的产品，是目前应用最广泛的 Web 服务器，支持 JavaEE 规范， 而且不断的完善以适应新的开发要求，适合大型项目（收费，用的不多，适合大公司）。



#### 4.Tomat服务器和Servlet版本的对应关系

企业常用版本：7、8

![](D:\java\imagesrecord\QQ截图20211005221922.png)



Servlet 程序从 2.5 版本是现在世面使用最多的版本（xml 配置） 到了 Servlet3.0 之后。就是注解版本的 Servlet 使用



#### 5.Tomat的使用

###### a)安装

找到你需要用的 Tomcat 版本对应的 zip 压缩包，解压到需要安装的目录即可

###### b)目录介绍

- bin 专门用来存放 Tomcat 服务器的可执行程序 
- conf 专门用来存放 Tocmat 服务器的配置文件 
- lib 专门用来存放 Tomcat 服务器的 jar 包 
- logs 专门用来存放 Tomcat 服务器运行时输出的日记信息 
- temp 专门用来存放 Tomcdat 运行时产生的临时数据 
- webapps 专门用来存放部署的 Web 工程。 
- work 是 Tomcat 工作时的目录，用来存放 Tomcat 运行时 jsp 翻译为 Servlet 的源码，和 Session 钝化的目录。

###### c)启动1

找到 Tomcat 目录下的 bin 目录下的 startup.bat 文件，双击，就可以启动 Tomcat 服务器。

如何测试 Tomcat 服务器启动成功？？？

-  打开浏览器，在浏览器地址栏中输入以下地址测试：
- 1、http://localhost:8080 
- 2、http://127.0.0.1:8080 
- 3、http://真实 ip:8080 当出现如下界面，说明 Tomcat 服务器启动成功！！！

<img src="D:\java\imagesrecord\QQ截图20211005223211.png" style="zoom:50%;" />



常见的启动失败的情况有，双击 startup.bat 文件，就会出现一个小黑窗口一闪而来。 这个时候，失败的原因基本上都是因为没有配置好 JAVA_HOME 环境变量

常见的 JAVA_HOME 配置错误有以下几种情况： 

- JAVA_HOME 必须全大写。 
- JAVA_HOME 中间必须是下划线，不是减号- 
- JAVA_HOME 配置的路径只需要配置到 jdk 的安装目录即可。不需要带上 bin 目录。

###### c)启动2

- 打开命令行 

- cd 到 你的 Tomcat 的 bin 目录

  ![](D:\java\imagesrecord\QQ截图20211005225456.png)

​         好处：发生错误可以看到错误信息                                               

###### d)Tomcat的停止

- 1、点击 tomcat 服务器窗口的 x 关闭按钮 
- 2、把 Tomcat 服务器窗口置为当前窗口，然后按快捷键 Ctrl+C 
- 3、找到 Tomcat 的 bin 目录下的 shutdown.bat 双击，就可以停止 Tomcat 服务



###### e)如何修改Tomcat的端口号

Mysql 默认的端口号是：3306 

Tomcat 默认的端口号是：8080

找到 Tomcat 目录下的 conf 目录，找到server.xml 配置文件

<img src="D:\java\imagesrecord\QQ截图20211005230459.png" style="zoom:50%;" />



平时上百度：http://www.baidu.com:80 

HTTP 协议默认的端口号是：80   不写也一样



###### f)如何部署web工程到Tomcat中

第一种部署方法：只需要把 web 工程的目录拷贝到 Tomcat 的 webapps 目录下 即可

只需要在浏览器中输入访问地址格式如下： http://ip:port/工程名/目录下/文件名即可访问

第二种方法：

找到 Tomcat 下的 conf 目录\Catalina\localhost\ 下,创建如下的配置文件：



abc.xml配置文件内容如下

```xml
<!-- Context 表示一个工程上下文
path 表示工程的访问路径:/abc（不同名字表示不同工程的xml）
docBase 表示你的工程目录在哪里
-->
<Context path="/abc" docBase="E:\book" />
```

访问这个工程的路径如下:http://ip:port/abc/ 就表示访问 E:\book 



###### g)拖动 html 页面到浏览器和在浏览器中输入 http://ip:端 口号/工程名/访问的区别

拖动：使用的协议是file://协议。告诉浏览器直接读取file://协议后面的路径，解析展示在浏览器上

输入访问地址访问：使用的是http协议，原理完全不同

![](D:\java\imagesrecord\QQ截图20211010104953.png)



###### h)ROOT 的工程的访问，以及 默认 index.html 页面的访问

当我们在浏览器地址栏中输入访问地址如下： http://ip:port/ ====>>>> 没有工程名的时候，默认访问的是 ROOT 工程

当我们在浏览器地址栏中输入的访问地址如下： http://ip:port/工程名/ ====>>>> 没有资源名，默认访问 index.html 页面



#### 6.IDEA整合Tomcat服务器

操作的菜单如下：File | Settings | Build, Execution, Deployment | Application Servers

点击+添加然后找到安装路径

<img src="D:\java\imagesrecord\20211010110717.png" style="zoom:50%;" />



#### 7.IDEA 中动态 web 工程的操作

###### a)IDEA如何创建动态web工程

- 创建一个新模块(java)
- 右键模块-添加框架支持
- javaEE8,webapplication

动态web工程成功：在创建的moudle下

![](D:\java\imagesrecord\QQ截图20211010113438.png)



###### b)web工程的目录介绍

![](D:\java\imagesrecord\QQ截图20211010113958.png)



###### c)给动态web工程添加额外jar包

方式一：复制到lib目录下，再右键添加

方式二：

- 打开项目结构菜单界面，添加一个 自己的类库
- libraries--+--Java
- 添加类库需要的jar包
- 选择你添加的类库，给哪个模块使用
- 选择 Artifacts 选项，将类库，添加到打包部署中
- <img src="D:\java\imagesrecord\QQ截图20211010120647.png" style="zoom:80%;" />



###### d)如何在IDEA中部署工程到Tomcat上运行

- 修改web工程对应的Tomcat运行实例名称

![](D:\java\imagesrecord\QQ截图20211010121850.png)

- 确认你的Tomcat实例中有你要部署运行的web工程模块

![](D:\java\imagesrecord\QQ截图20211010122053.png)

- 你还可以修改你的 Tomcat 实例启动后默认的访问地址

![](D:\java\imagesrecord\QQ截图20211010122146.png)

- 4、在IDEA中如何运行和停止Tomcat实例

  ![](D:\java\imagesrecord\QQ截图20211010122449.png)

![](D:\java\imagesrecord\QQ截图20211010122525.png)

![](D:\java\imagesrecord\QQ截图20211010130650.png)



###### e）修改工程访问路径

![](D:\java\imagesrecord\QQ截图20211010130947.png)



###### f)修改运行时的端口号

![](D:\java\imagesrecord\QQ截图20211010131122.png)



###### g)修改运行使用的浏览器

![](D:\java\imagesrecord\QQ截图20211010131203.png)



###### h)配置资源热部署（不重启，刷新页面就可以看见修改）

![](D:\java\imagesrecord\QQ截图20211010131418.png)









































