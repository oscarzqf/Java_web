#### jQery

#### 1.核心函数的四个作用

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>

<script type="text/javascript" src="../script/jquery-1.7.2.js"></script>
<script type="text/javascript">

	//使用$()代替window.onload
	$(function(){
		//使用选择器获取按钮对象，随后绑定单击响应函数
        //#id表示根据ID选择对象
		$("#btnId").click(function(){
			//弹出Hello
			alert('Hello');
		});
	});
</script>


</head>
<body>

	<button id="btnId">SayHello</button>

</body>
</html>

```

###### **核心函数$()**

- 传入参数为[函数]时，在文档加载完成后执行这个函数

  相当于window.onload

- 传入参数为[HTML字符串]时，根据这个字符串创建元素节点

- 传入参数为[选择器字符串]时，根据这个字符串查找元素节点对象

  $("#id");  	id选择器，根据id查询节点对象

  $("标签名");标签名选择器

  $(".class属性值")； 类选择器，根据class属性查询标签对象 	

- 传入参数为[DOM对象]时，将DOM对象包装为jquery对象返回

  DOM对象：通过getElementBy..查询出来的对象

  [object HTML 标签名]

  jQery对象：通过jQery创建，包装，查询到的对象

  [objec object]

  

###### jQery对象的本质

- jQuery 对象是 dom 对象的数组 + jQuery 提供的一系列功能函数。

- 两种对象使用的区别

  jQuery 对象不能使用 DOM 对象的属性和方法， DOM 对象也不能使用 jQuery 对象的属性和方法

###### 两种对象的相互转换

1、dom 对象转化为 jQuery 对象（*重点） 

- 先有 DOM 对象 

- *$( DOM 对象 ) 就可以转换成为 jQuery 对象*

*2、jQuery 对象转为 dom 对象（*重点）

- 先有 jQuery 对象 

- jQuery 对象[下标]取出相应的 DOM 对象

#### 2.基本选择器

- \#ID 选择器：根据 id 查找标签对象 

- .class 选择器：根据 class 查找标签对象 

  ```html
  $(function (){
  					$("#btn1").click(()=>{
  						$("#one").css("background-color","#bbffaa");
  						$(".mini").css("background-color","#bbffaa");
  					});
  
  				});
  ```

  

- element 选择器：根据标签名查找标签对象 

- 选择器：表示任意的，所有的元素 

- selector1，selector2 组合选择器：合并选择器 1，选择器 2 的结果并返回

  

#### 3.层级选择器

- ancestor descendant 后代选择器 ：在给定的祖先元素下匹配所有的后代元素 
- parent > child 子元素选择器：在给定的父元素下匹配所有的子元素 
- prev + next 相邻元素选择器：匹配所有紧接在 prev 元素后的 next 元素 
- prev ~ sibings 之后的兄弟元素选择器：匹配 prev 元素之后的所有 siblings 元素

#### 4.过滤选择器

###### 基本过滤器

- :first 获取第一个元素

-  :last 获取最后个元素 

- :not(selector) 去除所有与给定选择器匹配的元素 

- :even 匹配所有索引值为偶数的元素，从 0 开始计数 

- :odd 匹配所有索引值为奇数的元素，从 0 开始计数 

- :eq(index) 匹配一个给定索引值的元素 

- :gt(index) 匹配所有大于给定索引值的元素 

- :lt(index) 匹配所有小于给定索引值的元素 

- :header 匹配如 h1, h2, h3 之类的标题元素 

- :animated 匹配所有正在执行动画效果的元素

  注意：过滤器可以级联使用div:not(:animated):last

###### 内容过滤器

- :contains(text) 匹配包含给定文本的元素 
- :empty 匹配所有不包含子元素或者文本的空元素 
- :parent 匹配含有子元素或者文本的元素 
- :has(selector) 匹配含有选择器所匹配的元素的元素

###### 属性过滤器

- [attribute] 匹配包含给定属性的元素。 
- [attribute=value] 匹配给定的属性是某个特定值的元素 
- [attribute!=value] 匹配所有不含有指定的属性，或者属性不等于特定值的元素。 
- [attribute^=value] 匹配给定的属性是以某些值开始的元素 
- [attribute$=value] 匹配给定的属性是以某些值结尾的元素 
- [attribute*=value] 匹配给定的属性是以包含某些值的元素 
- 复合属性选择器，需要同时满足多个条件时使用,并列写[] []

###### 表单过滤器

- :input 匹配所有 input, textarea, select 和 button 元素 

- :text 匹配所有 文本输入框 

- :password 匹配所有的密码输入框 

- :radio 匹配所有的单选框 

- :checkbox 匹配所有的复选框 

- :submit 匹配所有提交按钮 

- :image 匹配所有 img 标签 

- :reset 匹配所有重置按钮 

- :button 匹配所有 input type=button 按钮 

- :file 匹配所有 input type=file 文件上传 

- :hidden 匹配所有不可见元素 display:none 或 input 

  

###### 表单对象属性筛选

- :enabled 匹配所有可用元素 

- :disabled 匹配所有不可用元素 

- :checked 匹配所有选中的单选，复选，和下拉列表中选中的 option 标签对象 

- :selected 匹配所有选中的 option

  

#### 5.jQery元素筛选

​      筛选：

- eq() 获取给定索引的元素 功能跟 :eq() 一样 

- first() 获取第一个元素 功能跟 :first 一样 

- last() 获取最后一个元素 功能跟 :last 一样 

- filter(exp) 留下匹配的元素 is(exp) 判断是否匹配给定的选择器，只要有一个匹配就返回，true 

- has(exp) 返回包含有匹配选择器的元素的元素 功能跟 :has 一样 

- not(exp) 删除匹配选择器的元素 功能跟 :not 一样 

  查找：

- children(exp) 返回匹配给定选择器的子元素 功能跟 parent>child 一样 

- find(exp) 返回匹配给定选择器的后代元素 功能跟 ancestor descendant 一样

- next() 返回当前元素的下一个兄弟元素 功能跟 prev + next 功能一样 

- nextAll() 返回当前元素后面所有的兄弟元素 功能跟 prev ~ siblings 功能一样 

- nextUntil() 返回当前元素到指定匹配的元素为止的后面元素 

- parent() 返回父元素 

- prev(exp) 返回当前元素的上一个兄弟元素 

- prevAll() 返回当前元素前面所有的兄弟元素 

- prevUnit(exp) 返回当前元素到指定匹配的元素为止的前面元素 

- siblings(exp) 返回所有兄弟元素

  串联 

- add() 把 add 匹配的选择器的元素添加到当前 jquery

  

#### 6.jQery属性操作

- html() 它可以设置和获取起始标签和结束标签中的内容。 跟 dom 属性 innerHTML 一样。 

- text() 它可以设置和获取起始标签和结束标签中的文本。 跟 dom 属性 innerText 一样。 

- val() 它可以设置和获取表单项的 value 属性值。 跟 dom 属性 value 一样       ;此方法同时也可以设置多个表单项的选中状态

  val（["选项对应的value值"]）

  ```html
  <script type="text/javascript">
  $(function () {
  /*
  // 批量操作单选
  $(":radio").val(["radio2"]);
  // 批量操作筛选框的选中状态
  $(":checkbox").val(["checkbox3","checkbox2"]);
  // 批量操作多选的下拉框选中状态
  $("#multiple").val(["mul2","mul3","mul4"]);
  // 操作单选的下拉框选中状态
  $("#single").val(["sin2"]);
  */
  $("#multiple,#single,:radio,:checkbox").val(["radio2","checkbox1","checkbox3","mul1","mul4","sin3"]
  );
  });
  ```

  **注意：不传参数是获取，传递参数是设置**

  

  - attr() 可以设置和获取属性的值，不推荐操作 checked、readOnly、selected、disabled 等等。attr 方法还可以操作非标准的属性。比如自定义属性：abc,bbj 

    ```html
        $(()=>{
          $(":checkbox:first").attr("name");//获取多选框属性值
          $(":checkbox:first").attr("name","abc");//设置多选框属性值
        });
    ```

    

  - prop() 可以设置和获取属性的值,只推荐操作 checked、readOnly、selected、disabled

    ```html
       $(()=>{
         $(":checkbox").prop("checked",true);//设置选中状态
        });
    ```

    ###### 练习：全选，单选，多选，反选,表单操作

    ```html
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
    <script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
    <script type="text/javascript">
    	
    	$(()=>{
    		$("#checkedAllBtn").click(()=>{//全选
    			$(":checkbox").prop("checked",true);
    		});
    		$("#checkedNoBtn").click(()=>{//全不选
    			$(":checkbox").prop("checked",false);
    		});
    
    		$("#checkedRevBtn").click(()=>{//反选
    			$(":checkbox[name='items']").each(function (){
    				this.checked=!this.checked;
    			});
    		});
    		// 给【全选/全不选】绑定单击事件
    		$("#checkedAllBox").click(function (){//不能使用箭头函数
    		// 在事件的 function 函数中，有一个 this 对象，这个 this 对象是当前正在响应事件的 dom 对象
    			// alert(this.checked);
    			$(":checkbox[name='items']").prop("checked",this.checked);
    		});
    		$("form").click(()=>{//为整个form添加事件，点击就会检测
    			let allCount = $(":checkbox[name='items']").length;
    			let selectCount = $(":checkbox[name='items']:checked").length;
    			$("#checkedAllBox").prop("checked",allCount===selectCount);
    		});
    
    		$("#sendBtn").click(()=>{//打印值
    			$(":checkbox[name='items']:checked").each(function (){
    				alert(this.value);
    			});
    		});
    	});
    	
    </script>
    </head>
    <body>
    
    	<form method="post" action="">
    	
    		你爱好的运动是？<input type="checkbox" id="checkedAllBox" />全选/全不选 
    		
    		<br />
    		<input type="checkbox" name="items" value="足球" />足球
    		<input type="checkbox" name="items" value="篮球" />篮球
    		<input type="checkbox" name="items" value="羽毛球" />羽毛球
    		<input type="checkbox" name="items" value="乒乓球" />乒乓球
    		<br />
    		<input type="button" id="checkedAllBtn" value="全　选" />
    		<input type="button" id="checkedNoBtn" value="全不选" />
    		<input type="button" id="checkedRevBtn" value="反　选" />
    		<input type="button" id="sendBtn" value="提　交" />
    	</form>
    
    </body>
    </html>
    ```

    

#### 7.DOM的增删改

###### 内部插入

- appendTo() 	a.appendTo(b)   把 a 插入到 b 子元素末尾，成为最后一个子元素
- prependTo()     a.prependTo(b)  把 a 插到 b 所有子元素前面，成为第一个子元素

###### 外部插入

- insertAfter()        a.insertAfter(b) 得到 ba 
- insertBefore()      a.insertBefore(b)   得到 ab

###### 替换

- replaceWith()       a.replaceWith(b)    用 b 替换掉所有 a 
- replaceAll()             a.replaceAll(b)     用 a 替换掉所有 b

###### 删除

- remove()       a.remove();     删除 a 标签 

- empty()          a.empty();    清空 a 标签里的内容,标签还在

  练习：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
	<style type="text/css">
		select {
			width: 100px;
			height: 140px;
		}
		
		div {
			width: 130px;
			float: left;
			text-align: center;
		}
	</style>
	<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
	<script type="text/javascript">
		$(()=>{
			$("button:eq(0)").click(function (){//选中的左边添加到右边
				$("select:eq(0) option:selected").appendTo($("select:eq(1)"))
			});
			$("button:eq(1)").click(function (){//全部添加到右边
				$("select:eq(0) option").appendTo($("select:eq(1)"));
			});
			$("button:eq(2)").click(function (){//右边选中的到左边
				$("select:eq(1) option:selected").appendTo($("select:eq(0)"))
			});
			$("button:eq(3)").click(function (){//右边全部到左边
				$("select:eq(1) option").appendTo($("select:eq(0)"));
			});
		});
	</script>
</head>
<body>

	<div id="left">
		<select multiple="multiple" name="sel01">
			<option value="opt01">选项1</option>
			<option value="opt02">选项2</option>
			<option value="opt03">选项3</option>
			<option value="opt04">选项4</option>
			<option value="opt05">选项5</option>
			<option value="opt06">选项6</option>
			<option value="opt07">选项7</option>
			<option value="opt08">选项8</option>
		</select>
		
		<button>选中添加到右边</button>
		<button>全部添加到右边</button>
	</div>
	<div id="rigth">
		<select multiple="multiple" name="sel02">
		</select>
		<button>选中删除到左边</button>
		<button>全部删除到左边</button>
	</div>

</body>
</html>
```

