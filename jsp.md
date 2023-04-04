# JSP

#### 1.什么是 jsp，它有什么用?

jsp 的是 java server pages。Java 的服务器页面。

jsp 的主要作用是代替 Servlet 程序回传 html 页面的数据

因为 Servlet 程序回传 html 页面数据是一件非常繁锁的事情。开发成本和维护成本都极高。



servlet回传html页面数据的代码

```java
public class PrintHtml extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //通过响应的输出流回传html页面
        resp.setContentType("text/html; charset=UTF-8");
        PrintWriter writer = resp.getWriter();
        writer.write("<!DOCTYPE html>\r\n");
        writer.write("<html lang=\"en\">\r\n");
        writer.write("<head>\r\n");
        writer.write("<meta charset=\"UTF-8\">\r\n");
        writer.write("<title>tttt</title>\r\n");
        writer.write("</head>\r\n");
        writer.write("<body>\r\n");
        writer.write("这是HTML数据\r\n");
        writer.write("</body>\r\n");
        writer.write("</html>\r\n");
    }
}
```

#### 2.如何创建jsp页面

![](D:\java\imagesrecord\jsp1.png)

![](D:\java\imagesrecord\jsp2.png)

#### 3.jsp如何访问

jsp 页面和 html 页面一样，都是存放在 web 目录下。访问也跟访问 html 页面一样

比如： 在 web 目录下有如下的文件： 

web 目录 

- a.html 页面 访问地址是 =======>>>>>> http://ip:port/工程路径/a.html 

- b.jsp 页面 访问地址是 =======>>>>>> http://ip:port/工程路径/b.jsp



#### 4.jsp的本质

jsp 页面本质上是一个 Servlet 程序。

当我们第一次访问 jsp 页面的时候。Tomcat 服务器会帮我们把 jsp 页面翻译成为一个 java 源文件。并且对它进行编译成 为.class 字节码程序。我们打开 java 源文件不难发现其里面的内容是：

![](D:\java\imagesrecord\jsp3.png)

我们跟踪原代码发现，HttpJspBase 类。它直接地继承了 HttpServlet 类。也就是说。jsp 翻译出来的 java 类，它间接了继 承了 HttpServlet 类。也就是说，翻译出来的是一个 Servlet

![](D:\java\imagesrecord\jsp4.png)

总结：通过翻译的 java 源代码我们就可以得到结果：jsp 就是 Servlet 程序。

 大家也可以去观察翻译出来的 Servlet 程序的源代码，不难发现。其底层实现，也是通过输出流。把 html 页面数据回传 给客户端。

```java
public void _jspService(final javax.servlet.http.HttpServletRequest request, final
javax.servlet.http.HttpServletResponse response)
throws java.io.IOException, javax.servlet.ServletException {
final java.lang.String _jspx_method = request.getMethod();
if (!"GET".equals(_jspx_method) && !"POST".equals(_jspx_method) && !"HEAD".equals(_jspx_method)
&& !javax.servlet.DispatcherType.ERROR.equals(request.getDispatcherType())) 
    response.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, "JSPs only permit GET POST or
HEAD");
return;
}
final javax.servlet.jsp.PageContext pageContext;
javax.servlet.http.HttpSession session = null;
final javax.servlet.ServletContext application;
final javax.servlet.ServletConfig config;
javax.servlet.jsp.JspWriter out = null;
final java.lang.Object page = this;
javax.servlet.jsp.JspWriter _jspx_out = null;
javax.servlet.jsp.PageContext _jspx_page_context = null;
try {
response.setContentType("text/html;charset=UTF-8");
pageContext = _jspxFactory.getPageContext(this, request, response,
null, true, 8192, true);
_jspx_page_context = pageContext;
application = pageContext.getServletContext();
config = pageContext.getServletConfig();
session = pageContext.getSession();
out = pageContext.getOut();
_jspx_out = out;
out.write("\r\n");
out.write("\r\n");
out.write("<html>\r\n");
out.write("<head>\r\n");
out.write(" <title>Title</title>\r\n");
out.write("</head>\r\n");
out.write("<body>\r\n");
out.write(" a.jsp 页面\r\n");
out.write("</body>\r\n");
out.write("</html>\r\n");
} catch (java.lang.Throwable t) {
if (!(t instanceof javax.servlet.jsp.SkipPageException)){
out = _jspx_out;
if (out != null && out.getBufferSize() != 0)
try {
if (response.isCommitted()) {
out.flush();
} else {
out.clearBuffer();
}
} catch (java.io.IOException e) {}
if (_jspx_page_context != null) _jspx_page_context.handlePageException(t);
else throw new ServletException(t);
}
} finally {
_jspxFactory.releasePageContext(_jspx_page_context);
}
}
```

