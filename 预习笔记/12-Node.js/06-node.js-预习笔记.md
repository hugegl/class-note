# 反馈
## 


# 今日内容
## path模块
1. 路径模块
2. 常用方法
  + path.basename('c:/a/a/index.js') 获取一个路径中的文件名部分,包含路径名
  + path.basename('c:/a/a/index.js','.js') 获取一个路径中的文件名部分,不包含后缀名
  + path.dirname() 获取一个路径中的目录部分
  + path.extname() 获取一个路径中的扩展名
  + path.isAbsoulte('路径') 判断一个路径是否是绝对路径;返回值true/false
  + path.parse('路径');将这个路径转换成对象;{root:'/',dir:'/'}
  + path.join('路径1','路径2');合并路径,拼接路径
3. __dirname 和 __filename 在文件操作中直接使用相对路径是不可靠的,因为在node中文件操作的路径被设计为相对执行node命令所处的路径
  + __dirname 动态获取当前文件模块所属的目录的绝对路径
  + __filename 动态获取当前文件绝对路径
4. require的路径就是相对于当前文件的,不受执行node命令的影响;fs的受执行node命令的影响;

##  使用 art-template include-extend-block语法
1. node中有很多第三方模板引擎
  + art-template
  + ejs
  + jade(pug)
  + handlebars
  + nunjuks
2. art-template中的模板继承语法
```js
//标准语法
{{include '路径'}}
{{include '路径' 文件名}}
//原始语法
<% include ('路径')%>
<% include ('路径',文件名)%>
```
3. 模板继承
```js
//可以在html的任意位置,可以是style或者script等等,都可以
//标准语法
//文件1  将这个在自己需要引入的文件中引入即可
{{extend '路径'}};
//如果不写替换neirong,默认使用原来的内容
//如果需要自己的内容,可以写
{{block '自定义名字'}}
 <h1>列表页自己的内容</h1>
 {{ /block}}


//文件2
{{block '自定义名字'}} 
<h1>默认内容</h1>
{{ /block}}
```




# 引申
## ESC6
### 函数的Rest参数
1. 箭头函数
```js
let 函数名 = (形参)=>函数体;//如果函数体只有一行
let 函数名 = (形参)=>{
函数体
};//如果函数体有多行,可以使用对象包
```
2. 展开运算符    动态参数函数
```js
function 函数名(...形参名){//...是them参数的意思,不太确定的(...m)
  函数体;
}
//箭头函数的写法
let 函数名 = (...m)=>{
  函数体;
}
```
3. 展开运算符      数组的扩展;对象也适用此法
```js
// ...[数组];//对数组的扩展
var [x,y] = [4,8]
console.log(...[4,8]);//把数组中的4和8拆解出来分别打印
//合并数组
let arr1 = [1,2];
let arr2 = [3,4];
[...arr1,...arr2];//输出结果是[1,2,3,4];如果是对象,有重复的项,那么用arr2的重复项值覆盖arr1的值;

var [x,...y] = [4,8,10,30];
//y的输出结果就是[8,10,30];x的输出结果就是4;[x,...y] 的输出结果是[4, 8, 10, 30]

let [a,b,c] = 'HUG';
//输出结果 a为H,b为U,c为G;实际输出结果是['H','U','G']


let xy = [...'HG']
```
4. 展开运算符  获取对象/数组除了前几项或者除了某几项的其他项
```js
//数组
const number = [1,2,3,4,5]
const [first, ...rest] = number
console.log(rest) //2,3,4,5
//对象
const user = {
    username: 'lux',
    gender: 'female',
    age: 19,
    address: 'peking'
}
const { username, ...rest } = user
console.log(rest) //{"address": "peking", "age": 19, "gender": "female"
}
```


### promise使用
```js
return new Promise((resolve,reject)=>{
  函数体;
})
//Promise.all语法
Promise.all([接口1,接口2])//接口1是第一个函数;接口2是第2个函数
      .then(([res1,res2])=>{函数体})//res1拿到的是第一个函数返回的结果;res2拿到的是第二个函数返回的结果
```

### module.exprots 和 ES6 import/exprots 的使用
1. exprots是导出
```js
// 导出默认, 有且只有一个默认
export default App

// 部分导出
export class App extend Component {};
//总结
// 1.当用export default people导出时，就用 import people 导入（不带大括号）
// 2.一个文件里，有且只能有一个export default。但可以有多个export。
// 3.当用export name 时，就用import { name }导入（记得带上大括号）
// 4.当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age } 
// 5.当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example
```
2. import是导入
```js
import 变量名字 from '路径';//全部导入
import {变量名1,变量名2} from '路径';//导入部分;调用的时候直接调用 变量名1,变量名2
import *  as 变量名 from '路径';//导入多个,将模块中所有导出作为对象的属性存在;调用的时候用 变量名.属性名1;变量名.属性名2 调用即可
```
3. import函数
```js
improt('路径')
```

