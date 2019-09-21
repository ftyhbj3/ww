#	jQuery简介

##	什么是jquery

jQuery是一个开源的，优秀的javascript函数库（js框架），他体积小，简化了很多对HTML、CSS、DOM、事件、动画的处理。

**2006年出现在美国纽约**

**jquery = javascript + Query(查询)**，意思是强大的DOM节点查询

##	JS优势

完善ajax

高低版本兼容性好

##	jquery下载与部署

jquery2.0及以后版本将不再支持IE6/7/8浏览器

jquery-1.8.3.js ：未经过压缩后的版本，具有可读性（内部有许多注释，

空格，回车）

jquery-1.8.3.min.js ：经过压缩后的版本，代表更精简（没有空格和回c

车）

#	jQuery中的选择器

要完成DOM的操作，选择元素是第一步，jquery为我们提供了强大、丰富的选择器

原生代码中使用document.gemElementByld（id）获取指定的id的DOM对象

在jquery中可以通过$标识符+选择器页面中的任意元素

在jQuery中使用$(":input")与$("input")的区别

$(":input")匹配所有表单元素，包括select与textarea元素

$("input")只能匹配input标签

##	**面试题**

在表单元素中disabled='true'和readonly='readonly'区别：

disabled与readonly虽然都可以限定文本框被编辑，但是两者还是有区别的，主要区别在于readonly可以在python页面接收设置为readonly属性表单的值。而disabled是接收不到任何数据的。

##	1、基本选择器

id：根据元素的id属性获取指定的元素

element：根据元素的名称获取指定的元素

selector1，selector2：匹配所有满足条件的元素

.class：根据元素的class属性获取指定的元素

js对象显示出来的是一个标签的样式

jquery单个对象显示出来的是init

jquery集合对象显示出来的是init(?)，集合中储存的是js的单个对象，通过.get()方法获取标签

```
<script type = "text/javascript" src = "./jquery-1.8.3.js"></script>
<script type = "text/javascript">
function t1(){
		//选择id= one的元素
		$("#one").css('background','green');
		//选择span标签，当前页面徐偶有中的span
		$("span").css('background','pink');
		//选择p和div、标签，也就是当前页面中的所有p和div
		$("p,div").css('backgroud','red');
		//选择class = one的元素
		$(".one").css("background","blue");
}
</script>

<body>
	<input type = "button" value = "基本选择器"onclick = "t1()"/><br/>
	<p>今天好天气</p>
	<div>
		<p><span class = 'one'>可以去旅游了</span></p>
		<span id = 'one'>下午可能要下雪</span>
	</div>
	<span>天气好</span></br>
	<span>天气不好</span>
	<p class = "one">中午不吃</p>
</body>
```

##	2、层级选择器

**ancestor  descendant**：选取祖元素下的所有后代元素(祖先与后代)

**parent>child**：选择父元素下的所有子元素

**prev + next**：选取同级元素紧邻的下一个元素

**prev~siblings**：选取同级元素所有的同级兄弟元素

```
<script src = 'jquery-1.8.3.js'></script>
<script>
function t1(){
	//选择div下面所有的span标签(祖先与后代)
	$('div span').css('background',red)
	//选择div下面的子元素为span的(父子关系)
	$('div>span').css('background','green')
	//选择在div后面的第一个span(兄弟节点，只有一个兄弟)
	$('div + span').css('backgroud','blue')
	//选择与div后面的所有同级的span(同胞选择器)
	$('div ~ span').css('backgroud','pink')
}
</script>

	<body>
		<input type = 'button' value = '层级选择器'onclick = 't1()'/><br/>
		<p>天气不错<p>
		<span>东游记</span>
		<div>
			<p><span class = 'one'>旅游</span></p>
			<span id = 'one'>下午有雪</span>
			<div>南游记</div>
			<span>沈阳<span>
		</div>
		<span>减肥</span><br/>	
		<span>吃大餐</span>
		<p class = 'one'>中午不吃</p>
		<span>西游记</span>
	</body>
```

##	3、简单选择器

：first   ：匹配第一个元素

：last    ：匹配最后一个元素

：even   ：匹配所有偶数

：odd     ：匹配所有奇数

：eq(index)   :匹配索引为index的元素(默认索引从0开始)

：ge(index)   :匹配索引大于index的元素

：lt(index)     :匹配索引小于index的元素

：not(selector)    ：匹配除指定选择器意外的其他元素

