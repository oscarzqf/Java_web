# Servlet技术

###### a)什么是 Servlet 

- 1、Servlet 是 JavaEE 规范之一。规范就是接口 
- 2、Servlet 就 JavaWeb 三大组件之一。三大组件分别是：Servlet 程序、Filter 过滤器、Listener 监听器。 
- 3、Servlet 是运行在服务器上的一个 java 小程序，它可以接收客户端发送过来的请求，并响应数据给客户端

###### b)手动实现 Servlet 程序 

- 1、编写一个类去实现 Servlet 接口 

  如果实现报错，就到tomcat安装目录下的lib目录找到servlet-api.jar包添加

- 2、实现 service 方法，处理请求，并响应数据 

- 3、到 web.xml 中去配置 servlet 程序的访问地址

Servlet程序的示例代码：

```java
    public class HelloServlet implements Servlet {
         /**
     * service 方法是专门用来处理请求和响应的
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("hello1233646");
    }
    }
```

web.xml中的配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--servlet标签给Tomcat配置servlet程序-->
    <servlet>
        <!--servlet-name 标签给servlet程序起一个别名（一般为类名）-->
        <servlet-name>HelloServlet</servlet-name>
        <!--servlet-class是servlet程序的全类名-->
        <servlet-class>com.zqf.servelet.HelloServlet</servlet-class>
    </servlet>
    <!--servlet-mapping给servlet程序配置访问地址-->
    <servlet-mapping>
        <!--servlet-name标签作用是告诉服务器，当前配置的地址是给哪一个servlet程序-->
        <servlet-name>HelloServlet</servlet-name>
        <!--url-pattern标签配置访问地址
            / 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径
            /hello  表示地址为：http://ip:port/工程路径/hello
            也可以取其他名字,尽量与类名对应，路径下无需有文件，一定要
            有 / 否则报错
        -->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

常见错误：

- url-pattern中配置的路径没有以斜杠开头
- servlet-name配置的值不存在
- servlet-class标签的全类名配置错误

###### c)url 地址到 Servlet 程序的访问

![](D:\java\imagesrecord\QQ截图20211018165510.png)

###### d)Servlet 的生命周期

- 1、执行 Servlet 构造器方法 

- 2、执行 init 初始化方法 

  第一、二步，是在第一次访问的时候创建 Servlet 程序会调用。 

- 3、执行 service 方法

   第三步，每次访问都会调用。 

- 4、执行 destroy 销毁方法 

  第四步，在 web 工程停止的时候调用。

  

###### e)GET 和 POST 请求的分发处理

```java
public class HelloServlet implements Servlet {
         /**
     * service 方法是专门用来处理请求和响应的
     * @param servletRequest
     * @param servletResponse
     * @throws ServletException
     * @throws IOException
     */
    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
       //向下类型转换为子类（因为它有getMethod()方法,可以得到是post还是get）
        HttpServletRequest httpServletRequest=(HttpServletRequest)servletRequest;
        String method = httpServletRequest.getMethod();
        if("get".equals(method)){
            //避免代码不好维护，写成方法调用
            doGet();
        }else if("post".equals(method)){
            doPost();
        }
    }
    public void doGet(){
        System.out.println("get请求");
    };
    public void doPost(){
        System.out.println("post请求");
    };
    
    }
```

###### f) 通过继承 HttpServlet 实现 Servlet

一般在实际项目开发中，都是使用继承 HttpServlet 类的方式去实现 Servlet 程序。 

- 1、编写一个类去继承 HttpServlet 类 
- 2、根据业务需要重写 doGet 或 doPost 方法 
- 3、到 web.xml 中的配置

Servlet类的代码：

```java
public class HelloServletNext extends HttpServlet {
    /**
     * doGet()在get请求的时候调用
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我是get请求");
    }

    /**
     * doPost()在post请求的时候调用
     * @param req
     * @param resp
     * @throws ServletException
     * @throws IOException
     */
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我是post请求");
    }
}
```

web.xml中的配置：

