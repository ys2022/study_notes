# vue学习笔记
## 概念特点
数据=》界面，js框架，自顶向上
组件化：HTML+css+js的封装
声明式
虚拟dom：diff适用数据经常变化

##初识

1. 必须创建Vue实例
2. 再创建一个容器，div，可以混入一些vue的语法,比如插值语法：{{js表达式}}
   1. 表达式：生成一个值放到一个需要的地方
3. 容器中的代码在vue中称为模板
4. 容器和实例一对一关系
5. data数据一旦发生改变，模板中用到该数据的地方也会自动更新

##模板语法
`{{}}`——插值语法：对标签体写入，解析js表达式，可以读取到实例中的data的所有属性
`v-bind:` 和其替代`:`——指令语法:对标签属性动态写入，其他同插值语法，`v-bind`只是一种，还会有其他指令`v-xxxxx`

##代码示例
```html
    <body>
        <!--准备一个容器-->
        <div id="root">
            <h1>hello，{{name}}</h1>
            <h2>{{school.name}}</h2>
        </div>
        <button>click</button>

        <script type="text/javascript">
            Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
            const vm = new Vue({
                el:'#root',//指定实例为哪个容器服务
                data:{
                    name:'ys',
                    school:{
                        name:'666'
                    }}//data用于储存数据
            })
        </script>
    </body>
```

## 数据绑定
`v-bind`单向绑定，数据只能从示例到页面
`v-modle`双向绑定，只能用在表单类有输入的元素

```
双向数据绑定：<input type="text" v-model:value="name">
双向数据绑定：<input type="text" v-model="name">//简写
```


`v.$mount('#root')`等同于`el:'#root'`
data的第二种写法：
*注意由Vue管理的函数一定不能写箭头函数，this就不是Vue实例了*
```
data:function(){
    return{
        name:'asdasd'
    }
}
```

## mvvm模型——Vue设计受到启发
model：模型对应data的数据
view：view视图页面
viewmodel：视图模型（桥梁纽带）vue实例
data中所有属性最后都出现在了vm实例上
vm身上的所有属性甚至vm原型上的所有属性在vue模板中都可直接使用

## 数据代理
通过一个代理对象对另一个对象属性的操作，读或者写
vm较为底层的原理
代码示例
```html
        <script type="text/javascript">
            let number = 18
            let person = { 
                name: 'John',
                sex: 'male'
            }
            Object.defineProperty(person,'age',{
               /*  value:18,
                enumerable:true,  //控制属性是否可以被枚举
                writable:true,    //控制属性是否可以被修改
                configurable:true //控制属性是否可以被删除
                //当有人读取person的age属性时，get函数就会被调用，且返回值就是age的值 */
                get:function peiqi(){
                    return number
                },
                //当有人修改person的age属性时，set函数就会被调用，且返回值就是age的值
                set(value){
                    number = value
                }
            })
        </script>
```
## 事件处理
用v-on:xxxx 或 @xxxx都可以绑定事件
```html
    <body>
        <div id="root">
            <button v-on:click="shwoInfo">点我</button>
            //shwoInfo也可以加括号(6666,$event)$event：点击事件
        </div>

        <script type="text/javascript">
            const vm = new Vue({
                el:'#root',
                data:{name:'xxxx'},
                methods: {
                     shwoInfo(){
                         //此处的this是vm
                        alert('nihao')}}})
        </script>
    </body>
```
## Vue中的事件修饰符
    1.prevent：阻止默认事件（常用）
    2.stop：阻止事件冒泡（常用）
    3.once：事件只触发一次（常用）
    4.capture：使用事件的捕获模式
    5.self：只有event.target是当前操作的元素时才触发事件
    6.passive：事件的默认行为立即执行，无需等待事件回调执行完毕
 

1.常用按键别名：
    回车 => enter
    删除 => delete (捕获“删除”和“退格”键)
    退出 => esc
    空格 => space
    换行 => tab (特殊，必须配合keydown去使用)
    上 => up
    下 => down
    左 => left
    右 => right
2.未提供别名按键，可用按键原始的key值去绑定，但要转为kebab-case（短横线命名）
3.系统修饰键（用法特殊）：ctrl、alt、shift、meta
    (1).配合keyup使用：按下修饰键时，再按其他键，随后释放其他键，事件才触发。
    (2).配合keydown使用：正常触发事件。
4.也可用keyCode去指定具体的按键（不推荐）
5.Vue.config.keyCodes.自定义键名 = 键码，定制按键别名

示例
```HTML
	<body>
		<div id="root">
			<input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo">
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		Vue.config.keyCodes.huiche = 13 //定义了一个别名按键
		new Vue({
			el:'#root',
			methods: {
				showInfo(e){
					// console.log(e.key,e.keyCode)
					console.log(e.target.value)}},})
	</script>
```

## Vue.js 计算属性

