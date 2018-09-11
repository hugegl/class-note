# 复习
## MongoDB 非关系型数据库
1. 特点,没有表结构,表与表之间没有关系,速度较快,存储在内存中
### mongod 
1. 启动数据库`mongod --dbpath 路径`

### mongo
1. 连接数据库`mongo`,并进行数据库操作(命令行)
#### 使用mongo操作数据库
1. 查看所有的数据库`show databases`
2. 切换数据库`use 数据库名称`
3. 查看当前数据库的所有集合`show collections`
4. 查
  + `db.集合名称.find()`查看所有,`db.集合名称.find({})`
  + `db.集合名称.find({条件对象})`;
    - 条件对象: {属性名:属性值}
    - 条件对象:{属性名:对象{条件}}??????是()还是{}????
    - $lt $gt $lte $gte $in $nin
5. 增
  + `db.集合名称.insert({属性名:属性值,属性名:属性值})`
  + `db.集合名称.insertOne({属性名:属性值,属性名:属性值})`
  + `db.集合名称.insertMany([{属性名:属性值},{属性名:属性值}])`
6. 删
  + `db.集合名称.deleteOne({条件对象})`,如果匹配到多个数据,只删除第一个
  + `db.集合名称.deleteMany({条件对象})`
7. 改
  + `db.集合名称.updateOne({条件对象},{操作对象})`,如果匹配到多个数据,只修改第一个
  + `db.集合名称.updateMany({条件对象},{操作对象})`

#### 使用node.js操作数据库
1. 下载驱动包
2. 步骤
```js
var MongoClient = require('mongodb').MongoClient
var connStr = 'mongodb://localhost:27017'
MongoClient.connect(connStr,function(err,client){
//1.通过client获取数据对象
var db = client.db(数据库名称)
var 集合 = db.collection(集合名称)
集合.find({条件对象}).toArray(function(err,arr){})
集合.insert({条件对象})(function(err,dbResult){})
集合.deleteOne({条件对象})(function(err,dbResult){})
集合.updateOne({条件对象},{操作对象})(function(err,dbResult){})
//关闭连接
client.close();
})
```



# 今日内容
## npm上传包
+ 目录需要在包下面执行命令工具
  1. 登录`npm login`
  2. 输入用户名
  3. 输入密码
  4. 输入邮箱
  5. `nrm use npm` 默认镜像的只能下载,不能上传,所以要切换到npm
  6. 上传`npm publish`
    + 注意
      - 包名不能和npm中已有的包同名
      - 代码内容更新之后,重新上传,需要修改版本号
      - 修改版本号的命令,可以手动修改
        + 修改主版本号`npm version major`
        + 修改次版本号`npm version minor`
        + 修改末版本号`npm version patch`
      - 上传包的时候,一定要用npm服务器 
+ 如果已经下载了老版本的,需要下载新版本时,可以加上版本号后下载

## 命令行工具cli
### 简介
1. 定义 可以在命令行中直接输入一个命令,实现某个功能
2. CLI: Command Line Interface 后期会学到 Vue-Cli

### 使用node.js编写命令行工具的流程
1. 先创建一个包
2. 在包中实现命令行工具的功能
3. 在文件第一行写`#! node`告诉系统使用node.js执行当前代码;环境变量要配置好,如果没有配置好,需要`#! node的完整路径`
4. package.json中
  + 属性增加`bin`
  + 将属性值改为`{'命令名称':'命令执行的路径文件'}`
  + 安装完成之后,命令行中就可以使用这个命令了
5. 将包上传到服务器
6. npm进行全局安装
7. 然后就可以使用`命令名称`执行命令了
```js
#! node//告诉系统使用node.js执行当前代码
var fs = require('fs');
// fs创建文件夹
//`fs.mkdir('路径',function(err){执行代码})`;创建成功err就是null;创建失败err就是错误对象
fs.mkdir('路径',function(err){
  if(!err){
    // 执行代码
  }
  })
```
## ES6 
1. 没有ES4,只是一个草案,未发行