```xml
 <!--使用继承HttpServlet类的方式去实现Servlet程序-->
    <servlet>
        <servlet-name>HelloServletNext</servlet-name>
        <servlet-class>com.zqf.servelet.HelloServletNext</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>HelloServletNext</servlet-name>
        <url-pattern>/hellonext</url-pattern>
    </servlet-mapping>
```



###### g)使用 IDEA 创建 Servlet 程序

![](D:\java\imagesrecord\QQ截图20211018230920.png)

没Servlet解决方案：

![](D:\java\imagesrecord\CSDN_1634569687520.jpg)

配置Servlet的信息：

![](D:\java\imagesrecord\QQ截图20211018231821.png)

自动生成实现了HttpServlet接口的类，web.xml自动配置<servlet-name>,但是<servlet-mapping>需要手动添加。



###### h)Servlet 类的继承体系

![](D:\java\imagesrecord\QQ截图20211018232456.png)

# ServletConfig 类

ServletConfig 类从类名上来看，就知道是 Servlet 程序的配置信息类。

 Servlet 程序和 ServletConfig 对象都是由 Tomcat 负责创建，我们负责使用。 

Servlet 程序默认是第一次访问的时候创建，ServletConfig 是每个 Servlet 程序创建时，就创建一个对应的 ServletConfig 对象。



###### a)三大作用

- 1、可以获取 Servlet 程序的别名 servlet-name 的值 
- 2、获取初始化参数 init-param 
- 3、获取 ServletContext 对象

**web.xml配置**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--通过继承Servlet实现Servlet程序-->
    <!--servlet标签给Tomcat配置servlet程序-->
    <servlet>
        <!--servlet-name 标签给servlet程序起一个别名（一般为类名）-->
        <servlet-name>HelloServlet</servlet-name>
        <!--servlet-class是servlet程序的全类名-->
        <servlet-class>com.zqf.servelet.HelloServlet</servlet-class>
        
        //每个servlet程序只能获取自己的参数
        <!--init-param是初始化参数-->
        <init-param>
            <!--是参数名-->
            <param-name>username</param-name>
            <!--是参数值-->
            <param-value>root</param-value>
        </init-param>
        <init-param>
            <param-name>url</param-name>
            <param-value>jdbc:mysql://localhost:3306/test</param-value>
        </init-param>
        
        
        
    </servlet>
    
    
    <!--servlet-mapping给servlet程序配置访问地址-->
    <servlet-mapping>
        <!--servlet-name标签作用是告诉服务器，当前配置的地址是给哪一个servlet程序-->
        <servlet-name>HelloServlet</servlet-name>
        <!--url-pattern标签配置访问地址
            / 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径
            /hello  表示地址为：http://ip:port/工程路径/hello
            也可以取其他名字,尽量与类名对应，路径下无需有文件，一定要
            有 / 否则报错
        -->
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <!--使用继承HttpServlet类的方式去实现Servlet程序-->
    <servlet>
        <servlet-name>HelloServletNext</servlet-name>
        <servlet-class>com.zqf.servelet.HelloServletNext</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>HelloServletNext</servlet-name>
        <url-pattern>/hellonext</url-pattern>
    </servlet-mapping>
    <servlet>
        <servlet-name>HelloServlet3</servlet-name>
        <servlet-class>com.zqf.servelet.HelloServlet3</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>HelloServlet3</servlet-name>
        <url-pattern>/hello3</url-pattern>
    </servlet-mapping>
</web-app>
```

Servlet代码：

```java
 @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("init初始化方法");
        //1.可以获取Servlet程序的别名servlet-name值
        System.out.println("程序的别名是："+servletConfig.getServletName());
        //2.获取初始化参数 init-param
        System.out.println("username="+servletConfig.getInitParameter("username"));
        System.out.println("url="+servletConfig.getInitParameter("url"));
        //3.获取 ServletContext 对象
        System.out.println(servletConfig.getServletContext());
    }