![](D:\java\imagesrecord\QQ截图20211004204029.png)



练习：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Untitled Document</title>
<link rel="stylesheet" type="text/css" href="styleB/css.css" />
<script type="text/javascript" src="../../script/jquery-1.7.2.js"></script>
<script type="text/javascript">
$(()=>{
	$("#addEmpButton").click(function (){//给提交按钮绑定事件
		let empName= $("input:eq(0)").val();//jQuery对象使用val()
		let email = $("input:eq(1)").val();
		let salary= $("input:eq(2)").val();
		let $obj = $("\t\t<tr>\n" +
				"\t\t\t<td>"+empName+"</td>\n" +//可以使用拼串
				"\t\t\t<td>"+email+"</td>\n" +
				"\t\t\t<td>"+salary+"</td>\n" +
				"\t\t\t<td><a href=\"deleteEmp?id=002\">Delete</a></td>\n" +
				"\t\t</tr>");
	$obj.appendTo("#employeeTable");
	$obj.find("a").click(function (){//给新的a添加事件
		let parent = $(this).parent().parent();
		let name = parent.find("td:first").text();
		if(confirm("确定删除"+name+"吗？")){
			parent.remove();
		}
		return false;
	});
	});

	$("a").click(function (){//新添加的元素不能
		//在事件响应函数中有一个this对象,表示正在触发的DOM对象
		//将当前中在响应的this DOM对象转换为jQuery对象，并获取行对象
		let parent = $(this).parent().parent();
		let name = parent.find("td:first").text();
		if(confirm("确定删除"+name+"吗？")){
			parent.remove();
		}
		return false;
	});

});
	
	
</script>
</head>
<body>

	<table id="employeeTable">
		<tr>
			<th>Name</th>
			<th>Email</th>
			<th>Salary</th>
			<th>&nbsp;</th>
		</tr>
		<tr>
			<td>Tom</td>
			<td>tom@tom.com</td>
			<td>5000</td>
			<td><a href="deleteEmp?id=001">Delete</a></td>
		</tr>
		<tr>
			<td>Jerry</td>
			<td>jerry@sohu.com</td>
			<td>8000</td>
			<td><a href="deleteEmp?id=002">Delete</a></td>
		</tr>
		<tr>
			<td>Bob</td>
			<td>bob@tom.com</td>
			<td>10000</td>
			<td><a href="deleteEmp?id=003">Delete</a></td>
		</tr>
	</table>

	<div id="formDiv">
	
		<h4>添加新员工</h4>

		<table>
			<tr>
				<td class="word">name: </td>
				<td class="inp">
					<input type="text" name="empName" id="empName" />
				</td>
			</tr>
			<tr>
				<td class="word">email: </td>
				<td class="inp">
					<input type="text" name="email" id="email" />
				</td>
			</tr>
			<tr>
				<td class="word">salary: </td>
				<td class="inp">
					<input type="text" name="salary" id="salary" />
				</td>
			</tr>
			<tr>
				<td colspan="2" align="center">
					<button id="addEmpButton" value="abc">
						Submit
					</button>
				</td>
			</tr>
		</table>

	</div>

