#	Vue

##	事件修饰符

**事件冒泡**
v-on:click.stop     停止事件冒泡
v-on:click.self     不参加事件冒泡
v-on:click.once     点击一次自动解绑 
v-on:click.capture  事件捕获，添加以后可以先触发，从外到内
v-on:click.prevent  阻止默认行为

```
<script src="11.js">
			
		</script>
	</head>
	<body>
		<div id = 'app' style="width:300px;height:300px;background-color: blue;"v-on:click.self = 'one'>
		<div style="width:200px;height:200px;background-color: green;"@click.self ='two'>
		<div style="width:100px;height:100px;background-color: red;"@click.self ='three'>
		<a href="http://www.baidu.com" v-on:click.prevent="four">百</a>
		</div>
		</div>
		</div>
		<script>
			var app = new Vue({
				el:'#app',
				methods:{
					one(){
						alert(1);
					},
					two(){
						alert(2);
					},
					three(){
						alert(3);
					},
					four(){
						alert(4);
					},
				},
			});
		</script>
	</body>
```

##	class样式控制

###	vue的类样式

```
	<script src="11.js">
		</script>
		<style>
			.red{
				color:red;
			}
			.i{
				font-style: italic;
			}
			.strong{
				font-size:30px;
			}
			.spcing{
				letter-spacing:1rem;
			}
		</style>
	</head>
	<body>
		<div id = 'app'>
			<p class="red i">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :class="['red','i','strong']">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :class="[{'red':flag,'strong:flag'}]">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p class="style_">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<input type="button" value="点击" @click = 'action'/>
		</div>
		<script>
			var app = new Vue({
				el:'#app',
				data:{
					flag:true,
					style_:['red':this.flag,'i':this.flag],
				},
				methods:{
					action(){
						this.flag = !this.flag;	
					}
				},
			});
		</script>
	</body>
```

##	css样式控制

```
<script src="11.js"></script>
	</head>
	<body>
		<div id="app">
			<p style="color: red;">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :style="{color:'red'}">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :style="style1">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :style="[style1,style2]">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<p :style="[style3.one]">鱼和熊掌不可兼得，但单身和穷可以！</p>
			<input type="button" value="点击" @click = 'action'/>
		</div>
		<script>
			var app = new Vue({
				el:'#app',
				data:{
					style1:{color:'pink','letter-spacing':'1em'},
					style2:{'font-size':'30px'},
					style3:{
						one:{color:'pink','letter-spacing':'1em'},
						two:{'font-size':'30px'},
					},
				},
				methods:{
					action(){
						
					},
				},
			});
		</script>
	</body>
```

















