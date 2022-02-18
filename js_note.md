# javascript

## 常用
/*js多行注释*/
//单行注释
/*严格区分大小写
*必须;结尾
*会忽略多个空格换行
*驼峰命名法
*/
转义：\
代码块：{}

## 变量
在 2015 前，用 var 来声明 JavaScript 变量。
在 2015 后， (ES6) 允许使用 const 关键字来定义一个常量，使用 let 关键字定义的限定范围内作用域的变量

## 数据类型
Number
String
Null
Undefine
boolean
Object

## 输出
```html
document.getElementById("id").innerHTML = "adasd";
document.write("");
console.log("");
alert("");
```
数组：[40, 100, 1, 5, 25, 10]

## 运算符

### 比较运算符
==
！=

### 逻辑运算符
&&	and	
||	or	
!	not	
### 条件运算符
variablename=(condition)?value1:value2 

## 条件语句
```html
if (time<10)
{document.write("<b>早上好</b>");}
else if (time>=10 && time<20)
{document.write("<b>今天好</b>");}
else
{document.write("<b>晚上好!</b>");}
var d=new Date().getDay();
switch (d)
{
    case 0:x="今天是星期日";
    break;
    default:
    x="期待周末";
}

```

## 函数：
function myFunction(a, b) { 
    return a * b;
}
return既可以返回也可以退出

## 对象

```html
var person = {
    firstName: "John",
    lastName : "Doe",
    id : 5566,
    fullName : function() //定义方法
	{
       return this.firstName + " " + this.lastName;
    }
};
person.lastName;
person["lastName"];
objectName.methodName
```

## 作用域
在函数中没有使用声明var的变量为全家变量
全局变量属于window对象是window对象的变量

## HTML事件

onchange	HTML 元素改变
onclick	    用户点击 HTML 元素
onmouseover	鼠标指针移动到指定的元素上时发生
onmouseout	用户从一个 HTML 元素上移开鼠标时发生
onkeydown	用户按下键盘按键
onload	    浏览器已完成页面的加载


## json
JSON.parse()	用于将一个 JSON 字符串转换为 JavaScript 对象。
JSON.stringify()	用于将 JavaScript 值转换为 JSON 字符串。