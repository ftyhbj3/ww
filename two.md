#	jquery

##	事件编程

###	绑定事件

bind(type,[data],fn)；为元素绑定相关的事件处理程序

type：事件类型，不带on前缀

[data]：可选参数，事件发生所传递的数据（了解）

fn：事件的处理程序

```
<script src="./jquery-1.8.3.js"></script>
<script type="text/javascript">
$(function(){
        $(":button").bind('click',function(){
                    alert('hello python');
        });
         $(":button").bind('click',function(){
                    alert('hello jquery');
        });

});
</script>

<body>
    <input type="button" value="绑定事件"/>
</body>
```

one(type,[data],fn)：为元素绑定事件，但事件只触发一次

type：事件类型

[data]：事件发生是所传递的数据

fn：事件的处理程序

```
<script src="./jquery-1.8.3.js"></script>
<script>
	$(function(){
        //给button绑定一次性单击事件，
        $("input[type=button]").one('click',function(){
                   alert('现在开始考试了，请把手机扔出教室');
        });
});
</script>

<style type="text/css">
	div{width:400px;height:200px;background:gold;}
</style>

<body>
    <input type="button" value="开始考试" />
</body>
```

###	移除事件

unbind([type])

type：要移除的事件类型

在原生javascript代码中，如果想要进行事件移除，那么必须有一个前提：在事件绑定时，必须为事件的处理程序名

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
     //给div绑定三个事件，一个是鼠标滑过，一个是鼠标离开，一个是单击事件
      $("div").bind({'mouseover':function(){
            $('span').html('你来了');
            },'mouseout':function(){
            $('span').html('你走了');
            },'click':function(){
            $('span').html('你敢点我');
        }});
        $(":button:eq(0)").click(function(){
            //给div移除单击事件
            $('div').unbind('click');
        });
        $(":button:eq(1)").click(function(){
            //给div移除所有事件
            $('div').unbind();
        });
});
</script>

<style type="text/css">
div{width:400px;height:200px;background:gold;}
</style>

<body>
     <input type="button" value="移除单击事件"/>
     <input type="button" value="移除所有事件"/>
     <div></div>
     <span></span>
</body>
```

##	事件绑定中的this对象

在javascript代码中，事件监听中的this指向：

IE5/6：指定Window对象

W3C：指向当前要操作的DOM对象

**jquery绑定事件中的this是指dom对象**

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      //可以给表单绑定一个submit事件。
      //原生态方式获取button对象
      var oBtn = document.getElementById('btn');
      console.log(oBtn);
      $("#btn").click(function(){
           console.log(this);
        });
});
</script>

<style type="text/css">
	#one{width:300px;height:200px;background:gold;}
</style>

<body>
    <input type="button" value="单击" id="btn"/>
    <div id="one">西游记,大话西游</div>
</body>
```

##	基本动画

show()：显示

show(speed,[callback])：以动画效果显示

speed：速度(动画的持续时间)

[callback]：可选参数，事件完成时所触发的回调函数



hide()：隐藏

hide(speed,[callback])：以动画效果隐藏

speed：速度(动画的持续时间)

[callnack]：可选参数，时间完成市所触发的回调函数



toggle()：切换显示或隐藏

toggle(switch)：显示或隐藏true：显示false：隐藏

toggle(speed,[callback])：以动画效果切换显示或隐藏

speed：‘slow’，‘normal’，‘fast’；slow：慢，normal：正常，fast：快速

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      //给隐藏按钮绑定事件
      $(":button:eq(0)").bind('click',function(){
             $('img').hide(1000,function(){alert('我走了')});
        });
       //给显示按钮绑定事件
       $(":button:eq(1)").bind('click',function(){
             $('img').show(1000,function(){alert('我来了')});
        });
        //给切换显示隐藏按钮绑定事件
        $(":button:eq(2)").bind('click',function(){
             $('img').toggle(1500);
        });
});
</script>

<body>
    <input type="button" value="隐藏"/><input type="button" value="显示"/>
    <input type="button" value="切换显示隐藏"/><hr/>
     <img src="one.jpg" width="400"/>