#### 5.jsp的三种语法

###### a)jsp头部的page指令

jsp 的 page 指令可以修改jsp 页面中一些重要的属性，或者行为

```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```

- language 属性 表示 jsp 翻译后是什么语言文件。暂时只支持 java。

- contentType 属性 表示 jsp 返回的数据类型是什么。也是源码中 response.setContentType()参数

- pageEncoding 属性 表示当前 jsp 页面文件本身的字符集。

- import 属性 跟 java 源代码中一样。用于导包，导类。

  autoFlush 属性 设置当 out 输出流缓冲区满了之后，是否自动刷新冲级区。默认值是 true。

  buffer 属性 设置 out 缓冲区的大小。默认是 8kb

  

  缓冲区溢出错误:

  ![](D:\java\imagesrecord\jsp9.png)

- errorPage 属性 设置当 jsp 页面运行时出错，自动跳转去的错误页面路径。

  ```xml
  <!--
  errorPage 表示错误后自动跳转去的路径 <br/>
  这个路径一般都是以斜杠打头，它表示请求地址为 http://ip:port/工程路径/
  映射到代码的 Web 目录
  -->
  ```

- isErrorPage 属性 设置当前 jsp 页面是否是错误信息页面。默认是 false。如果是 true 可以 获取异常信息。
- session 属性 设置访问当前 jsp 页面，是否会创建 HttpSessionn 对象。默认是 true
- extends 属性 设置 jsp 翻译出来的 java 类默认继承谁

 

###### b)jsp中的常用脚本

- **声明脚本（极少使用）**

  声明脚本的格式是： <%! 声明 java 代码 %> 作用：可以给 jsp 翻译出来的 java 类定义属性和方法甚至是静态代码块。内部类等。

   

  声明脚本例子：

  ![](D:\java\imagesrecord\QQ截图20211130200152.png)

- **表达式脚本（常用）**

表达式脚本的格式是：<%=表达式%>

表达式脚本的作用是： jsp 页面上输出数据。

 表达式脚本的特点：

- 所有的表达式脚本都会被翻译到_jspService() 方法中
- 表达式脚本都会被翻译成为 out.print()输出到页面
- 由于表达式脚本翻译的内容都在 _jspService() 方法中,所以 _jspService()方法中的对象都可以直接使用。
- 表达式脚本中的表达式不能以分号结束。

![](D:\java\imagesrecord\QQ截图20211130203045.png)

- 代码脚本

  代码脚本的格式是：

  <% java 语句 %>

  代码脚本的作用是：可以在 jsp 页面中，编写我们自己需要的功能（写的是 java 语句）。

代码脚本的特点是：

- 代码脚本翻译之后都在_jspService 方法中
- 代码脚本由于翻译到 _jspService()方法中，所以在 _jspService()方法中的现有对象都可以直接使用。
- 还可以由多个代码脚本块组合完成一个完整的 java 语句。
- 代码脚本还可以和表达式脚本一起组合使用，在 jsp 页面上输出数据

![](D:\java\imagesrecord\QQ截图20211201093639.png)

###### c)jsp中的三种注释

