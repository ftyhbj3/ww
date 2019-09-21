#	jquery

##	each方法

遍历jquery对象

each方法非常简单，只有一个参数callback，是一个函数

function callback(i，item){

​	//javascript代码

}

i：每次遍历时，系统会自动将下标放入变量i中

item：每次遍历时，系统会自动将遍历得到的值(dom对象)放到item选项中

jquery对象本质是一个DOM对象集合的数据，所以遍历时每个遍历对象都是一个DOM对象，所以item也是一个DOM对象，如果想使用jquery中的属性或方法，需要通过$符号进行封装

#	ajax

##	什么是ajax

Asynchronous：异步

asyncio

JavaScript：Javascript技术

And：和

XML：xml

是一种在页面没有刷新的情况下，通过客户端浏览器与服务器交互的一种技术

**ajax语言的载体是javascript最大特点，页面不刷新完成请求**

##	起源

1998年微软IE5.5浏览器中应用此技术(Outlook小组研发)，当时名称为“XMLHTTP”

2005年Google公司真正把Ajax技术应用在web网页中(Google Map、Google Gmail)

由于ajax的出现，javascript语言被重视

**基于IE内核的浏览器(IE以下版本)**

**var xhr = new ActiveObject("Microsoft.XMLHTTP");**

**基于W3C内核的浏览器(IE以上内核，以及谷歌，火狐等)**

**var xhr = new XMLHttpRequest();**

##	ajax写法

```

<script>
	window.onload = function(){
		var obtn = document.getElementById('one');
		//给按钮绑定事件，向服务器端请求数据
		obtn.onclick = function(){
			//具体请求步骤
			//创建一个ajax对象
			var xhr = new XMLHttpRequest();
			//设置监听事件，处理回调函数
			xhr.onreadystechange = function(){
				//完成请求后的处理
				if(xhr.readyState == 4){
					var res = xhr.responseText;
					//返回的数据结果
					console.log(res);
				}
			}
			//创建一个http请求
			xhr.open('get','demo.php');
			//发送请求
			xhr.send(null);
		}
	}
</script>
<style tyle = 'text/css'></style>

<body>
	<input type = 'button' value = '获取数据' id = 'one'/>
</body>
```

**demo.php**

```
<?php
	$arr = [
		['name'=>'tom','age'=>'18','sex'=>'male']
		['name'=>'tii','age'=>'18','sex'=>'male']
		['name'=>'too','age'=>'18','sex'=>'male']
	];
	echo json_encode($arr);
>
```

#	引用ajax

ajax的底层实现

jquery.ajax(options)

$.ajax();

ajax的高级实现

$.get(url,[data],[callback])

$.post(url,[data],[callback])

##	ajax的实现

jquery.ajax(options)或$.ajax(option)

options是一个json对象

ajax方法只有一个参数，要求是一个json对象

async：是否异步，默认值是true

cache：是否缓存，默认值是true，get

complete：当ajax状态码为4时，所触发的回调函数

contentType：请求头信息，如果是post请求，默认是application/x-www-form-urlencoded

data：发送ajax时传递的参数，要求是一个字符串或json格式对象

dataType：期待的返回值类型，常用的是用有text，xml，json，默认为text

success：当ajax状态码为4qie响应状态码为200时，所触发的回调函数

type：http请求，get与post  #get post put patch delete

url：请求的页面

```
<script src = './jquery-1.8.3.js'><script>
<script>
	$(function(){
		$('input[type = button]').click(function(){
			//写ajax的请求
			$.ajax({
				type:'get',
				url:'demo.php',
				success:function(msg){
				//msg是从服务器端请求回来的数据
				$('#res').html(msg);
				}
			});
		});
	});
</script>
<style>
#res{width:300px;height:150px;background:gray;}
</style>
<body>
	<input type = 'button' value = '获取ajax请求数据'>
	<br/> 
	<div id = 'res'></div>
</body>
```

**demo.php**

```
<?php
	echo '你怎么穿品如衣服'；
>
```

##	ajax缓存

在原生 JS的ajax中，是在url后面添加随机数或者添加时间截或者添加If-Modified-Since来解决缓存问题

在jquery的ajax中，我们可以使用cache：false来解决

```
<script src = './jquery-1.8.3.js'></script>
<script>
	$(function(){
		$('input[type=button]').click(function(){
			//获取输入的两个值
			var num1 = $('#num1').val();
			var num2 = $('#num2').val();
			//写ajax的请求
			//post请求使用方式一，data是一个字符串格式的数据
			$.ajax({
				type:'get',
				cache:'false',
				data:'num1='+num1+'&num2='+num2,
				url:'demo.php',
				success:function(msg){
					$('#res).html(msg);
				}
			});
		});
	});
</script>
```

#	XML和JSON

**ajax中XML处理大批数据**

