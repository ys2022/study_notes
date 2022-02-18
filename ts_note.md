# **Typescripts**

## 环境搭建

- 使用npm全局安装typescript
  - npm i -g typescript
- 创建一个ts文件
- 使用tsc对ts文件进行编译
  - 进入命令行
  - 进入ts文件所在目录
  - 执行命令：tsc xxx.ts


## 类型声明

```typescript
let 变量: 类型;

let 变量: 类型 = 值;

function fn(参数: 类型, 参数: 类型): 类型{
    ...
}
```

变量声明和赋值同时进行ts自动判断
js函数不考虑参数个数和类型

```typescript
function sum(a:number,b:number):number{
    return a+b;
}
sum(123,456)
let b:"a"|"b";
let d:string|number;/多种类型，或
```
## 类型断言
实例

```typescript
x as number;
<string>x;
```

## 类型种类
 
1. any
    1. `let x/x类型为any;`
    2. `let x:unkonw;//安全型的any;`
2. 字面型
3. void：没有返回值，返回为空
4. never:永远不会返回值，连空都没有
5. object:对象
   1. `let b:{name:string,age?:number,[name:string]:any};`
   2. `let d:(a:number,b:string) => number;`
6. array:
   1. `let e:string[];`
   2. `let g Array<string>`
7. tuple:长度固定的数组
   1. `let h:[string,string];`
8. enum 枚举
    ```typescript
    enum Gender{male=0,female=0}
    let i:{name:string,gender:Gender}
    i={
        name:"ys"
        gender:Gender.male
    }
    ```
9. 自定义类型
    ```typescript
    type myType=1 | 2 | 3 | 4 | 5;
    let x:myType;
    ```

## 编译选项

- 执行`$tsc xxx.ts`自动编译单独文件: `-w`

- 自动编译所有文件：目录建一个`tsconig.json`再执行`$tsc`
```json
{
"include":[
    "./src/**/*"],
"exclued":[
    ./src/hello/**/*],
    }
files
extends
compilerOptions:{
    "target": "ES6",
    "module":"ES2015",
    "lib":["dom","Es6"],
    "outDir":"./dist",
    "outFile":"./dist/app.js",
     ......
}
```
## 接口
接口的作用类似于抽象类，不同点在于接口中的所有方法和属性都没有实值,主要负责定义一个类的结构
- 示例（检查对象类型）：
  - ```typescript
    interface Person{
        name: string;
        sayHello():void;
    }
    function fn(per: Person){
        per.sayHello();
    }
    fn({name:'孙悟空', sayHello() {console.log(`Hello, 我是 ${this.name}`)}});
    ```
- 示例（实现）
  - ```typescript
    interface Person{
        name: string;
        sayHello():void;
    }
    class Student implements Person{
        constructor(public name: string) {
        }
        sayHello() {
            console.log('大家好，我是'+this.name);
        }
    }
    ```
  - 
## 类

- 定义类：
  - ```typescript
    class 类名 {
    	属性名: 类型;
    	constructor(参数: 类型){
    		this.属性名 = 参数;
    	}
    	方法名(){
    		....
    	}
    }
    ```
- this
  - 在类中，使用this表示当前对象
- 只读属性（readonly）：
  - 如果在声明属性时添加一个readonly，则属性便成了只读属性无法修改
- TS属性修饰符：
  - public（默认值），可以在类、子类和对象中修改
  - protected ，可以在类、子类中修改
  - private ，可以在类中修改
- 静态属性
  - 静态属性（方法），也称为类属性。使用静态属性无需创建实例，通过类即可直接使用
- 继承extneds
  - 继承时面向对象中的又一个特性
- 重写
  - 发生继承时，如果子类中的方法会替换掉父类中的同名方法，这就称为方法的重写
- 抽象类（abstract class）
  - 抽象类是专门用来被其他类所继承的类，它只能被其他类所继承不能用来创建实例
  - ```typescript
    abstract class Animal{
        abstract run(): void;
        bark(){
            console.log('wwww');
        }
    }
    class Dog extends Animals{
        run(){
              console.log('狗在跑~');
        }
      }
  ```

## 泛型
无法确定其中要使用的具体类型（返回值、参数、属性的类型不能确定）

```typescript
function test<T>(arg: T): T{
    return arg;
}
```
## TypeScript 模块

// 文件名 : SomeInterface.ts 
export interface SomeInterface { 
   // 代码部分
}

import someInterfaceRef = require("./SomeInterface");

## 描述文件
使用第三方库时，需要创建`xxx.d.ts`文件于目录

```typescript
declare module Runoob { 
   export class Calc { 
      doSum(limit:number) : number; 
   }
}
```