</body>
```

###	滑动效果

slideDown(speed,[callback])：以动画的效果向下滑动显示

slideUp(speed,[callback])：以动画效果向上滑动隐藏

slideToggle(speed,[callback])：以动画效果滑动显示或隐藏

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
       //给隐藏按钮绑定事件
       $(":button:eq(0)").bind('click',function(){
             $('img').slideUp('normal',function(){alert('我走了')});
        });
        //给显示按钮绑定事件
        $(":button:eq(1)").bind('click',function(){
             $('img').slideDown('normal',function(){alert('我来了')});
        });
        //给切换显示隐藏按钮绑定事件
        $(":button:eq(2)").bind('click',function(){
              $('img').slideToggle('slow');
        });
});
</script>

<body>
    <input type="button" value="隐藏"/><input type="button" value="显示"/>
    <input type="button" value="切换显示隐藏"/><hr/>
     <img src="one.jpg" width="400" height="300"/>
</body>
```

###	淡入淡出效果

fadeIn(speed,[callback])：以动画形式淡入(显示)

fadeOut(speed,[callback])：以动画形式淡出(隐藏)

speed：动画的持续时间

[callback]：动画完成时所触发的回调函数

fadeToggle()切换淡入淡出

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
       //给隐藏按钮绑定事件
       $(":button:eq(0)").bind('click',function(){
             $('img').fadeOut(2000);
        });
        //给显示按钮绑定事件
        $(":button:eq(1)").bind('click',function(){
             $('img').fadeIn(2000);
        });
        //给切换显示隐藏按钮绑定事件
        $(":button:eq(2)").bind('click',function(){
             $('img').fadeToggle('slow');
        });
});
</script>

<body>
    <input type="button" value="淡出"/><input type="button" value="淡入"/>
    <input type="button" value="切换淡入淡出"/><hr/>
    <img src="one.jpg" width="400" height="300"/>
</body>
```

###	设置元素的透明度

speed：动画的持续时间

opacity：透明度(0-1)；0全透明；1不透明

[callback]：动画完成时所触发的回调函数

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
       //给隐藏按钮绑定事件
       $(":button:eq(0)").bind('click',function(){
             $('img').fadeTo(2000,0.5);
        });
});
</script>

<body>
    <input type="button" value="透明度设置"/><br/>
    <img src="one.jpg" width="400" height="300"/>
</body>
```

###	自定义动画

animate(params,[speed])：自定义动画效果

parmas：自定义动画，要求参数是一个json格式的数据

[speed]：动画的持续时间

```
<script src=".jquery-1.8.3.js"></script>
<script>
$(function(){
      //给隐藏按钮绑定事件
      $(":button:eq(0)").bind('click',function(){
            $('img').fadeTo(2000,0.5);
        });
});
</script>

<body>
    <input type="button" value="透明度设置"/><br/>
    <img src="one.jpg" width="400" height="300"/>
</body>
```

#	在元素内部插入dom元素

##	在元素内部后面插入

A.append(B)：将B插入到A的内部的后面

B.appendTo(A)：将B插入到A的内部的后面

```
<script src = "./jquery-1.8.3.js"></script>
<script>
	$(function(){
		$(':button:eq(0)').click(function(){
			   //把"大话西游"文本插入到div内部的后面，
               //$("#one").append('大话西游');
               //把原来p标签插入到div内部的后面
               //$("#one").append($('p'));
               //把新建strong标签插入到 div内部的后面
               $("#one").append($('<strong>三打白骨精</script>
		});
	});
</script>
<style type='text/css'>
*{margin:0;padding:0;list-style:none}
#one{width:200px;height:200px;background:gray;}
<style>

<body>
	<input type="button" value="在div里面后面添加内容"/>
    <div id="one">西游记之-</div>
    <p>降魔篇</p>
</body>
```

##	在元素内部前面插入

A.prepend(B)：将B插入到A的内部的前面

B.prependTo(A)：将B插入到A的内部的前面

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
     $(":button:eq(0)").click(function(){
           //把div里面前面添加文本，文本内容是：今天晚上上映
           //$("#one").prepend('今天晚上上映');
           //把p标签添加到div里面前面
           //$("#one").prepend($('p'));
             $('p').prependTo($('#one'));
           //新建一个strong标签，添加到div里面的前面。
             $("<strong>今天隆重上映</strong>").prependTo
($('#one'));
       });
});
</script>