```

在其他地方可以使用getServletConfig获取ServletConfig实例

注意点：

![](D:\java\imagesrecord\QQ截图20211020095140.png)





# ServletContext 

###### a)什么是 ServletContext

- 1、ServletContext 是一个接口，它表示 Servlet 上下文对象 
- 2、一个 web 工程，只有一个 ServletContext 对象实例。 
- 3、ServletContext 对象是一个域对象。 
- 4、ServletContext 是在 web 工程部署启动的时候创建。在 web工程停止的时候销毁。

**什么是域对象?** 

域对象，是可以像 Map 一样存取数据的对象，叫域对象。 这里的域指的是存取数据的操作范围，是整个 web 工程。

​						存数据 				取数据 					删除数据 

Map				 put() 					get() 						remove() 

域对象 		setAttribute() 		getAttribute() 		removeAttribute();

###### b)ServletContext 类的四个作用 

- 1、获取 web.xml 中配置的上下文参数 context-param
-  2、获取当前的工程路径，格式: /工程路径 
- 3、获取工程部署后在服务器硬盘上的绝对路径 
- 4、像 Map 一样存取数据

ServletContext代码：

```java
public class ContextServlet extends HttpServlet {
    @Override
    //默认调用get请求
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
       //获取serletContext对象
        //方式1
        ServletContext context = getServletConfig().getServletContext();
        //方式2
        ServletContext context1 = getServletContext();
        // 1、获取 web.xml 中配置的上下文参数 context-param
        String username = context.getInitParameter("username");
        System.out.println(username);
        String password = context.getInitParameter("password");
        System.out.println(password);
        //  2、获取当前的工程路径，格式: /工程路径
        String path = context.getContextPath();
        System.out.println(path);
        //3、获取工程部署后在服务器硬盘上的绝对路径
        //  / 斜杠在服务器解析的时候，表示地址为：http://ip:port/工程路径/
        //  映射到IDEA的web目录
        String realPath = context.getRealPath("/");
        System.out.println(realPath);
        System.out.println("web工程下css目录的绝对路径是："+context.getRealPath("/css"));
        //4、像 Map 一样存取数据,只要创建全局都可以访问
        //必须执行后才存在
        context1.setAttribute("key1","value1");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}

```

web.xml配置：

```xml
<!--context-param是上下文参数，属于整个web工程,可以配置多组-->
    <context-param>
        <param-name>username</param-name>
        <param-value>root</param-value>
    </context-param>
    <context-param>
        <param-name>password</param-name>
        <param-value>123</param-value>
    </context-param>