- <!-- 这是 html 注释 --> html 注释会被翻译到 java 源代码中。在_jspService 方法里，以 out.writer 输出到客户端。
- // 单行 java 注释      /* 多行 java 注释 */    java 注释会被翻译到 java 源代码中
- <%-- 这是 jsp 注释 --%>   jsp 注释可以注掉jsp 页面中所有的代码

#### 6.jsp九大内置对象

jsp 中的内置对象，是指 Tomcat 在翻译 jsp 页面成为 Servlet 源代码后，内部提供的九大对象，叫内置对象。

![](D:\java\imagesrecord\QQ截图20211201095343.png)

#### 7.jsp 四大域对象

四个域对象分别是：

- pageContext (PageContextImpl 类) 当前 jsp页面范围内有效
- request (HttpServletRequest 类)、 一次请求内有效
- session (HttpSession 类)、 一个会话范围内有效（打开浏览器访问服务器，直到关闭浏览器）
- application (ServletContext 类) 整个 web 工程范围内都有效（只要 web 工程不停止，数据都在）

域对象是可以像 Map 一样存取数据的对象。四个域对象功能一样。不同的是它们对数据的存取范围

虽然四个域对象都可以存取数据。在使用上它们是有优先顺序的。

四个域在使用的时候，优先顺序分别是，他们从小到大的范围的顺序。

pageContext ====>>> request ====>>> session ====>>> application

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 22837
  Date: 2021/12/1
  Time: 12:07
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"%>
<html>
<head>
    <title>四大域对象</title>
</head>
<body>
<h1>scope.jsp页面</h1>
<%
    // 往四个域中都分别保存了数据,pageContext.setAttribute("key", "pageContext");
    //报错，原因为没有加入jar包
    request.setAttribute("key", "request");
    session.setAttribute("key", "session");
    application.setAttribute("key", "application");
%>
request 域是否有值：<%=request.getAttribute("key")%> <br>
session 域是否有值：<%=session.getAttribute("key")%> <br>
application 域是否有值：<%=application.getAttribute("key")%> <br>
</body>
</html>

```

#### 8.jsp 中的 out 输出和 response.getWriter 输出的区别

response 中表示响应，我们经常用于设置返回给客户端的内容（输出）

out 也是给用户做输出使用的

![](D:\java\imagesrecord\QQ截图20211201122743.png)

由于 jsp 翻译之后，底层源代码都是使用 out 来进行输出，所以一般情况下。我们在 jsp 页面中统一使用 out 来进行输出。避 免打乱页面输出内容的顺序。

out.write() 输出字符串没有问题

out.print() 输出任意数据都没有问题（都转换成为字符串后调用的 write 输出）

深入源码，浅出结论：在 jsp 页面中，可以统一使用 out.print()来进行输出

#### 9.jsp的常用标签

###### a)jsp静态包含 (常用)

示例说明：

<%@ include file=""%> 就是静态包含

file 属性指定你要包含的 jsp 页面的路径

地址中第一个斜杠 / 表示为 http://ip:port/工程路径/ 映射到代码的 web 目录

静态包含的特点：

- 静态包含不会翻译被包含的 jsp 页面。
- 静态包含其实是把被包含的 jsp 页面的代码拷贝到包含的位置执行输出

<%@ include file="/include/footer.jsp"%>

###### b)jsp 动态包含

 <jsp:include page="">   < </jsp:include>> 这是动态包含

page 属性是指定你要包含的 jsp 页面的路径

动态包含也可以像静态包含一样，把被包含的内容执行输出到包含位置。

动态包含的特点：

- 动态包含会把包含的 jsp 页面也翻译成为 java 代码
- 动态包含底层代码使用如下代码去调用被包含的 jsp 页面执行输出JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);
- 动态包含，还可以传递参数

```jsp
<jsp:include page="/include/footer.jsp">
	<jsp:param name="username" value="bbj"/>
	<jsp:param name="password" value="root"/>