XML和HTML非常相似，但是它不是用来做网页结构的，而是一种DTD严格约束型的数据传输格式，在互联网的第三方制度和金融交易中经常使用的一种数据交互格式

**为什么在金融交易中心会使用XML**

因为XML可以控制自定义标签中可以输入‘值得类型’和‘长度’或者其他的约束

**返回复杂的xml数据**

```
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="./jquery-1.8.3.js"></script>
		<script>
			$(function(){
		        $("input[type=button]").click(function(){
		                $.ajax({
		                    type:'get',
		                    dataType:'xml',
		                    url:'demo.php',
		                    success:function(msg){
		                        //返回的是复杂的xml数据。
		                        var str = '';
		                        $(msg).find('book').each(function(i,item){
		                            str+=$(item).find('name').text()+'---'+$(item).find('price').text()+'<br/>';
		                        });
		                        $('#res').html(str);
		                    }
		                });   
		        });    
		});
		</script>
	</head>
	<body>
		<input type="button" value="获取数据"/><hr/>
		    <div id="res"></div>
	</body>
</html>

```

demo.php

```
<?php
header('content-type:text/xml;charset=utf-8');
$str=<<<XML
<root>
        <book>
                <name>从入门到放弃</name>
                <price>123</price>
        </book>
        <book>
                <name>我</name>
                <price>45</price>
        </book>
        <book>
                <name>狗子</name>
                <price>15</price>
        </book>
         <book>
                <name>python从入门到放弃</name>
                <price>55</price>
        </book>
</root>
XML;

echo $str;
>
```

**ajax中json处理大批数据**



**返回复杂的json格式数据**

```
<script src = './jquery-1.8.3.js'></script>
<script>
	$(function(){
		$("input[type=button]").click(function(){
			$.ajax({
				type:'get',
				dataType:'json',
				url:'demo.php',
				success:function(msg){
                //处理大批量的json格式数据
                 var str = '';
                 $(msg).each(function(i,item){
					 str+=item.name+'--'+item.age+'---'+item.address+'<br/>';
                            });
						$('#res').html(str);
						}
					});
				});    
			});
</script>

 <body>
        <input type="button" value="获取数据"/><hr>
        <div id="res"></div>
</body>
```

**demo.php**

```
<?php
    $arr = [
        ['name'=>'狗子','age'=>18,'address'=>'中国'],
        ['name'=>'沈阳','age'=>18,'address'=>'中国'],
        ['name'=>'小米','age'=>18,'address'=>'中国'],
        ['name'=>'呵呵','age'=>18,'address'=>'中国']
    ];
echo json_encode($arr);
>
```

#	ajax的高级实现

$.get(url,[data],[callback],[dataType])：ajax中的get请求

$.post(url,[data],[callback],[dataType])：ajax中的post请求

url：请求的url地址

[data]：要求格式是一个json对象，也可以是字符串，但是建议使用json对象

[callback]：当ajax状态码为4且响应状态码为200时所触发的回调函数

[dataType]：期待的返回值类型，text，xml，json

#	ajax中的跨域请求

同源策略：起到保护作用，不让其他服务器请求

```
<script src="./jquery-1.8.js"></script>
<script>
	$(function(){
        $("input[type=button]").click(function(){
              var name = $('input[name=name]').val();
              var age = $('input[name=age]').val();
              var data = {name:name,age:age};              				 $.post('http://www.hal.com/demo9.php',data,
function(msg){
	console.log(msg);
               });
        });    
});
</script>

<body>
      姓名：<input type="text" name="name"/><br/>
      年龄：<input type="text" name="age"/><br/>
      <input type="button" value="提交"/><hr>
</body>


2new_file.html?__hbt=1522250043273:1 Failed to load http://www.hal.com/demo8.php: No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://127.0.0.1:8020' is therefore not allowed access.

//跨域请求被阻止
```

##	跨域请求详解

受到浏览器中的同源策略影响，基于安全考虑，不允许跨域

同源策略阻止从一个域上加载的脚本获取或操作另一个域上的文档属性，也就是说，受到请求的url的域必须与当前web页面的域相同

###	jsonp解决跨域请求

JSONP是一个非官方的协议，它允许在服务器端集成script tags返回至客户端，通过javascript callback的形式实现跨域访问

json：一组无序数据的集合，主要实现数据的传输与存储，是一种通用的数据传输格式

jsonp：是一种非官方协议，主要用于解决ajax跨域请求问题

###	jquery解决跨域问题

$.ajax
主要是添加两个选项

一个是dataType：jsonp(指定数据传输的类型)和jsonp：‘fn’(指定回调函数的参数，与后端文件里面介绍函数的参数名称一致即可)

$.get

$.getJSON

都是通过使用get请求解决跨域问题



nginx允许跨域

apache允许跨域





























































































