</body>
</html>

```

<img src="D:\java\imagesrecord\QQ截图20211004214801.png" style="zoom:120%;" />

注意：此处新添加的元素需要重新绑定事件；如果将重复代码提出去单独定义函数表达式，注意this的变化，可以只写函数名将函数体引入。



#### 8.CSS样式操作

- addClass() 添加样式 
- removeClass() 删除样式 
- toggleClass() 有就删除，没有就添加样式。 
- offset() 获取和设置元素的坐标。

```html
	$(function(){
		
		let $divEle = $('div:first');
		
		$('#btn01').click(function(){
			//addClass() - 向被选元素添加一个或多个类
			$divEle.addClass("redDiv blueBorder");
		});
		
		$('#btn02').click(function(){
			//removeClass() - 从被选元素删除一个或多个类 
			$divEle.removeClass("redDiv");
		});
	
		
		$('#btn03').click(function(){
			//toggleClass() - 对被选元素进行添加/删除类的切换操作 
			$divEle.toggleClass("redDiv");
		});
		
		
		$('#btn04').click(function(){
			//offset() - 返回第一个匹配元素相对于文档的位置。
			console.log($divEle.offset());//获取
			$divEle.offset({//设置值
				top:100,
				left:50
			});
		});
	});
```



#### 9.jQery动画

**基本动画** 

- show() 将隐藏的元素显示 
- hide() 将可见的元素隐藏。 
- toggle() 可见就隐藏，不可见就显示。

注意：以上动画方法都可以添加参数。 第一个参数是动画 执行的时长，以毫秒为单位    第二个参数是动画的回调函数 (动画完成后自动调用的函数



**淡入淡出动画**

- fadeIn() 淡入（慢慢可见） 

- fadeOut() 淡出（慢慢消失） 

- fadeTo() 在指定时长内慢慢的将透明度修改到指定的值。0 透明，1 完成可见，0.5 半透明 

- fadeToggle() 淡入/淡出 切换

  **示例**

  ```html
  		$(function(){
  			//显示   show()
  			$("#btn1").click(function(){
  				$("#div1").show();
  			});		
  			//隐藏  hide()
  			$("#btn2").click(function(){
  				$("#div1").hide();
  			});	
  			//切换   toggle()
  			$("#btn3").click(function(){
  				$("#div1").toggle(1000,abc);
  			});	
  			let abc=function (){//传入回调函数，递归调用自动执行动画
  				$("#div1").toggle(1000,abc);
  			}
  			//淡入   fadeIn()
  			$("#btn4").click(function(){
  				$("#div1").fadeIn(1000);
  			});	
  			//淡出  fadeOut()
  			$("#btn5").click(function(){
  				$("#div1").fadeOut();
  			});	
  			
  			//淡化到  fadeTo()
  			$("#btn6").click(function(){						$("#div1").fadeTo(2000,0.5,function(){
  alert('fadeTo完成');//2s内透明度降到0.5
  });
  			});	
  			//淡化切换  fadeToggle()
  			$("#btn7").click(function(){
  				$("#div1").fadeToggle();
  			});	
  		})
  ```

  

**练习：**

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>品牌展示练习</title>
<style type="text/css">
* {
	margin: 0;
	padding: 0;
}

body {
	font-size: 12px;
	text-align: center;
}

a {
	color: #04D;
	text-decoration: none;
}

a:hover {
	color: #F50;
	text-decoration: underline;
}

.SubCategoryBox {
	width: 600px;
	margin: 0 auto;
	text-align: center;
	margin-top: 40px;
}

.SubCategoryBox ul {
	list-style: none;
}

.SubCategoryBox ul li {
	display: block;
	float: left;
	width: 200px;
	line-height: 20px;
}

.showmore , .showless{
	clear: both;
	text-align: center;
	padding-top: 10px;
}

.showmore a , .showless a{
	display: block;
	width: 120px;
	margin: 0 auto;
	line-height: 24px;
	border: 1px solid #AAA;
}

.showmore a span {
	padding-left: 15px;
	background: url(img/down.gif) no-repeat 0 0;
}

.showless a span {
	padding-left: 15px;
	background: url(img/up.gif) no-repeat 0 0;
}

.promoted a {
	color: #F50;
}
</style>
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(function() {
		//初始状态
		$("li:gt(5):not(:last)").hide();
		$(".showmore a").click(function (){
			$("li:gt(5):not(:last)").toggle();//使用切换显示
			if($("li:gt(5):not(:last)").is(":hidden")){
				$("div div a span").text("显示全部品牌");
				$("div div").removeClass("showless");
				$("div div").addClass("showmore");
			}else{
				$("div div a span").text("显示精简品牌");
				$("div div").removeClass("showmore");
				$("div div").addClass("showless");
			}
			$("li:contains('佳能')").toggleClass("promoted")
		return false;
		});
	});
</script>
</head>
<body>
	<div class="SubCategoryBox">
		<ul>
			<li><a href="#">佳能</a><i>(30440) </i></li>
			<li><a href="#">索尼</a><i>(27220) </i></li>
			<li><a href="#">三星</a><i>(20808) </i></li>
			<li><a href="#">尼康</a><i>(17821) </i></li>
			<li><a href="#">松下</a><i>(12289) </i></li>
			<li><a href="#">卡西欧</a><i>(8242) </i></li>
			<li><a href="#">富士</a><i>(14894) </i></li>
			<li><a href="#">柯达</a><i>(9520) </i></li>
			<li><a href="#">宾得</a><i>(2195) </i></li>
			<li><a href="#">理光</a><i>(4114) </i></li>
			<li><a href="#">奥林巴斯</a><i>(12205) </i></li>
			<li><a href="#">明基</a><i>(1466) </i></li>
			<li><a href="#">爱国者</a><i>(3091) </i></li>
			<li><a href="#">其它品牌相机</a><i>(7275) </i></li>
		</ul>
		<div class="showmore">
			<a href="more.html"><span>显示全部品牌</span></a>
		</div>
	</div>
</body>
</html>


```