```



# HTTP 协议



##### a)什么是 HTTP 协议

什么是协议? 

​			协议是指双方，或多方，相互约定好，大家都需要遵守的规则，叫协议。 

​			所谓 HTTP 协议，就是指，客户端和服务器之间通信时，发送的数据，需要遵守的规则，			叫 HTTP 协议。 

​			HTTP 协议中的数据又叫报文。

##### b)请求的 HTTP 协议格式

- 客户端给服务器发送数据叫请求。 

- 服务器给客户端回传数据叫响应。 

- 请求又分为 GET 请求，和 POST 请求两种





###### **GET请求**

1、请求行 

(1) 请求的方式    GET 

(2) 请求的资源路径[+?+请求参数] 

(3) 请求的协议的版本号 HTTP/1.1

2、请求头

 key : value    组成 不同的键值对，表示不同的含义。

![](D:\java\imagesrecord\QQ截图20211022195641.png)



###### **POST请求**

1、请求行 

(1) 请求的方式 POST 

(2) 请求的资源路径[+?+请求参数] 

(3) 请求的协议的版本号 HTTP/1.1 

2、请求头 

key : value 不同的请求头，有不同的含义

空行 

3、请求体 ===>>> 就是发送给服务器的数据

![](D:\java\imagesrecord\QQ截图20211022202028.png)



###### **常用请求头的说明：**

- Accept: 表示客户端可以接收的数据类型 
- Accpet-Languege: 表示客户端可以接收的语言类型 
- User-Agent: 表示客户端浏览器的信息 
- Host： 表示请求时的服务器 ip 和端口



###### **哪些是 GET 请求，哪些是 POST 请求**

​      GET 请求有哪些：

-  1、form 标签 method=get 

- 2、a 标签 

- 3、link 标签引入 css 

- 4、Script 标签引入 js 文件 

- 5、img 标签引入图片 

- 6、iframe 引入 html 页面 

- 7、在浏览器地址栏中输入地址后敲回车 

  POST 请求有哪些： 

- 8、form 标签 method=post



##### c)响应的 HTTP 协议格式

1、响应行 

​		(1) 响应的协议和版本号 

​		(2) 响应状态码 

​		(3) 响应状态描述符 

2、响应头 

​		(1) key : value 		不同的响应头，有其不同含义 

空行 

3、响应体 	---->>>	 就是回传给客户端



![](D:\java\imagesrecord\QQ截图20211022205253.png)

##### d)常用的响应码说明

- 200 表示请求成功 
- 302 表示请求重定向
-  404 表示请求服务器已经收到了，但是你要的数据不存在（请求地址错误） 
- 500 表示服务器已经收到请求，但是服务器内部错误（代码错误）



##### e)MIME 类型说明

MIME 是 HTTP 协议中数据类型。

MIME 的英文全称是"Multipurpose Internet Mail Extensions" 多功能 Internet 邮件扩充服务。MIME 类型的格式是“大类型/小 类型”，并与某一种文件的扩展名相对应。



常见的 MIME 类型：

![](D:\java\imagesrecord\QQ截图20211022205923.png)

![](D:\java\imagesrecord\QQ截图20211022205938.png)



**谷歌浏览器如何查看HTTP 协议：**

![](D:\java\imagesrecord\QQ截图20211022210113.png)

**火狐浏览器如何查看 HTTP 协议**

![](D:\java\imagesrecord\QQ截图20211022210703.png)





# HttpServletRequest类

##### a)HttpServletRequest 类有什么作用

每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request 对象中。 然后传递到 service 方法（doGet 和 doPost）中给我们使用。我们可以通过 HttpServletRequest 对象，获取到所有请求的 信息。

##### b)HttpServletRequest 类的常用方法

- i. getRequestURI()				获取请求的资源路径 
- ii. getRequestURL() 	   获取请求的统一资源定位符（绝对路径） 
- iii. getRemoteHost()       获取客户端的 ip 地址 
- iv. getHeader()   		获取请求头 
- v. getParameter() 获取请求的参数 
- vi. getParameterValues() 获取请求的参数（多个值的时候使用）
-  vii. getMethod() 获取请求的方式 GET 或 POST 
- viii. setAttribute(key, value); 设置域数据 
- ix. getAttribute(key); 获取域数据 
- x. getRequestDispatcher() 获取请求转发对象

```java
public class RequestAPIServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //i. getRequestURI() 获取请求的资源路径(工程名/标签地址)
        System.out.println("uri---"+ request.getRequestURI());
        //ii. getRequestURL() 获取请求的统一资源定位符（绝对路径）
        System.out.println("url---"+request.getRequestURL());
        //iii. getRemoteHost() 获取客户端的 ip 地址
        /**
         * 在 IDEA 中，使用 localhost 访问时，得到的客户端 ip 地址是 ===>>> 127.0.0.1<br/>
         * 在 IDEA 中，使用 127.0.0.1 访问时，得到的客户端 ip 地址是 ===>>> 127.0.0.1<br/>
         * 在 IDEA 中，使用 真实 ip 访问时，得到的客户端 ip 地址是 ===>>> 真实的客户端 ip 地址<br/>
         */
        System.out.println("ip--"+request.getRemoteHost());
        //iv. getHeader() 获取请求头
        System.out.println("请求头"+request.getHeader("User-Agent"));
        //vii. getMethod() 获取请求的方式 GET 或 POS
        System.out.println(request.getMethod());
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}
```



##### c)如何获取请求参数

```JAVA
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取请求的参数
        //获取单个值
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        //获取多个值
        String[] hobbies = request.getParameterValues("hobby");
        System.out.println(username);
        System.out.println(password);
        for (String hobby : hobbies) {
            System.out.println(hobby);
        }
    }