### AMD,CMD,CommonJS 和ES6对比
1. AMD 是require在推广过程中对模块定义的规范化产出;是异步模块定义;依赖前置
2. CMD 是SeaJS在推广过程中对模块定义的规范化输出;通过require引入依赖;依赖延迟
3. CommonJS 是module.exprots 在node.js服务端端用的较多
4. ES6特性 exprots/import
```js
exprot default{
  prop:['num'],
  data(){
    return{
    }
  },
  methods:{
    increment(){
      this.$emit('incre');
      import('./../util')
    },
    decrement(){
      this.$emit('decre');
    }
  }
}
```

### 循环
1. of循环
```js
for(var i of m){//对m对象的遍历,i是m对象里的每个元素
  //循环体
}
```
### 字符串
1. 字符串可以用``包裹,这种支持换行;如果是"字符串"需要换行,每一行需要加\转义
2. 拼接
`字符串 ${变量}`;{}里面放变量即可
```js
const name = 'lux'
console.log(`hello ${name}`)//输出结果 hello lux
```
3. 字符串的方法
  + 字符串.includes('元素');判断字符串是否有元素,true/false
  + 字符串.repeat(num);获取字符串重复num次
  + 字符串.startsWith('元素');判断字符串是否以元素开始
  + 字符串.endsWith('元素');判断字符串是否以元素结束
  + 填充字符串;被填充的字符串.padStart(长度,'补全字符串')
```js
// padStart(参数1,参数2)和padEnd(参数1,参数2)一共接受两个参数;
// 第一个参数用来指定字符串的最小长度，第二个参数是用来补全的字符串。
// 如果原字符串的长度，等于或大于指定的最小长度，则返回原字符串。
'xxx'.padStart(2, 'ab') // 'xxx'
// 如果用来补全的字符串与原字符串，两者的长度之和超过了指定的最小长度，则会截去超出位数的补全字符串。
'abc'.padStart(10, '0123456789')// '0123456abc'
// 如果省略第二个参数，默认使用空格补全长度。
'x'.padStart(4) // ' x'
// padStart()的常见用途是为数值补全指定位数。下面代码生成 10 位的数值字符串。
'1'.padStart(10, '0') // "0000000001"
// 另一个用途是提示字符串格式。
'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
'09-12'.padStart(10, 'YYYY-MM-DD') // "YYYY-09-12"

```

### 函数
1. 指定函数的默认参数值
```js
function action(num = 200) {//如果num不传,则默认是200
        console.log(num)
    }
```

### 对象
1. 键值对重名可以省略,只写一个
```js
// ES5里面
{
  name: name,
  age: age
};
//ES6可以写
{
  name,
  age
}
```
2. 如果是函数,可以省略`:function`
```js
//ES5
const people = {
    getName: function() {
        console.log(this.name)
    }
}
//ES6
const people = {
  getName () {
      console.log(this.name)
  }
}
```
3. 对象的复制
+ Object.assign(目标对象, 拷贝对象1, 拷贝对象2);返回值是{拷贝对象1内容,拷贝对象2内容};同时也会给目标对象赋上这个值
```js
const objA = { name: 'cc', age: 18 }
const objB = { address: 'beijing' }
const objC = {} // 这个为目标对象
const obj = Object.assign(objC, objA, objB)

// 我们将 objA objB objC obj 分别输出看看
console.log(objA)   // { name: 'cc', age: 18 }
console.log(objB) // { address: 'beijing' }
console.log(objC) // { name: 'cc', age: 18, address: 'beijing' }
console.log(obj) // { name: 'cc', age: 18, address: 'beijing' }

// 是的，目标对象ObjC的值被改变了。
// so，如果objC也是你的一个源对象的话。请在objC前面填在一个目标对象{}
Object.assign({}, objC, objA, objB)
```

4. 对象的解构
+ 语法 `{属性名1,属性名2} = 对象名`;得到的结果就是`属性名1=属性值1;属性名2=属性值2`
+ 数组可可以进行解构 
```js
//ES5
const people = {
    name: 'lux',
    age: 20
}
const name = people.name
const age = people.age

//ES6
//对象
const people = {
  name: 'lux',
  age: 20
}
const { name, age } = people;//name是 lux;age是20
console.log(`${name} --- ${age}`);
//数组
const color = ['red', 'blue']
const [first, second] = color
console.log(first) //'red'
console.log(second) //'blue'

// 请使用 ES6 重构一下代码

// 第一题
var jsonParse = require('body-parser').jsonParse
// 1.
import { jsonParse } from 'body-parser'


// 第二题
var body = request.body
var username = body.username
var password = body.password
// 2. 
const { body, body: { username, password } } = request
```

