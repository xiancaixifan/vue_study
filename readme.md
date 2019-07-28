# 笔记总纲:2019-7-29/00:31
# Table of Contents

* [使用到的指令](#使用到的指令)
  * [一.起步](#一起步)
    * [1.1 vue是响应式的](#11-vue是响应式的)
    * [1.2 绑定vue成员变量到dom属性](#12-绑定vue成员变量到dom属性)
    * [1.3 条件](#13-条件)
    * [1.4 遍历循环](#14-遍历循环)
    * [1.5 事件监听器](#15-事件监听器)
    * [1.6 即时数据渲染](#16-即时数据渲染)
    * [1.7 组件](#17-组件)
      * [1.7.1 非动态组件](#171-非动态组件)
      * [1.7.2 动态参数绑定](#172-动态参数绑定)
  * [二. Vue 实例](#二-vue-实例)
    * [2.1 Vue对象的初始化](#21-vue对象的初始化)
    * [2.2 获取Vue本身的属性和方法](#22-获取vue本身的属性和方法)
  * [三.Vue语法特性 Vue本生的API](#三vue语法特性-vue本生的api)
    * [3.1 文本渲染](#31-文本渲染)
    * [3.2 DOM对象渲染](#32-dom对象渲染)
    * [3.3 动态绑定标签属性](#33-动态绑定标签属性)
    * [3.4 使用JavaScript 表达式](#34-使用javascript-表达式)
  * [四.计算属性和侦听器](#四计算属性和侦听器)
    * [4.1 计算属性](#41-计算属性)
      * [4.1.2 计算属性的getter/setter](#412-计算属性的gettersetter)
    * [4.2 侦听属性](#42-侦听属性)
  * [五.绑定Class和Style](#五绑定class和style)
    * [5.1 对象语法](#51-对象语法)
  * [5.2 Class绑定语法使用计算属性](#52-class绑定语法使用计算属性)
    * [5.3 数组语法](#53-数组语法)
    * [5.4 行内样式绑定](#54-行内样式绑定)


> 2019-7-23 vue学习仓库创建,该文件用于记录笔记	=-

# 使用到的指令
- v-bind 为DOM的属性动态渲染值 
- v-if   判定条件,根据条件来决定 移除/插入元素
- v-for  遍历Vue中属性,没有一次遍历便可以 插入一次元素
- v-on   为DOM标签的事件绑定Vue函数,其一般为动态内容,绑定的是函数,如blur,onchange,click等
- v-model 为DOM即时渲染数据
- v-once 大括号内容不会随着Vue改变,其中内容只会渲染一次
- v-html 将文本渲染为DOM对象插入到HTML中
- v-bind:[property]="$data" 动态选择属性进行赋值
- 组件

```javascript
Vue.component('组件名称',{
	[props:[组件参数名称]],
	templaet:"组件模板"
	})
```
- 缩写
 - v-bind可缩写为 `:`
 - v-on可缩写为 `@`


## 一.起步
### 1.1 vue是响应式的
```javascrip

	<!DOCTYPE html>
	<html>
		<head>
			<meta charset="utf-8">
			<title></title>
		</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
		<body>
			<div id="app">
				{{message}}
			</div>
		</body>
		
		<script type="text/javascript">
			var app = new Vue({
				<!-- el:定义要被vue渲染的dom容器  -->
				el:"#app",
				<!-- data:vue对象全局可使用的参数 -->
				data:{
					message:"hello vue"
				}
			})
		</script>
	</html>
		<!-- 参数即时修改，前端及时响应变更 -->

```


### 1.2 绑定vue成员变量到dom属性

> v-bind 是绑定指令, 所有以 v- 为前缀的都是指令
>  
> **他们会在DOM上渲染特殊的 `响应式行为`(数据变化时可自动更新数据)**


```javascript
<!DOCTYPE html>
<html>
<head>
	<title></title>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	
</head>
	<body>
		<div id="app">
			<!-- 这段组合代码作用是在文字上鼠标悬浮展示message的值 -->
			<!-- 其中 v-bind 可以省略,直接通过title="message"的方式可以达到同样的效果 -->
			<span v-bind:title="message">
				鼠标悬浮展示
			</span>
		</div>
	</body>
	<script type="text/javascript">
		var app = new Vue({
			el:"#app",
			data:{
				message:"hello vue"
			}
		});
		
	</script>
</html>
```

### 1.3 条件
```JavaScript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<button type="button" @click="turn">开关</button>
			<!-- if中的条件为Boolean类型,和js中的if()相同 -->
			<span v-if="seen">看到我了吗</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				seen:false
			},
			methods:{
				turn(){
					this.seen = this.seen?false:true;
				}
			}
		})
	</script>
</html>
```


### 1.4 遍历循环


```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
			<div id="app">
				<!-- 遍历个数,每有一个元素就会有一组<li>生成 -->
				<li v-for="item in items">
					<!-- 元素中,可使用当前遍历位置对象的属性 -->
					{{item.text}}
				</li>
			</div>
	</body>
	<script type="text/javascript">
		 new Vue({
			el:"#app",
			data:{
				items:[
					{text:"笔记记录"},
					{text:"github"},
					{text:"xiancaixifan"}
				]
			}
		})
	</script>
</html>
```


### 1.5 事件监听器
> v-on 为DOM渲染响应式的事件
> 
> v-bind,为DOM属性绑定Vue属性,v-on是为DOM事件赋值一个Vue函数

```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<p>{{message}}</p>
			<button v-on:click="reverseMessage">吃吧</button>
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"Xian Cai Xi Fan 好吃哦"
			},
			methods:{
				    reverseMessage() {
						this.message = this.message.split('').reverse().join('');
					}
			}
		})
	</script>
</html>
```



### 1.6 即时数据渲染
```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 文本框中输入任意数据,下方立刻动态渲染改动数据 -->
			<input type="text" v-model="message">
			<br>
			{{message}}
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:""
			}
		})
	</script>
</html>
```

### 1.7 组件
#### 1.7.1 非动态组件

```javascript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<ol>
				<todo-item v-for="obj in lists" v-bind:title="obj.id">
					{{obj.item}}
				</todo-item>
			</ol>
		</div>
	</body>
	<script type="text/javascript">
		
	Vue.component('todo-item', {
		<!-- 组件元素内部的信息为定死的,不许要修改, -->
		template: '<li>这是个待办项</li>'
	})
		
		var app = new Vue({
			el:"#app",
			data:{
				
				lists:[
					{id:1,item:"第一个参数"},
					{id:2,item:"第二个参数"},
					{id:3,item:"第三个参数"},
					{id:4,item:"第四个参数"},
					{id:5,item:"第五个参数"},
					{id:6,item:"第六个参数"},
				]
			}
		})
	</script>
</html>
```


#### 1.7.2 动态参数绑定
```JavaScript
<!DOCTYPE html>
<html>
	<head>
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			<ol>
				<todo-item 
				v-for="obj in lists" 
				v-bind:param="obj"
				v-bind:key="obj.id"
				v-bind:title="obj.id"></todo-item>
			</ol>
		</div>
	</body>
	<script type="text/javascript">
		<!-- 在组件中定义好参数的,在元素中将Vue对象中的属性传递到组件参数中,
		实现动态生成 -->
		<!-- 类似于一种函数,调用方法的传参 -->
	Vue.component('todo-item', {
		props:["param"],
		template: '<li>{{param.item}}</li>'
	})
		
		var app = new Vue({
			el:"#app",
			data:{
				lists:[
					{id:1,item:"第一个参数"},
					{id:2,item:"第二个参数"},
					{id:3,item:"第三个参数"},
					{id:4,item:"第四个参数"},
					{id:5,item:"第五个参数"},
					{id:6,item:"第六个参数"},
				]
			}
		})
	</script>
</html>
```


> part1 起步


## 二. Vue 实例
### 2.1 Vue对象的初始化

> 在Vue对象初始化完成时, vm.a = 1 此时若修改datas.a的值,那么vm.a的值也会响应变化,反之亦然

> Vue对象初始化完成后,在datas中添加属性b 如:datas.b=1, Vue对象无法渲染到b, vm.b=underfine

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		<div id="app">
			
		</div>
	</body>
	<script type="text/javascript">
		var datas = {a:1};
		
		// Vue实例可以直接访问data中的属性,data为其成员变量
		// vm.a = 1; 相当于 data.a
		var vm = new Vue({
			data:datas
		})
		
	</script>
</html>

```

> 上面的例子中,如果有些属性是后期将要用到的,可以现在data中初始化,

```javascript
//初始化变量,方便后期使用
	data:{
		b:"",
		a:datas.a,
		todo:[],
		isOk:false
	}
```

> Object.freeze() 冻结一个对象,使该对象无法在被修改,则Vue将无法起到响应式的作用

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<button type="button" @click="changeMessage">改变</button>
			<input type="text" v-model="message">
		</div>
	</body>

	<script type="text/javascript">
		var datas = {
				message: "你动我试试"
			}
			
		// 点击按钮会报错,因为datas对象无法修改,是只读的
		Object.freeze(datas);
			new Vue({
				el: "#app",
				data: datas,
				methods:{
					changeMessage(){
						this.message="试试就试试"
					}
				}
			})
	</script>
</html>


```


### 2.2 获取Vue本身的属性和方法
> Vue的实例暴露了一些有用的实例属性和方法, 用$作为前缀
[vue-api](https://cn.vuejs.org/v2/api/#%E5%AE%9E%E4%BE%8B%E5%B1%9E%E6%80%A7)

## 三.Vue语法特性 Vue本生的API
### 3.1 文本渲染
> `{{obj}}` , 学名 Mustache,无论何时,Vue对象中的obj参数发生了变化,对应大括号内渲染的值都会随之变化

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	<body>
		
		<div id="app">
			
			//点击按钮自动动态渲染
			<span>{{message}}</span>
			<br>
			//只会渲染一次,后续不再改变
			<span v-once>{{message}}</span>
			<button @click="changeMessage">改变</button>
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"动态渲染的参数",
				num : 0
			},
			methods:{
				changeMessage(){
					this.num++;
					this.message = '变化了'+this.num+'下';
				}
				
			}
			
		})
	</script>
</html>

```


### 3.2 DOM对象渲染
> `Mustache`只可渲染普通文本
> 如果要渲染DOM对象到HTML,类似append的操作,则要使用`v-html`

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<span>普通大括号渲染效果:</span>{{dom1}}<br />
			
			<span>v-html 渲染效果:</span><span v-html="dom1"></span>
		</div>
		
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				dom1:"<a href='https://www.baidu.com'>点击进入百度</a>"
			}
			
		})
		
	</script>
</html>
```


### 3.3 动态绑定标签属性
> 动态的 可通过Vue对象来选择DOM属性 并进行配置

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<span v-bind:title="message">鼠标悬浮查看title</span>
			<br><br>
			<span v-bind:[property]="message">鼠标悬浮查看title</span>
			
		</div>
	</body>
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"我是悬浮文字",
				property:"title"
			}
		})
	</script>
</html>

```

> 浏览器会默认的将标签上的属性转为小写,所以在定义property的时候要注意设置参数为小写


### 3.4 使用JavaScript 表达式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			数字表达式:{{number+1}}<br />
			布尔类型操作:{{isok?"yes":"no"}}<br />
			字符类型操作:{{str.split('').reverse().join('') }}
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				number:"100",
				isok:false,
				str:"旋转跳跃"
			}
		})
	</script>
</html>

```

## 四.计算属性和侦听器

### 4.1 计算属性
> 属性计算,就是对参数进行Javscript运算

> 计算属性类似于一个funcation,和函数不同的地方在于它拥有缓存,不需要每次使用都重新计算

> 但运算在`{{}}`中使用复杂的时候,就推荐使用计算属性,将计算过程放到后台,而不是`渲染过程` 中

```html

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<input type="text" v-model="message"><br>
			<span>{{message}}</span><br>
			<span>{{resersedMessage}}</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				message:"信息文字"
			},
			computed:{
				//计算属性的getter
				//计算属性也算是属性,调用的时候不需要加( )
				//计算属性里面的其他属性值,就是`this.xxx`,会自动监听,一但其中数值发生变化,计算属性也会重新计算
				//如果其他属性没有变化,计算属性不会重新计算,并且一直缓存着
				resersedMessage:function(){
					//this只想当前Vue实例
					return this.message.split('').reverse().join('');
				}
			}
		})
	</script>
</html>


```


#### 4.1.2 计算属性的getter/setter

> 计算属性默认放出的是一个get接口,如例 4.1 中的代码
> 也可以手动声明一个set,其将在被指定参数被赋值后调用

> 如果使用了set,那么该侦听属性不能存在于data中进行初始化

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>计算属性的getter和setter</title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<button @click="messageSet">setter</button>
			<br>
			getter: <input type="text" :value="message">
			
			<br>
			
			{{target}}
		</div>
	</body>
	
	<script type="text/javascript">
		var vm = new Vue({
			el:"#app",
			data:{
				target:'q'
			},
			computed:{
				message:{
					get:function(){
						return this.target = 'message的get方法调用'
					},
					set:function(){
						return this.target = 'message的set方法调用'
					}
				}
			},
			methods:{
				messageSet(){
					this.message = '重新赋值'
				}
			}
		})
	</script>
</html>

```


### 4.2 侦听属性
> 案例中侦听了firsttitle属性,在侦听调用方法中不能给firstitle进行任何赋值,不然会造成监听死循环

```html

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<input type="text" v-model="firsttitle">
			<span>{{firsttitle}}</span>
			<span>{{secondtitle}}</span>
		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				firsttitle:"a",
				secondtitle:"b"
			},
			watch:{
				firsttitle:function(val){
					this.secondtitle = val + this.secondtitle;
				}
				
			},
			
		})
	</script>
</html>


```

## 五.绑定Class和Style
### 5.1 对象语法
> 给`:class`一个对象,可动态切换clss
> 
> 绑定一个Class 首先需要该CSS存在
>
> 绑定语法可以决定是否使用该CSS

```HTML

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>

	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}

		.class1 {
			background-color: lightgoldenrodyellow;
		}
		.class2{
			background-color: red;
		}
	</style>
	<body>
		<div id="app">
			<!-- 不需要动态绑定的直接引入 -->
			<div class="static">
				a
			</div>
			<hr />
			<button @click="changehasError">点击修改hasError的值</button>
			<div class="static" :class="{class1:isActive,class2:hasError}">
				b
			</div>
		</div>
	</body>

	<script type="text/javascript">
		let vm = new Vue({
			el: "#app",
			data: {
			 isActive: true,
			  hasError: false
			},
			methods:{
				changehasError(){
					this.hasError = !this.hasError
				}
			}
		})
	</script>
</html>

```

## 5.2 Class绑定语法使用计算属性
```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
		<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}
	
		.class1 {
			background-color: lightgoldenrodyellow;
		}
		.class2{
			background-color: red;
		}
	</style>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 不需要动态绑定的直接引入 -->
			<div class="static" :class="ClassObject">
				a
			</div>

		</div>
	</body>
	
	<script type="text/javascript">
		new Vue({
			el:"#app",
			data:{
				
			},
			computed:{
				ClassObject:function(){
					return {
						class1:true
					}
				}
			}
		})
	</script>
</html>

```


### 5.3 数组语法
> 给 `:class`传递一个数组,应用一个样式列表

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>
	<style type="text/css">
		.static {
			width: 12.5rem;
			height: 12.5rem;
			background-color: lightblue;
		}

		.class1 {
			background-color: lightgoldenrodyellow;
		}

		.class2 {
			background-color: red;
		}
	</style>
	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

	<body>
		<div id="app">
			<!-- 通过isActive的属性值来判定是否添加class1样式 -->
			<div  :class="[staticObject,isActive?classObject:'']">
				a
			</div>
			
			<hr>
			<!-- 同样,上面的表达式也可以使用对象语法 -->
			<div  :class="[staticObject,{classObject:isActive}]">
				a
			</div>
		</div>
	</body>

	<script type="text/javascript">
		let vm = new Vue({
			el: "#app",
			data: {
				isActive:true,
				classObject:"class1",
				staticObject:"static"
			}
		})
	</script>
</html>

```




### 5.4 行内样式绑定
> 基本上和Class绑定的通用,但是有一些问题需要注意,详将如下

```HTML
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title></title>
	</head>

	<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
	
	<body>
		<div id="app">
			<!-- 单个样式绑定 -->
			<div :style="{color:activeColor,fontSize:activeFont}">a</div>
			<hr >
			<!-- 绑定一组样式,有些样式不支持,比如background-color-->
			<div :style="styleObject">b</div>
			
		
			
			
			
		</div>
	</body>

	<script type="text/javascript">
		new Vue({
			el: "#app",
			data: {
				activeColor:"red",
				activeFont:"20px",
				styleObject:{
					width: "12.5rem",
					height: "12.5rem",
					/* vue应该是有bug,没办法识别 -  */
					// background-color: "lightgoldenrodyellow",
					// font-style: oblique,
					color:"yellow"
				}
			}
		})
	</script>
</html>

```