#### 10.jQuery事件

###### $( function(){} ); 和 window.onload = function(){} 的区别？

**他们分别是在什么时候触发？**

- jQuery 的页面加载完成之后是浏览器的内核解析完页面的标签创建好 DOM 对象之后就会马上执行。 

- 原生 js 的页面加载完成之后，除了要等浏览器内核解析完标签创建好 DOM 对象，还要等标签显示时需要的内容加载 完成（成功或失败）。

**他们触发的顺序？** 

- jQuery 页面加载完成之后先执行 
- 原生 js 的页面加载完成之后

**他们执行的次数？** 

- 原生 js 的页面加载完成之后，只会执行最后一次的赋值函数。 
- jQuery 的页面加载完成之后是全部把注册的 function 函数，依次顺序全部执行。



###### jQuery 中其他的事件处理方法

```html
jquery对象.事件方法(回调函数(){ 触发事件执行的代码 }).事件方法(回调函数(){ 触发事件执行的代码 }).事件方法(回调函数(){ 触发事件执行的代码 })绑定事件可以链式操作
```

- click() 它可以绑定单击事件，以及触发单击事件 

- mouseover() 鼠标移入事件 

- mouseout() 鼠标移出事件 

- bind() 可以给元素一次性绑定一个或多个事件。

  ```html
  //jQuery提供的绑定方式：bind(type,[data],fn)函数把元素和事件绑定起来
  				//type表示要绑定的事件   [data]表示传入的数据   fn表示事件的处理方法
  				//bind(事件字符串,回调函数),后来添加的元素不会绑定事件
  				//使用bind()绑定多个事件   type可以接受多个事件类型，使用空格分割多个事件
  $(".head").bind("click mouseover",function(){
  					$(".content").toggle();});
  ```

   

