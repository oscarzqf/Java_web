# xml

#### 1.xml简介



###### 什么是xml语言？

xml 是可扩展的标记性语言



###### xml的作用

xml 的主要作用有： 

- 用来保存数据，而且这些数据具有自我描述性 
- 它还可以做为项目或者模块的配置文件 
- 还可以做为网络传输数据的格式（现在 JSON 为主）。



#### 2.xml语法

###### 2.1创建xml文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--
<?xml version="1.0" encoding="UTF-8" ?>为xml文件的声明
version="1.0" version表示xml的版本
endcoding表示xml文件本身的编码
<?xml 要连一起
-->
<books>
    <book sn="SN12345666"> <!--book表示一个图书的信息 sn属性表示图书的序号-->
        <name>时间简史</name><!--name标签是表示书名-->
        <author>霍金</author><!--author标签表示作者-->
        <price>75</price>   <!--price标签表示价格-->
    </book>
    
</books>

```

###### 2.2xml注释

html 和 XML 注释 一样 



###### 2.3元素（标签）

- 名称可以含字母、数字以及其他的字符
- 名称不能以数字或者标点符号开始
- 名称不能包含空格

**xml 中的元素（标签）也 分成 单标签和双标签**： 

- 单标签 格式： <标签名 属性=”值” 属性=”值” ...... /> 
- 双标签 格式：< 标签名 属性=”值” 属性=”值” ......>文本数据或子标签</标签名>



#### 3.xml属性

- xml 的标签属性和 html 的标签属性是非常类似的，属性可以提供元素的额外信息

- 在标签上可以书写属性： 一个标签上可以书写多个属性。每个属性的值必须使用 引号 引起来。 规则和标签的书写规则一致

  注意事项：

- XML 标签对大小写敏感

- XML 文档必须有根元素；根元素就是顶级元素， 没有父标签的元素，叫顶级元素。 根元素是没有父标签的顶级元素，而且是**唯一**一个才行。

- XML 中的特殊字符需要使用字符实体

###### 文本区域（CDATA区）

CDATA 语法可以告诉 xml 解析器， CDATA 里的文本内容，只是纯文本，不需要 xml语法解析

CDATA 格式：

**<![CDATA[ 这里可以把你输入的字符原样显示，不会解析 xml ]]>**

------



#### 4.xml解析技术介绍

xml 可扩展的标记语言。 不管是 html 文件还是 xml 文件它们都是标记型文档，都可以使用 w3c 组织制定的 dom 技术来解析。

<img src="D:\java\imagesrecord\QQ截图20211005160921.png" style="zoom:50%;" />

document 对象表示的是整个文档（可以是 html 文档，也可以是 xml 文档）

早期 JDK 为我们提供了两种 xml 解析技术 DOM 和 Sax 简介（已经过时，但我们需要知道这两种技术）

dom 解析技术是 W3C 组织制定的，而所有的编程语言都对这个解析技术使用了自己语言的特点进行实现。 Java 对 dom 技术解析标记也做了实现。 

sun 公司在 JDK5 版本对 dom 解析技术进行升级：SAX（ Simple API for XML ） SAX 解析，它跟 W3C 制定的解析不太一样。它是以类似事件机制通过回调告诉用户当前正在解析的内容。 它是一行一行的读取 xml 文件进行解析的。不会创建大量的 dom 对象。 所以它在解析 xml 的时候，在内存的使用上。和性能上。都优于 Dom 解析。 

第三方的解析：

- jdom 在 dom 基础上进行了封装  

- dom4j 又对 jdom 进行了封装。 

- pull 主要用在 Android 手机开发，是在跟 sax 非常类似都是事件机制解析 xml 文件。

这个 Dom4j 它是第三方的解析技术。我们需要使用第三方给我们提供好的类库才可以解析 xml 文件。

###### 4.1dom4j解析技术

由于 dom4j 它不是 sun 公司的技术，而属于第三方公司的技术，我们需要使用 dom4j 就需要到 dom4j 官网下载 dom4j 的 jar 包。并在工程或模块引入dom4j的jar包

###### dom4j 编程步骤

- 第一步： 先加载 xml 文件创建 Document 对象 
- 第二步：通过 Document 对象拿到根元素对象 
- 第三步：通过根元素.elelemts(标签名); 可以返回一个集合，这个集合里放着。所有你指定的标签名的元素对象 
- 第四步：找到你想要修改、删除的子元素，进行相应在的操作 
- 第五步，保存到硬盘上



需要解析的内容：book.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<books>
    <book sn="SN12341232">
        <name>辟邪剑谱</name>
        <price>9.9</price>
        <author>班主任</author>
    </book>
    <book sn="SN12341231">
        <name>葵花宝典</name>
        <price>99.99</price>
        <author>班长</author>
    </book>
</books>

```

对应的java类：Book.java

```java
package com.zqf.domxml;

import java.math.BigDecimal;

/**
 * @author oscarzqf
 * @description
 * @create 2021-10-05-16:25
 */
public class Book {
    private String sn;
    private String name;
    private double price;
    private String author;

    public Book() {
    }

    public Book(String sn, String name, double price, String author) {
        this.sn = sn;
        this.name = name;
        this.price = price;
        this.author = author;
    }

    public String getSn() {
        return sn;
    }

    public void setSn(String sn) {
        this.sn = sn;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    @Override
    public String toString() {
        return "Book{" +
                "sn='" + sn + '\'' +
                ", name='" + name + '\'' +
                ", price=" + price +
                ", author='" + author + '\'' +
                '}';
    }
}

```

java读取步骤：

```java
@Test
    /**
     * 读取books.xml文件生成book类
     */
    public void test2() throws Exception{
        //1.读取book.xml文件,单元测试时相对路径为当前moudle开始算
        SAXReader saxReader = new SAXReader();
        Document document = saxReader.read("xml/book.xml");
        //2.通过Documnet元素获取根元素
        Element rootElement = document.getRootElement();
        //3.通过根元素获取book标签对象
        //element()和elements()都是通过标签名查找子元素
        List<Element> books = rootElement.elements("book");
        //4.遍历，处理每一个book标签转换为Book类
        for(Element book:books){
            //asXML()可以把标签对象转换为标签字符
            //根据标签名获取book中的标签
            Element nameElement = book.element("name");
            //getText()：可以获取标签中的文本内容
            String nameText=nameElement.getText();
            //elementText():可以直接获取指定标签名的内容
            String priceText = book.elementText("price");
            String authorText=book.elementText("author");
            //获取属性值
            String snValue = book.attributeValue("sn");
            //装入对象
            System.out.println(new Book(snValue,nameText,
                    Double.parseDouble(priceText),authorText));
        }
    }
```