```

表单

```xml
<form action="http://localhost:8080/tomcat_war_exploded/parameterServlet" method="get">
  用户名：<input type="text" name="username"><br/>
  密码：<input type="password" name="password"><br/>
  兴趣爱好：<input type="checkbox" name="hobby" value="cpp">C++
  <input type="checkbox" name="hobby" value="java">Java
  <input type="checkbox" name="hobby" value="js">JavaScript<br/>
  <input type="submit">
</form>
```

##### d)POST 请求的中文乱码解决

```java
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
// 设置请求体的字符集为 UTF-8，从而解决 post 请求的中文乱码问题
//也要在获取请求参数之前调用才有效，不能放下面
req.setCharacterEncoding("UTF-8");
System.out.println("-------------doPost------------");
// 获取请求参数
String username = req.getParameter("username");
String password = req.getParameter("password");
String[] hobby = req.getParameterValues("hobby");
System.out.println("用户名：" + username);
System.out.println("密码：" + password);
System.out.println("兴趣爱好：" + Arrays.asList(hobby));
}
```

doGet 请求的中文乱码解决：

```java
// 获取请求参数
String username = req.getParameter("username");
//1 先以 iso8859-1 进行编码
//2 再以 utf-8 进行解码
username = new String(username.getBytes("iso-8859-1"), "UTF-8");
```





##### e)请求的转发

什么是请求的转发? 

请求转发是指，服务器收到请求后，从一次资源跳转到另一个资源的操作叫请求转发。

![](D:\java\imagesrecord\QQ截图20211023094001.png)

servlet1代码：

```java
 @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取请求的参数查看
        String username = request.getParameter("username");
        System.out.println("在servlet1中查看材料："+username);
        //给材料盖章，并传递到servlet2去查看
        request.setAttribute("key1","盖章了");
        //问路：servlet2（柜台2）怎么走
        /**
         * 请求转发必须要以斜杠打头，/ 斜杠表示地址为：http://ip:port/工程名/ ,
         * 映射到 IDEA 代码的 web 目录
         * */
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/servlet2");
        //走向servlet2程序（柜台2）
        requestDispatcher.forward(request,response);
    }
```

servlet2代码：

```java
@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取请求的参数（办事的材料）查看
        String username = request.getParameter("username");
        System.out.println("servlet2查看材料："+username);
        //查看servlet1是否盖章
        Object key1 = request.getAttribute("key1");
        System.out.println("servlet2查看是否有章"+key1);
        //处理自己的事务
        System.out.println("servlet2处理自己业务");
    }
```

##### f) base 标签的作用

![](D:\java\imagesrecord\QQ截图20211023103908.png)

```html
<!DOCTYPE html>
<html lang="zh_CN">
<head>
<meta charset="UTF-8">
<title>Title</title>
    
<!--base 标签设置页面相对路径工作时参照的地址
href 属性就是参数的地址值,后面/不能省略
-->
<base href="http://localhost:8080/07_servlet/a/b/">
    
</head>
<body>
这是 a 下的 b 下的 c.html 页面<br/>
<a href="../../index.html">跳回首页</a><br/>
</body>
</html>
```

```java
@Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("跳转到了frowardC");
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/a/b/c.html");
        requestDispatcher.forward(request,response);
    }
```





##### g)Web 中的相对路径和绝对路径

在 javaWeb 中，路径分为相对路径和绝对路径两种：

相对路径是：

-  . 表示当前目录 

- .. 表示上一级目录 

- 资源名 表示当前目录/资源名

绝对路径：

​     http://ip:port/工程路径/资源路径

在实际开发中，路径都使用绝对路径，而不简单的使用相对路径。 

- 绝对路径 
- base+相对

##### h)web 中 / 斜杠的不同意义

在 web 中 / 斜杠 是一种绝对路径。

 /  斜杠 如果被浏览器解析，得到的地址是：http://ip:port/

```html
<a href="/">斜杠</a>
```

/  斜杠 如果被服务器解析，得到的地址是：http://ip:port/工程路径

```html
1、<url-pattern>/servlet1</url-pattern>
2、servletContext.getRealPath(“/”);
3、request.getRequestDispatcher(“/”);