- one() 使用上跟 bind 一样。但是 one 方法绑定的事件只会响应一次。 

- unbind() 跟 bind 方法相反的操作，解除事件的绑定 

- live() 也是用来绑定事件。它可以用来绑定选择器匹配的所有元素的事件。哪怕这个元素是后面动态创建出 来的也有效

  

###### 事件的冒泡

什么是事件的冒泡？ 

事件的冒泡是指，父子元素同时监听同一个事件。当触发子元素的事件的时候，同一个事件也被传递到了父元素的事件里去 响应。

那么如何阻止事件冒泡呢？ 

在子元素事件函数体内，return false; 可以阻止事件的冒泡传递。



###### javaScript事件对象

事件对象，是封装有触发的事件信息的一个 javascript 对象。（对象,事件类型，坐标等很多信息） 

重点关心的是怎么拿到这个 javascript 的事件对象。以及使用。 

如何获取呢 javascript 事件对象呢？ 

在给元素绑定事件的时候，在事件的 function( event ) 参数列表中添加一个参数，这个参数名，我们习惯取名为 event。 这个 event 就是 javascript 传递参事件处理函数的事件对象

```html
//原生js获取事件对象
//1
window.onload = function () {
document.getElementById("areaDiv").onclick = function (event) {
console.log(event);
}
}
//2
(()=>function(){
  obj.addeventListener('click',function(event){});
});
```