```
<script src = 'jquery-1.8.3.js'></script>
<script>
	function t1(){
		//查找当前页面中的第一个li标签
        //$("li:first").css('background','red');
        //查找当前页面中的偶数的li标签
        //$("li:even").css('background','red');
        //查询li的排序大于3的li
        //$('li:gt(3)').css('background','green');
        //查询第4个li标签
        //$('li:eq(3)').css('background','green');
        //查询大于2的li标签排除最后一个li标签。
        $("li:gt(1):not(:last)").css('background','red');
	}
</script>

 <body>
    <input type='button' value="简单选择器"onclick="t1()"/><br/>
    <ul>
        <li>西游记</li>
        <li>东游记</li>
        <li>鬼吹灯</li>
        <li>诛仙传</li>
        <li>罗贯中</li>
        <li>李莫愁</li>
    </ul>
 </body>
```

##	4、内容选择器

：contains(text)    ：匹配内容包含指定文本的元素

：empty                 ：匹配内容为空的元素

：has(selector)      :   匹配具有指定选择器的元素

：parent                 ：匹配具有子元素的元素(内容不能为空)

```
<script type = 'jquery-1.8.3.js'></script>
<script>
	function t1(){
		//选择li元素中包含"记"的li元素
        //$("li:contains('记')").css('background','red');
        //选择li中为空的li元素。
        //$("li:empty").css('background','green');
        //选择li中有span标签的li
        //$("li:has('span')").css('background','blue');
        //选择li中有子元素的li(不为空，自己做了父亲)
        $("li:parent").css('background','pink');
}
</script>
<style type="text/css">
</style>
</head>
    <body>
    <input type='button' value="内容选择器"onclick="t1()"/><br/>
    <ul>
        <li>西游记</li>
        <li>东游记</li>
        <li>鬼吹灯</li>
        <li>诛仙传</li>
        <li><span>罗贯中</span></li>
        <li>李莫愁</li>
        <li></li>
    </ul>
	</body>
```

##	5、可见选择器

：hidden   ：匹配所有隐藏元素(display:none, input type = 'hodden')

：visible    ：匹配所有可见元素(display:block)

```
<script src="./jquery-1.8.3.js"></script>
<script>
function t1(){
     //选择li元素中包含"记"的li元素
     //$("li:contains('记')").css('background','red');
     //选择li中为空的li元素。
     //$("li:empty").css('background','green');
     //选择li中有span标签的li
     //$("li:has('span')").css('background','blue');
     //选择li中有子元素的li(不为空，自己做了父亲)
     $("li:parent").css('background','pink');
}
</script>
<style type="text/css">
</style>
</head>
    <body>
    <input type='button' value="内容选择器"onclick="t1()"/><br/>
    <ul>
        <li>西游记</li>
        <li>东游记</li>
        <li>鬼吹灯</li>
        <li>诛仙传</li>
        <li><span>罗贯中</span></li>
        <li>李莫愁</li>
        <li></li>
    </ul>
    </body>
```

##	6、属性选择器

[attribute]：匹配具有指定属性的元素

[attribute = value]：匹配属性值等于value的元素

[attribute != value]：匹配水性指不等于value的元素

[attribute ^= value]：匹配属性值以value开始的元素

[attribute $= value]：匹配属性值以value结尾的元素

[attribute *= value]：匹配属性值包含value的元素

[selectorN]：匹配包含多个属性的元素

```
<script src="./jquery-1.8.3.js"></script>
<script>
function t1(){
    //选择具有name属性的div
    //$('div[name]').css('background','red');
    //选择name属性值为username的div
    //$('div[name=username]').css('background','green');
     //选择name属性值不等于username的div  注意:会选择所有的div的。
    //$('div[name!=username]').css('background','green');
    //选择name属性值以user开头的div
    //$('div[name^=user]').css('background','red');
    //选择name属性值以age结尾的div
    //$('div[name$=age]').css('background','red');
     //选择具有name属性和color属性的div
    $('div[name][color]').html('<p>我的薪水是2300</p>');}
</script>
</head>
<body>
    <input type='button' value="属性选择器" onclick="t1()"/><br/>
    <div name="username">程咬金</div>
    <div name="userage">12</div>
    <div name="age">45</div>
    <div name="salary" color="red">23000</div>
</body>
```

##	7、子类选择器

：nth-child(index/even/odd)从1算起：匹配索引为index的指定元素

：first-child：匹配第一个子元素

：last-chaild：匹配最后一个子元素

：only-chaild：如果房钱元素只有唯一子元素，则匹配