### 介绍-在ES6入门的书内
1. [ES6阮一峰](http://es6.ruanyifeng.com/#docs/intro)
2. 提案流程
  + Stage 0 - Strawman（展示阶段）
  + Stage 1 - Proposal（征求意见阶段）
  + Stage 2 - Draft（草案阶段）
  + Stage 3 - Candidate（候选人阶段）
  + Stage 4 - Finished（定案阶段）

### 变量声明的方式
1. `let 变量名`
  + 不可以重复声明
  + 有块级作用域,只能在`{}`内部生效
```js
for(var i =0;i<10;i++){
  setTimeout(function(){
    console.log(i)
  },0)
}//打印10次10
for(let i =0;i<10;i++){
  setTimeout(function(){
    console.log(i)
  },0)
}//打印1~9;用let限制i的块级作用域,所以函数每次只能访问自己的那一个i
```
2. `const 变量名`
  + 声明的叫做常量,不能被修改的量
  + 不能重复申明
  + 有代码块作用域,`{}`包裹起来就是一个块级作用域
  + 声明常量的时候必须赋值
  + 如果储存的是一个地址,那么这个地址里面的值少吃可以改的
```js
const obj = {
  name:'pp',
  age:15,
}
obj.age = 18;//可以执行
```
3. 简写
+ 属性和方法简写
```js
var obj = {
  name:name,
  sing:fucntion(){
  //内容
  }
}
var obj = {
  name,
  sing(){
  //内容
  }
}
```
### 解构赋值
+ let {对象的属性名:要声明的变量名} = 对象;就会自动声明一个变量出来,变量的值就是对象中对应的属性的值
+ 对象解构
```js
let obj = {
  name:'pp',
  age:15,
  sing(){
    console.log('aaa')
  }
}
let{name:name} = obj;//name = obj.name
let{name} = obj;//name = obj.name
let{name,age} = obj;//name = obj.name;age = obj.age;简写,只有要声明的变量和对象中的变量名一样的时候使用
function test({name,age}){
  console.log(name,age)
}
test(obj)
```
+ 数组解构;解构与声明的结构一样即可
```js
let arr = [1,23,4];
let [num1] = arr;//1
//如果只拿第三个
let [,,num] = arr;//4
let arr = [[1,2],[3,4]]
let[[num1,num2],[num3,num4]] = arr;
```
### rest-element 剩余元素
+ ...语法在数组解构赋值中叫做 RestElement 剩余元素
+ 剩余元素只能有一个
+ 剩余元素只能是最后一个元素
```js
let arr = [1,2,3,4,5]
let [num1,...num2] = arr;//1,[2,3,4,5]
```
### 箭头函数
+ 在ES6中函数表达式可以使用箭头函数
+ 借鉴的是java里面的lenbuda(音译)表达式
```js
//基本用法
// let 函数名 = (形参) => {函数体}
let sayHi = () => {
  console.log('aaa');
}
sayHi();
```
+ 简写形式
  + 如果形参只有一个,`()`可以省略
  ```js
  let doulbe = a => {
    //函数体
  }
  ```
  + 如果函数体只有一句代码,`{}`可以省略
  ```js
  let doulbe = a => console.log('aaa');//函数体
  ```
  + 如果函数体只有一句代码,且这句代码是返回语句,`return`和`{}`都可以省略
  ```js
  let sum = (a,b) => a + b;//函数体
  ```
  + 如果函数体只有一句代码,且没有形参,`{}`都可以省略,`()`变成`_`
  ```js
  let sum = _ => console.log('哈哈');//函数体
  ```
+ 箭头函数中的 `this`
  + 没有 this
  + 如果在箭头函数中使用 this ,会向上一级作用域中进行查找
  + 之前使用`var that = this`的场景,都可以用箭头函数直接使用this
  + node中,全局对象this
+ 箭头函数中`arguments` 是用来获取所有形参的值的
  + 没有 arguments
  + 剩余参数
    - 只能有一个,并且只能是参数列表的最后一个
    - 是一个真数组,可使用任何数组的方法
  ```js
  let fun = (...a) => {
    console.log(a)
  }
  fun(1,2,3);//打印[1,2,3]
  let fun = (b,...a) => {
    console.log(a)
  }
  fun(1,2,3);//打印[2,3]
  ```
+ 函数参数的默认值
```js
function sum(a =0 ,b = 0){//如果不传,默认是0
  return a+b;
}
```
### 对象
1. 在声明对象的时候,使用变量的值作为属性名声明对象
```js
//实现这种效果
var key = 'name';
var obj = {
  name : 'pp'
}
//ES6实现:
var key = 'name';
var obj = {
  [key] : 'pp'
}
```
2. 对象扩展运算符,使用...可以将对象中所有的属性给当前对象添加一份
```js
var aa = {
  name:'pp',
  age:18
}
var bb = {...aa};//b的值为{name:'pp',age:18}
var bb2 = {...aa,title:'哈哈'};//b的值为{name:'pp',age:18,title:'哈哈'}
```
### ...
1. 数组传参时用法,拆解数组
```js
function sum (a,b,c){
  return a+b+c;
}
var arr = [1,2,3]
//...在下面的场景中就相当于将数组中所有元素拆解开,依次传递给函数的形参了
sum(...arr);
//也可以使用
sum.apply(null,arr)
```
### ES6中的class关键字的使用
1. 对象是类的实例
+ 类的申明不能重名
+ 静态方法:static 方法名(){函数体}
+ 静态属性;后期没有,草案中有;草案中使用 static 变量名 = 值;
```js
class Person{//Person是变量名
  constructor (name,age){ //是一个构造函数;不写,就是默认是{}空对象
    this.name = name;
    this.age = age;
  }
  sayHello(){//在这里直接写的方法是自动放到了 Person.prototype上面去了;就是放到原型对象上去了
    //函数体
  }
  //静态方法
  // static 函数名(){
  //   //函数体
  // }
  static sayHi(){
    //函数体
  }
}
var p = new Person();
//工具,与实例无关的会放到静态方法上面去
//$.ajax
//Array.isArray
//Object.create
```
2. 使用class关键字自实现继承
  + extends`class 子 extends 父 {}`
  + 子类构造函数中,需要调用一下父类的构造函数`super()`;父类的静态方法也会继承
  ```js
  class Person{//Person是变量名
  constructor (name,age){ //是一个构造函数;不写,就是默认是{}空对象
    this.name = name;
    this.age = age;
  }
  sayHello(){//在这里直接写的方法是自动放到了 Person.prototype上面去了;就是放到原型对象上去了
    //函数体
  }
  new Person()
  //继承 class 子类 extends 父类 {}
  class Student extends Person{};//student继承了person的属性
  class Student extends Person{//student继承了person的属性
       constructor (name,age){
        super(name,age);//调用父类的构造函数,之后才可以增加自己的方法
        this.code = 'code';//这里可以写自己的属性
      }
  };
  new Student()
  ```
  + 借用构造函数继承(super()调用的原因)
  ```js
  function Person(){
    this.name = 'pp'
    this.age = 15;
  }
  function Student(){
    Person.call(this);//执行构造函数,并且把Person里面的this指向student的this
  }
  var stu = new Student();
  //super()相当于这里的call
  ```

### ES6中的模板字符串
1. 模板字符串 `
  + var str = `字符串`;支持换行
  + 可以直接在字符串中嵌入变量;里面支持`${变量名}`
  ```js
  var name = 'pp';
  var age = 15;
  var str = `我叫${name},我今年${age}岁`
  ```
### promise
1. 出现的目的 解决回调地狱
2. 使用别人写好的 promise api
  + `.then(函数1,函数2)`,第一个是成功的回调函数,第二个是失败的回调
3. 自己封装 promise 给别人使用`.then()`
```js
// promise 对象有.then方法,可以用来传递回调函数
//promise 有三种状态: pedding(挂起,正在执行)  fullfilled(成功 已经执行完毕,结果是成功的)  rejected(失败,已经执行完毕并且结果是失败的)
function timeout(time){
  return new Promise(function(resolve,reject){
    setTimeout(function(){
      //当一部操作完成之后,只需要改变 promise 的状态就可以了
      //1. resolve 函数调用,可以将当前 promise 改变为成功;
      //2. reject 函数调用,可以将当前 promise 改变为失败
      //3. resolve,reject都可以传参给使用的then传递的两个函数的实参使用; 
      resolve(resolve形参);
      reject(reject形参);
    },time)
  })
}
timeout(1000).then(function(resolve实参){
})
```
4. promise 进阶
  + `.then`需要上一个 .then 的函数中有 promise 对象,才可以继续调用;
  + new Promise (function(resolve,reject){函数体});和.then(函数1,函数2);中 resolve 和 函数1;reject 和 函数2 一一对应;
```js
timeout(1000).then(function(resolve实参){
  return timeout(1000)
}).then(function(){
return timeout(1000)
})
```
  + catch 方法  捕获异常
```js
timeout(1000)
  .then(function(){})
  .catch(function(){//捕获异常的函数体})
```
  +  Promise 静态方法
    - Promise.all() 在所有的 promise 异步操作完成之后执行某个任务
      - ` Promise.all(异步操作们).then(function(){函数体})`
    - Promise.race() 在第一个 promise 异步操作完成之后执行某个任务
      - ` Promise.race(异步操作们).then(function(){函数体})`
```js
var arr = [timeout(1000),timeout(2000),timeout(3000)]
Promise.all(arr).then(function(data){
  //所有异步操作全部完成之后,会执行这边的函数体
  //每次异步操作成功的结果都放到这个data中,以数组的形式
})
Promise.race(arr).then(function(){
  //第一个 promise 异步操作完成了只有执行的函数体
  })
```



# 引申
1. 刷题网站1 [网址](https://leetcode-cn.com)
2. 刷题网站2 noline judge [网址](https://acm.sjtu.edu.cn/OnlineJudge/problems)
3. 通过`http.request`模块,可以用来发送请求,整合拿到的结果
4. arguments的作用,在函数被调用的时候,会将所有实参存储到 arguments 对象中,是一个伪数组;
  + 使用场景,传的参数个数不定的时候,可以不写形参,在函数内部使用`arguments`接收所有的实参;
5. 判断是否是数组
    + Array.isArray(查询的变量)
    + Istanbul(???下课查?)
6. 成员: 属性和方法的统称
  + 实例成员:指通过实例访问的成员
  + 静态成员:指通过构造函数本身访问的成员
7. super父类 derived子类
8. axios:用来发送ajax请求的库,这个库支持 promise;就可以用`.then()`方法来使用回调函数
```js
axios.({
  url:'',
  data:{},
  method:'get',
})
.then(function(data){

})
.then(function(data){
  //成功会执行的函数
},function(err){
  //错误会执行的函数
  //err是错误信息
})
```
9. 配合 promise 使用的 async 和 await (了解)