```html
//jQuery代码 获取事件对象
$(function () {
$("#areaDiv").click(function (event) {
console.log(event);
});
});
```

```html
//使用 bind 同时对多个事件绑定同一个函数。怎么获取当前操作是什么事件。
$("#areaDiv").bind("mouseover mouseout",function (event) {
if (event.type == "mouseover") {
console.log("鼠标移入");
} else if (event.type == "mouseout") {
console.log("鼠标移出");
}
});
```



练习：

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<style type="text/css">
	body {
		text-align: center;
	}
	#small {
		margin-top: 150px;
	}
	#showBig {
		position: absolute;
		display: none;
	}
</style>
<script type="text/javascript" src="script/jquery-1.7.2.js"></script>
<script type="text/javascript">
	$(function(){
		$("#small")
			.mouseover(function(event){
				$("#showBig")
					.show()
					.css("left",event.pageX+10)
					.css("top",event.pageY+10);//两张图片离开点距离
			})
			.mousemove(function(event){
				$("#showBig")
					.css("left",event.pageX+10)
					.css("top",event.pageY+10);
			})
			.mouseout(function(){
				$("#showBig").hide();
			});
	});
</script>
</head>
<body>

	<img id="small" src="img/small.jpg" />
	
	<div id="showBig">
		<img src="img/big.jpg">
	</div>

</body>
</html>
```



![](D:\java\imagesrecord\QQ截图20211005124059.png)



------



















































