```
<script ./jquery-1.8.3.js"></script>
<script type="text/javascript">
function t1(){
   //选择ul中的第一个子元素
   //$("ul :first-child").html('一个和尚和一群妖怪的故事');
   //选择ul中只有一个li的li标签
   //$("ul :only-child").css('background','red');
   //选择ul中第2个li元素，注意：索引是从1开始的。
   $('ul :nth-child(2)').css('background','green');
}
</script>

<body>
	<input type='button' value="子元素选择器"onclick="t1()"
/><br/>
		<ul>
            <li>西游记</li>
            <li>三国演义</li>
            <li>3个女人和105个男人的故事</li>
            <li>一个男人和大群女人的故事</li>
        </ul>
        <ul><li>煎饼侠</li></ul>
</body>
```

##	8、表单选择器

:input ：匹配所有表单元素

:text ：匹配所有文本框

:password：匹配所有密码框

:radio ：匹配所有单选按钮

:checkbox：匹配所有复选框

:submit ：匹配提交按钮

:reset：匹配重置按钮

:image：匹配图像域

:button：匹配按钮

:file：匹配文件域

:hidden：匹配隐藏表单

```
<script src="./jquery-1.8.3.js"></script>
<script>
function t1(){
        //匹配所有的表单元素
        //$(':input').css('background','yellow');
        //匹配所有的文本框
        //$(":text").css('background','yellow');
        //匹配所有的单选框
         //$(":radio").attr('disabled',true);
          //匹配所有的复选框
         //$(":checkbox").attr('disabled',true);
         //$("input[name=age]").val('请选择你的年龄');
}
</script>

<body>
    <input type='button' value="子元素选择器" onclick="t1()"/><br/>
     <form>
          姓名:<input type="text" name="name"/><br/>
          年龄:<input type="text" name="age"/><br/>
          性别:<input type="radio" name="sex"value="男"/> 
          <input type="radio" name="sex" value="女"/>女
          <input type="radio" name="sex" value="妖"/>妖<br/>
          爱好:
          <input type="checkbox" name="hobby[]" value="读书"/>读书
           <input type="checkbox" name="hobby[]"value="写诗"/>
           <input type="checkbox" name="hobby[]"value="学习"/>
           <input type="checkbox" name="hobby[]"value="运动"/>
           <input type="checkbox" name="hobby[]"value="唱歌"/>唱歌<br/>
           介绍 ：
            <textarea cols="20" rows="5"></textarea>
            <input type="submit" value="提交"/>      
     </form>
</body>
```

##	9、变淡属性的选择器

：enable：匹配所有可用属性

：disable：匹配所有不可用元素

：checked：匹配复选框单选框所有选中的元素(问题多)

：selected：匹配下拉选框所有选中元素

#	DOM对象与jquery对象

dom对象和jquery对象不是一回事

##	什么是dom对象

使用document.getElementById或document.getElementsByTagName获取的对象就是dom对象

##	什么是jquery对象

使用$符号选择的元素就是jquery对象



**$(‘div’)里面，包含div的dom对象的，jquery对象是对dom对象的重新封装，他们之间是可以相互转换的**

##	jquery对象与DOM对象相互转换

**jquery对象的实质就是一个数组，每个数组元素本质就是一个DOM对象**

###	jquery对象转换成dom对象

DOM对象 = jquery对象[下标]；

DOM对象 = jquery对象.get(下标)；

###	把dom对象转换成jquery对象

jquery对象 = $(DOM对象); 

##	jquery中的属性

###	attr属性

attr(name)：获取指定元素的属性

attr(key,value)：设置元素的属性

attr(object)：为元素同时设置多个属性，要求参数是一个json数据

attr(key,fn)：通过函数的返回值设置元素属性

removeAttr(name)：移除元素属性

###	class属性

addClass(class)：为元素添加class属性

removeClass(class)：移除元素的class属性

toggleClass(class)：切换样式，如果元素不存在该属性则添加，否则移除

hasClass(class)：判断元素是否具有某个css类样式

###	css方法

**通过css方法添加的样式是行内样式**

css(name)：获取元素样式属性

css(name,value)：设置元素样式属性

css(object)：同时为元素设置多个样式属性，要求参数是一个object数据

###	offset位置

offset()：获取元素的位置，返回json格式数据，带有left与top属性

offset(coordinates)：设置元素的位置，要求参数是一个json数据且必须要拥有left与top属性

###	元素的尺寸

width()：获取元素的宽度

width(value)：设置元素的宽度

height()：获取元素的高度

height(value)：设置元素的高度

###	文本域值

相当于以前的innerHTML属性

html()：获取元素的值

html(val)：设置元素的值