</jsp:include>
```

动态包含的底层原理：

![](D:\java\imagesrecord\QQ截图20211203085615.png)

###### c)jsp 标签-转发

 <jsp:forward page=""><</jsp:forward>>是请求转发标签，它的功能就是请求转发

page 属性设置请求转发的路径

```jsp
<jsp:forward page="/scope2.jsp"></jsp:forward>
```

###### 例题

![](D:\java\imagesrecord\QQ截图20211203092323.png)

Student类：

```java
public class Student {
		private Integer id;
		private String name;
		private Integer age;
		private String phone;
}
```

SearchStudentServlet程序:注意配置web.xml

```java
public class SearchStudentServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException,
IOException {
    // 获取请求的参数
	// 发 sql 语句查询学生的信息
	// 使用 for 循环生成查询到的数据做模拟
    List<Student> studentList = new ArrayList<Student>();
    for (int i = 0; i < 10; i++) {
		int t = i + 1;
		studentList.add(new Student(t,"name"+t, 18+t,"phone"+t));
	}
    // 保存查询到的结果（学生信息）到 request 域
    req.setAttribute("stuList", studentList)
      // 请求转发到 showStudent.jsp 页面
	req.getRequestDispatcher("/test/showStudent.jsp").forward(req,resp);
	}
}
```

showStudent.jsp页面

```jsp
<%@ page import="java.util.List" %>
<%@ page import="com.atguigu.pojo.Student" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8"language="java"%>
<html>
<head>
    	<title>Title</title>
    	<style>
            table{
				border: 1px blue solid;
				width: 600px;
				border-collapse: collapse;<!--合并每个格子边框-->
			}
            td,th{
				border: 1px blue solid;
			}
          </style>
</head>
<body>
    <%
	List<Student> studentList = (List<Student>) request.getAttribute("stuList");
	%>
    <table>
		<tr>
			<td>编号</td>
			<td>姓名</td>
			<td>年龄</td>
			<td>电话</td>
			<td>操作</td>
		</tr>
        	<% for (Student student : studentList) { %>
				<tr>
					<td><%=student.getId()%></td>
					<td><%=student.getName()%></td>
					<td><%=student.getAge()%></td>
					<td><%=student.getPhone()%></td>
					<td>删除、修改</td>
					</tr>
			<% } %>
    </table>
</body>       
</html>

            
```



#### 10.Listener监听器

###### a)什么是监听器？

- Listener 监听器它是 JavaWeb 的三大组件之一。JavaWeb 的三大组件分别是：Servlet 程序、Filter 过滤器、Listener 监 听器
- Listener 它是 JavaEE 的规范，就是接口
- 监听器的作用是，监听某种事物的变化。然后通过回调函数，反馈给客户（程序）去做一些相应的处理。

###### b)ServletContextListener 监听器

ServletContextListener 它可以监听 ServletContext 对象的创建和销毁

ServletContext 对象在 web 工程启动的时候创建，在 web工程停止的时候销毁

监听到创建和销毁之后都会分别调用  ServletContextListener 监听器的方法反馈。

两个方法分别是：

```java
public interface ServletContextListener extends EventListener {
    /**
	* 在 ServletContext 对象创建之后马上调用，做初始化
	*/
    void contextInitialized(ServletContextEvent var1);
	/**
	* 在 ServletContext 对象销毁之后调用
	*/
    void contextDestroyed(ServletContextEvent var1);
}
```

如何使用 ServletContextListener 监听器监听 ServletContext 对象。

 使用步骤如下： 

- 编写一个类去实现 ServletContextListener 
- 实现其两个回调方法 
- 到 web.xml 中去配置监听器

监听器实现类：

```java
public class MyServletContextListenerImpl implements ServletContextListener {
		@Override
		public void contextInitialized(ServletContextEvent sce) {
		System.out.println("ServletContext 对象被创建了");
		}
		@Override
		public void contextDestroyed(ServletContextEvent sce) {
		System.out.println("ServletContext 对象被销毁了");
		}
}
```

web.xml 中的配置：

```xml
<!--配置监听器-->
<listener>
	<listener-class>com.atguigu.listener.MyServletContextListenerImpl</listener-class>
</listener>
```