特殊情况： response.sendRediect(“/”); 把斜杠发送给浏览器解析。得到 http://ip:port/
```



# HttpServletResponse 类

##### a)HttpServletResponse 类的作用

HttpServletResponse 类和 HttpServletRequest 类一样。每次请求进来，Tomcat 服务器都会创建一个 Response 对象传 递给 Servlet 程序去使用。HttpServletRequest 表示请求过来的信息，HttpServletResponse 表示所有响应的信息， 我们如果需要设置返回给客户端的信息，都可以通过 HttpServletResponse 对象来进行设置

##### b)两个输出流的说明

字节流 	getOutputStream(); 	 常用于下载（传递二进制数据） 

字符流 	 getWriter(); 				   常用于回传字符串（常用）

注意：两个流同时只能使用一个。 使用了字节流，就不能再使用字符流，

反之亦然，否则就会报错

![](D:\java\imagesrecord\QQ截图20211023110904.png)



##### c)如何往客户端回传数据

要求 ： 往客户端回传 字符串 数据。

```java
   @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        PrintWriter writer = response.getWriter();
        writer.write("response's content!!!");

    }
```

##### d)响应的乱码解决

解决响应中文乱码方案一（不推荐使用）

```java
resp.getCharacterEncoding();//默认字符集为ISO-8859-1不支持中文
// 设置服务器字符集为 UTF-8
resp.setCharacterEncoding("UTF-8");
// 通过响应头，设置浏览器也使用 UTF-8 字符集
resp.setHeader("Content-Type", "text/html; charset=UTF-8");
```

解决响应中文乱码方案二（推荐）：

```java
// 它会同时设置服务器和客户端都使用 UTF-8 字符集，还设置了响应头
// 此方法一定要在获取流对象之前调用才有效
resp.setContentType("text/html; charset=UTF-8");
```



##### e)请求重定向

请求重定向，是指客户端给服务器发请求，然后服务器告诉客户端说。我给你一些地址。你去新地址访问。叫请求 重定向（因为之前的地址可能已经被废弃）

![](D:\java\imagesrecord\QQ截图20211023112141.png)

说明：web-inf是受保护的资源，浏览器不能直接访问

请求重定向的第一种方案： 

// 设置响应状态码 302 ，表示重定向，（已搬迁） 

resp.setStatus(302); 

// 设置响应头，说明 新的地址在哪里 

resp.setHeader("Location", "http://localhost:8080/工程名/资源路径");



请求重定向的第二种方案（推荐使用）：

resp.sendRedirect("http://localhost:8080");



# 在进行前后端交互中遇到的问题

```java
//遇到的重要的问题

//1：在进行请求转发跳转页面时，如果无法跳转可能是前端js代码设置点击事件后返回 return false 导致表单无法执行提交
//解决方法去掉return 语句

报错：
java.lang.NullPointerException: inStream parameter is null

//2.junit测试数据库连接正确，而使用tomcat运行时报错java.lang.NullPointerException: inStream parameter is null
//原因：读取配置文件时使用的是系统类加载器改为当前类加载器时不报错正常连接。
//查阅资料发现
//
//ClassLoader.getSystemClassLoader方法无论何时均会返回ApplicationClassLoader,其只加载classpath下的class文件。
//
//在javaSE环境下，一般javaSE项目的classpath为bin/目录，因此只要编译后的class文件在classpath下就可以。
// 此时ApplicationClassLoader就可以加载动态生成的类。
//
//但在javaEE环境下，我们的项目里的类是通过WebAppClassLoader类来加载的，
// 此时我们获取了ApplicationClassLoader，因此自然找不到class文件。
    
    
3.HTTP Status 500 - Cannot forward after response has been committed
response不能在已经提交后跳转，把doPost中的"super.doPost()"删除.
OK!项目成功运行！
    
```