```
<script. src="script/jquery-1.8.3.js"></script>
<script>
function t1(){
    //获取元素的文本
    console.log($('#one').html());
}
function t2(){
    //设置元素文本
    $("#one").html("<strong>你好</strong>");
}
</script>

<style type="text/css">
#one{width:150px;height:150px;border:1px solid red;}
</style>

<body>
    <input type="button" value="获取元素文本内容" onclick="t1()"/>
    <input type="button" value="设置元素文本内容" onclick="t2()"/>
    <div id="one"><a>今天很暖和</a></div>
</body>
```

相当于以前的value属性

val()：获取表单元素的值

val(val)：设置表单元素的值

```
<script src="./jquery-1.8.3.js"></script>
<script>
function t1(){
    //获取表单域里面的值
   console.log($('input[name=username]').val());
}
function t2(){
    //设置表单域里面的值
  $('input[name=username]').val('请求输入你的姓名')
}
</script>


<body>
    <input type="button" value="获取表单域文本" onclick="t1()"/>
    <input type="button" value="设置表单域文本" onclick="t2()"/>
    <input type="text" name="username"/>
</body>
```

相当于以前的innerText属性

text()：获取元素的值

text(val)：设置元素的值

```
<script src="./jquery-1.8.3.js"></script>
<script>
function t1(){
    //获取表单域里面的值
    console.log($('div').text());
    console.log($('div').html());
}
function t2(){
    //获取表单域里面的值
    $("#one").html("<font color='red'>大家好</font>");
    $("#two").text("<font color='red'>大家好</font>");
}
</script>

<body>
    <input type="button" value="获取文本" onclick="t1()"/>
    <input type="button" value="设置文本" onclick="t2()"/>
    <div id="one"><a>你好</a></div>
    <div id="two"></div>
</body>
```

##	jquery中的事件

在原生javascript代码中，我们通过window.onload实现页面的在日功能，其主要执行流程如下：载入HTML代码到内存->形成DOM树->载入全部资源（文本、图片、样式）->执行javascript脚本

通过jquery中的ready方法实现页面的载入功能

###	语法

语法1：

$(document).ready(function(){

​	//事件的处理程序

})；

语法2：

$(function(){

​	//事件的处理程序

});

语法3：

$().ready(function(){

​	//事件的处理程序

})；

###	window.onload与raedy区别

ready方法执行流程如下：载入HTML代码到内存中->形成DOM树结构->执行jquery脚本->载入全部资源(文本、图片、样式)



在原生javascript代码中，我们通过window.onload实现页面的在日功能，其主要执行流程如下：载入HTML代码到内存->形成DOM树->载入全部资源（文本、图片、样式）->执行javascript脚本



**通过比较，ready方法的执行速度要快于window.onload方法，原因在于两者执行的顺序不同，资源的载入是非常大的，需要消耗大量的事件，jquery先执行完脚本以后再载入资源，这是优化的过程**

##	常用事件

jquery对象.事件(事件的程序)

blur(fn)：失去焦点时触发

change(fn)：状态改变时触发

click(fn)：点击时触发

dblclick(fn)：双击时触发

focus(fn)：获得焦点时触发

keydown(fn)：键盘按下时触发

keyup(fn)：键盘弹起时触发

keypress(fn)：键盘按下时触发

load(fn)：页面载入时触发，功能与ready类似

unload(fn)：页面关闭时触发

mousedown(fn)：鼠标按下时触发

mouseup(fn)：鼠标弹起时触发

mousemove(fn)：鼠标移动时触发

mouseover(fn)：鼠标悬浮时触发

mouseout(fn)：鼠标离开时触发

resize(fn)：调整大小时触发

scroll(fn)：滚动时触发

select(fn)：文本选中时触发

submit(fn)：表单提交时触发

**和原生的比较，是没有on的**

jquery对象.事件的类型(function(){

​	//处理程序

});

###	事件的切换

hover(over.out)：鼠标悬浮于鼠标离开事件

over：鼠标悬浮事件

out：鼠标离开事件

toggle()方法切换元素的可见状态

speed：可选，规定元素从可见到隐藏的速度，默认为0，如果设置此参数，则无法使用weitch参数

callback：可选，toggle函数执行完之后要执行函数，除非设置了speed参数，否则不能设置该参数

switch：可选，布尔值，规定toggle是否隐藏或显示所有被选元素，True->显示所有元素    False->隐藏所有元素

如果设置此元素，则无法使用speed和callback参数

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      //单击button时，如果img显示就隐藏，如果隐藏就显示
      $('#btn').click(function(){
            $('img').toggle(1500);
        });
});
</script>

<body>
    <input type="button" value="显示隐藏" id="btn"/><br/>
    <img src="one.jpg" width="400" height="400"/>
</body>
```













































































































































































































































































































































































































































































































