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
                data:{name:'尚硅谷'},
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