计算属性关键词: computed。
计算属性：
1.定义：要用的属性不存在，要通过已有属性计算得来。
2.原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
3.get函数执行
    (1).初次读取时会执行一次。
    (2).当依赖的数据发生改变时会被再次调用。
4.优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
5.注：
    1.计算属性最终出现在vm上，直接读取使用即可。
    2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```html
<div id="app">
  <p>原始字符串: {{ message }}</p>
  <p>计算后反转字符串: {{ reversedMessage }}</p>
</div>
 
<script>
var vm = new Vue({
  el: '#app',
  data: {
    message: '666666'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }}})
</script>
```

## 监听属性

监视属性watch：
 1. 当被监视的属性变化时, 回调函数自动调用, 进行相关操作
 2. 监视的属性必须存在，才能进行监视！！
 3. 监视的两种写法：
   1. new Vue时传入watch配置
   2. 通过vm.$watch监视

```html
<div id = "app">
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button>
</div>
<script type = "text/javascript">
var vm = new Vue({
    el: '#app',
    data: {
        counter: 1
    }
});
vm.$watch('counter', function(nval, oval) {
    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
});
</script>
```

## 绑定样式
```html
    <div id="root">
        <!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
        <div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br/><br/>
        <!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
        <div class="basic" :class="classArr">{{name}}</div> <br/><br/>
        <!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
        <div class="basic" :class="classObj">{{name}}</div> <br/><br/>
        <!-- 绑定style样式--对象写法 -->
        <div class="basic" :style="styleObj">{{name}}</div> <br/><br/>
        <!-- 绑定style样式--数组写法 -->
        <div class="basic" :style="styleArr">{{name}}</div>
    </div>
</body>

<script type="text/javascript">
    Vue.config.productionTip = false
    
    const vm = new Vue({
        el:'#root',
        data:{
            name:'ysss',
            mood:'normal',
            classArr:['atguigu1','atguigu2','atguigu3'],
            classObj:{
                atguigu1:false,
                atguigu2:false,
            },
            styleObj:{
                fontSize: '40px',
                color:'red',
            },
            styleObj2:{
                backgroundColor:'orange'
            },
            styleArr:[
                {
                    fontSize: '40px',
                    color:'blue',
                },
                {
                    backgroundColor:'gray'
                }
            ]
        },
        methods: {
            changeMood(){
                const arr = ['happy','sad','normal']
                const index = Math.floor(Math.random()*3)
                this.mood = arr[index]
            }
        },
    })
</script>
```

## 条件判断 v-if

```html
<div id="app">
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    type: 'C'
  }
})
</script>
```

## 循环使用 v-for 指令。
v-for 指令需要以 site in sites 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。
v-for 可以绑定数据到数组来渲染一个列表：

```html
<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.name }}
    </li>
  </ol>
</div>
 
<script>
new Vue({
  el: '#app',
  data: {
    sites: [
      { name: 'Runoob' },
      { name: 'Google' },
      { name: 'Taobao' }
    ]
  }
})
</script>
```

## 过滤器：
定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
语法：
1. 注册过滤器：Vue.filter(name,callback) 或 new Vue{filters:{}}
2. 使用过滤器：{{ xxx | 过滤器名}}  或  v-bind:属性 = "xxx | 过滤器名"
备注：
1. 过滤器也可以接收额外参数、多个过滤器也可以串联
2. 并没有改变原本的数据, 是产生新的对应的数据
   
```html
<div id="app">
  {{ message | capitalize }}
</div>
<script>
new Vue({
  el: '#app',
  data: {
    message: 'runoob'
  },
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)}}})
</script>
```


## 组件化编程
局部组件、全局组件
1. 创建组件
2. 注册局部组件：new Vue时传入 components{}
3. 编写组件标签
4. 全局注册： Vue.component('组件别名'，组件名)
   
```html
		<div id="root">
			<hello></hello>
			<hr>
			<h1>{{msg}}</h1>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<school></school>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<student></student>
		</div>
		<div id="root2">
			<hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		//第一步：创建school组件，可简写：const school={}
		const school = Vue.extend({
			template:`
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>
					<button @click="showName">点我提示学校名</button>	
				</div>
			`,
			// el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
			data(){
				return {
					schoolName:'尚硅谷',
					address:'北京昌平'
				}
			},
			methods: {
				showName(){
					alert(this.schoolName)
				}
			},
		})
		//第一步：创建student组件
		const student = Vue.extend({
			template:`
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
			data(){
				return {
					studentName:'张三',
					age:18
				}
			}
		})
		
		//第一步：创建hello组件
		const hello = Vue.extend({
			template:`
				<div>	
					<h2>你好啊！{{name}}</h2>
				</div>
			`,
			data(){return {name:'Tom'}}
		})

		//第二步：全局注册组件
		Vue.component('hello',hello)
		//创建vm
		new Vue({
			el:'#root',
			data:{
				msg:'你好啊！'
			},
			//第二步：注册组件（局部注册）
			components:{
				school,
				student}
		})
		new Vue({
			el:'#root2',
		})
	</script>