<style type="text/css">
*{margin:0;padding:0;list-style:none}
#one{width:200px;height:200px;background:gray;}
</style>

<body>
    <input type="button" value="在div里面前面添加内容"/>
    <div id="one"> 《西游记》</div>
    <p>降魔篇</p>
</body>
```

#	在元素外部插入dom元素

##	在元素外部的后面

A.after(B)：将B插入到A的外面的后面

B.insertAfter(A)：将B插入到A的外面的后面

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      $(":button:eq(0)").click(function(){
            $("li:first").after('<li>西瓜刀</li>');
       });
            $(":button:eq(1)").click(function(){
                $('<li>指甲剪</li>').insertAfter ("li:contains('屠龙刀')");
       });
});
</script>

<body>
    <input type="button" value="在第一个li后面添加一个li标签"/>
    <input type="button" value="在屠龙刀li后面添加一个li标签"/><br/>
    <ul>
            <li>倚天剑</li>
            <li>屠龙刀</li>
            <li>诛仙剑</li>
            <li>捆仙绳</li>
            <li>水果刀</li>
    </ul>
</body>
```

在元素外部的前面

A.before(B)：将B插入到A的外面的前面

B.insertBefore(A)：将B插入到A的外面的前面

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      $(":button:eq(0)").click(function(){
            $("li:first").before('<li>西瓜刀</li>');
       });
      $(":button:eq(1)").click(function(){
          //$("li:contains('屠龙刀')").before('<li>指甲剪</li>');
            $("<li>铅笔刀</li>").insertBefore($( "li:
contains('屠龙刀')"));
       });
});
</script>

<body>
    <input type="button" value="在第一个li前面添加一个li标签"/>
    <input type="button" value="在屠龙刀li前面面添加一个li标签"/><br/>
    <ul>
            <li>倚天剑</li>
            <li>屠龙刀</li>
            <li>诛仙剑</li>
            <li>捆仙绳</li>
            <li>水果刀</li>
    </ul>
</body>
```

#	删除操作

empty()：清空元素内容

remove：删除元素节点及内容

```
<script src="./jquery-1.8.3.js"></script>
<script>
$(function(){
      $(":button:eq(0)").click(function(){
            $("li:first").empty();
       });
       $(":button:eq(1)").click(function(){
            $("li:first").remove();
       });
});
</script>

<body>
    <input type="button" value="删除第一个li标签的内容"/>
    <input type="button" value="删除第一个li标签"/><br/>
    <ul>
            <li>倚天剑</li>
            <li>屠龙刀</li>
            <li>诛仙剑</li>
            <li>捆仙绳</li>
            <li>水果刀</li>
    </ul>
</body>
```

##	复制操作

clone()：克隆（复制）元素

clone(true)：克制（复制）元素同时复制元素的事件

```
<script>
$(function(){
      $(":button:eq(0)").click(function(){
             //$("ul").append($("li:first"));//直接把"li:first"给移动到ul里面最后的位置。
             var new_li = $("li:first").clone(true);
             $("ul:eq(0)").append(new_li);

       });
       $('li:eq(0)').click(function(){
             alert('爱琴海!')
    })
});
</script>

 <body>
    <input type="button" value="复制第一个li,添加到ul的后面"/>
    <ul>
            <li>倚天剑</li>
            <li>屠龙刀</li>
            <li>诛仙剑</li>
            <li>捆仙绳</li>
            <li>水果刀</li>
    </ul>
</body>
```

##	替换操作

值替换    html():

节点(标签)替换：replaceWith():

##	包裹操作

用新的标签把原来的标签包裹起来

wrap()：对每一个元素进行单独包裹

##	查找操作

eq(index)：通过元素的索引查找元素，index默认从0 开始

filter(expr)：查找与给定元素匹配的元素，expr匹配条件

not(expr)：查找与给定元素不匹配的元素

children([expr])：查找所有子元素

find(expr)：查找所有后代元素

next([expr])：查找紧邻的下一个元素

nextAll();查找紧邻的后面的所有元素

prev([expr])：查找紧邻的上一个元素

prevAll();查找紧邻的前面的所有元素

parent([expr])：查找当前元素的父元素

siblings([expr])：查找所有同级兄弟节点（无论上下）





















































































































































































































