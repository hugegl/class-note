# 反馈
1. JavaScript天生不支持模块化,支持模块化的有
  + require
  + exports
  + Node.js才有
2. 在浏览器中也可以像在 node 中的模块一样来进行编程,使用第三方库
  + require.js     AMD
  + sea.js          CMD
  + `<script>`标签来引用加载,而且必须考虑顺序问题
3. 可以解决JavaScript的模块化问题CommonJS,AMD,CMD,UMD,EcmaScript 6 Modules官方规范
  + Node  8.5以后的版本才对EcmaScript 6 module 进行了支持;但是老版本还是不支持,使用编译器将EcmaScript 6 编译成 5 
4. package-lock.json;
  + 保存了 `node_modules`中所有包的信息(版本\下载地址);重新下载的时候速度可以提升
    - npm 5以后加入了这个文件;npm 5以前是不会有package-lock.json
    - 安装包的时候,都会生成这个package-lock.json文件;
    - npm 5 以后的版本安装包不需要加`--save`参数,它自动会保存依赖信息
    - 当你安装包的时候,会自动创建或者是更新`package-lock.json`文件
  + 这个`lock`是用来锁定版本的
    - 如果项目依赖了旧版,如果重新install其实会下载最新版本,这个lock文件就是锁定版本号,防止第三方自动升级到新版本



# 今日内容
## MongoDB
+ 源码存储在github上
+ 可以有多个数据库
+ 一个数据库可以有多个集合
+ 一个集合(在mySql里叫数据表)可以有多个文档(在mySql里叫表记录)
+ 文档结构很灵活,没有限制
+ MongoDB非常灵活,不需要像MySQL一样先创建数据库,表,设计表结构
  - 在MongoDB中只需要,当你需要插入数据的时候,值需要指定往哪个数据库的哪个集合操作即可
  - 一切都由 MongoDB 来帮你自动完成建库建表;
+ 怎么存数据的?
```js
//举个例子,存储结构
{
  '数据库1':{
      users:[//集合collocation
        {},//文档
        {},
        {},
      ]
  },
  '数据库2':{
    
  }
}
```
### 关系型和非关系型数据库
1. 表就是关系,表与表之间就存在关系
  + 所有的关系型数据库都需要通过`sql`语言来操作
  + 所有关系型数据库,在操作之前都需要设置表结构
  + 而且数据表还支持约束
    - 唯一的
    - 主键
    - 默认值
    - 非空
2. 非关系型数据库非常灵活;有的非关系型数据库就是key-value对儿
  + MongoDB定义:长得最像关系型数据库的非关系型数据库
    - 数据库 => 数据库
    - 数据表 => 集合(数组)
    - 表记录 => (文档对象)
  + MongoDB不需要设计表结构
  + 可以任意的往里面存数据,没有结构性这么一说
  + 是C++语言直接编写,开源,也可以配合php使用

### MongoDB 使用步骤
操作数据库的方法都是异步的
#### 安装
1. 正常的网上找新版安装即可
2. 如果需要32位的 [网址](https://www.mongodb.org/dl/win32/i386)
3. 配置环境变量
4. 详细参考菜鸟教程

#### 启动和关闭数据库
1. 启动控制台,输入`mongod`,默认使用执行 mongod 命令所处的盘符 /data/db 作为自己的存储目录,第一次执行该命令之前,自己手动创建这个目录
2. 关闭`ctrl +c`
3. 如需修改默认的存储目录   `mongod --dbpath=数据存储路径`

#### 连接和退出数据库
1. 连接命令 `mongo` ;默认连接本机的mongoDB服务
2. 退出命令 `exit`

#### 基本命令
1. 查看显示所有数据库  `show dbs`
2. 切换到指定的数据库 `use 数据库名称`,如果没有这个数据库,就会新建
3. 查看当前数据库 `db`
4. 插入数据
5. 显示当前db的所有集合 `show collections`
6. 查询当前集合中所有的数据 `db.集合名称.find()`

#### 使用node.js操作mongoDB 之 mongoose

1. 使用官方的mongoDB包来操作
  + [官网](https://github.com/mongodb/node-mongodb-natlve)
2. 使用底单房mongoose来操作MongoDB数据库
  + 第三方包: `mongoose`基于MongoDB官方的`mongodb`包再做一次封装
  - [mongoose网址](http://mongoosejs.com/)
3. 在官网复制初始示例下来
+ 起步
  - 安装
  `npm i mongoose`
  - hello world
```js
//引包 const 是申明常量
const mongoose = require('mongoose');
//连接数据库,指定连接的数据库不需要存在,当你存入第一个数据的时候自动创建
//{useMongoClient:true}
mongoose.connect('mongodb://localhost/test',{useMongoClient:true});
//创建模型,设定数据库;MongoDB是动态的,非常灵活,只需要在代码中设计数据库就可以了
//规定Cat的模型,怎么存储数据
const Cat = mongoose.model('Cat', { name: String });
//实例化一个Cat
const kitty = new Cat({ name: 'Zildjian' });
//持久化保存kitty实例
kitty.save().then(() => console.log('meow'));
```
+ demo 02 设计 Schema 发布 model
```js
var mongoose = require('mongoose');
 var Schema = mongoose.Schema;
mongoose.connect('mongodb://localhost/test');
//2. 设计集合结构(表结构)
//字段名称就是表结构中的属性名称
//值的类型;约束数据,保证完整的数据
  var UserSchema = new Schema({
    username:{
      type:String,
      required:true,//'required:true' 必须有
    }
    password:{
      type:String,
      required:true,
    },
    email:{
      type:String,
      required:true,
    },
    gender: { 
      type: Number, 
      enum:[0,1],//限定只能是0或者1
      default: 0,
      },
   
  });
  //3. 将文档结构发布为模型
  //mongoose.model('参数', 架构);将架构发布为model,返回值是模型对象(即模型构造函数)
  var User = mongoose.model('blogSchema', UserSchema);
```
+ mongoose.model('参数1', 参数2);
  - 参数1:传入一个大写名字单数字符串用来表示你的数据库名称,mongoose会自动将大写名词的字符串生成小写复数的集合名称;如User最终会变成users集合名称
  - 参数2: 模型架构(Schema)
  - 返回值是模型对象(即模型构造函数);我们可以使用这个返回值对 users 集合中的数据进行任意操作

#### mongoose数据库的基本操作,增删改查
官方指南 ;详细查看官方文档
1. 增
```js
var admin = new User({
  username:{
    username:'admin',
    password:'123456',
    email:'admin@admin.com'
  }
})
admin.save(function(err,ret){
if(err){
  '存储失败'
}else{
  '保存成功'
}
})
```
2. 删
+ 库名.remove({条件},函数);删除符合条件的所有数据
+ 库名.findByIdAndRemove('id',函数);根据id删除一个
+ 库名.findOneAndRemove({条件},函数);根据条件删除一个

```js
User.remove({
username:'zs',
},function(err){
  //err,删除失败
  //只要不报错就是删除成功
})
```
3. 改 
+ 库名.findByIdAndUpdate('id',{更新的内容},函数);根据id名修改内容
+ 库名.update(条件,{更新的内容},函数);根据条件修改内容
+ 库名.findOneAndUpdate({条件},{更新的内容},函数);根据条件修改一个
```js
//查询所有,User是数据库名字
User.findByIdAndUpdate('id',{
  name:'ls',
}function(err,ret){
if(err){
  '查询失败'
}else{
  //ret就是结果
}
//查询指定结果;find({条件},函数)
User.find({
  name:'zs',//查找name叫张三的
  },function(err,ret){
if(err){
  '查询失败'
}else{
  //ret就是结果
}
})
```

4. 查
+ 按条件查询所有 库名.find({条件},函数);查询结果都会放到数组中
+ 使用 库名.findOne();查询结果是一个对象
```js
//查询所有,User是数据库名字
User.find(function(err,ret){
if(err){
  '查询失败'
}else{
  //ret就是结果
}
//查询指定结果;find({条件},函数)
User.find({
  name:'zs',//查找name叫张三的
  },function(err,ret){
if(err){
  '查询失败'
}else{
  //ret就是结果
}
})
```

#### 使用node.js操作 MySQl数据库 

##### 使用步骤
1. 安装
```shell
npm i mysql
```
2. demo 
```js
var mysql  = require('mysql');
//1.创建连接
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 //2.连接数据库
connection.connect();
 //3.执行操作 SELECT 1 + 1 AS solution 操作语句;增删查都在这个位置写
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
 //4.关闭连接
connection.end();
```









# 引申

## 数组中涉及到遍历的方法
1. 数组.includes(条件)   判断数组中是否包含条件;true包含;false不包含;
2. 数组.reduce

## 字符串替换
1. 字符串.replace(字符串/正则,新字符串/函数);默认替换第一个字符串
  + `/"/g`,找到全局的"
  + 字符串模式,简单,不支持全局和忽略大小写问题
  + 正则表达式模式强大,支持全局和忽略大小写

## promise 数据库操作案例
+ 防止多个嵌套的方式;避免回调地狱;在ES 6中新增了一个API: `promise` 
+ 只有函数内部 return 了 promise 对象(就是一个容器)的方法才能使用这个 promise 写法
+ jQuery 里面封装了方法,可以直接调用 promise 的
+ promise API
 - promise是一个构造函数
 - 创建的时候
 - ` new Promise(function(resolve,reject){异步任务}`和`then(函数1,函数2)`
 - 函数1 与 resolve 对应,意为成功,成功时调用
 - 函数2 与 reject 对应,意为失败,失败时调用
```js
//1.创建 promise 容器 //翻译为承诺
// promise 容器一旦创建,就开始执行里面的代码
var p1 = new Promise(function(resolve,reject){
  //resolve 是成功执行的,形参
  //reject 是失败执行的,形参
  //promise 本身不是异步的
  //容器内部放置异步任务,fs就是异步的
  fs.readFile('路径','utf8',function(err,data){
    if(err){
      //失败了,promise 容器中的任务失败了;把容器中的 pedding 状态改为 reject
      reject(err)
    }else{
       //成功了,promise 容器中的任务成功了;把容器中的 pedding 状态改为 resolve
      resolve(data)
    }
  })
})

//使用
//当p1成功了,然后(then) 做指定的操作 then 就对应了 成功 (resolve)了
//then(函数);接收的函数就是容器中 resolve(data) 这个函数;里面的data,就是异步函数处理的结果;
p1.then(function(data1){
      //成功时调用
        return P2;//就是后面then(成功函数,失败函数),成功函数中的形参就是拿到的 P2 ;
        //主要是return 一个 promise对象;当return 一个promise 对象的时候,后续的then中的方法的第一个参数会作为 这个return出去的 promise对象的 resolve函数
        },function(err){
        //失败时调用
        return P2-error;//就是后面then(成功函数,失败函数),失败函数中的形参就是拿到的 P2-error ;
        //如果return 一个 promise对象;后续的then中的方法的第二个参数会作为 这个return出去的 promise对象的 reject 函数来使用
        })
    .then(function(data2){
          //这里能拿到 P2 中成功函数的 data数据;失败函数的数据在then(函数1,函数2),函数2中声明形参也可以拿到
          return P3;
        })
    .then(function(data2){
    //这里能拿到 P3 中成功函数的 data数据;失败函数的数据在then(函数1,函数2),函数2中声明形参也可以拿到
          })
```
+ mongoose 所有的 api 都支持 promise
```js
//例子,判断用户是否存在,如果已存在,结束注册;如果不存在,注册(保存一条用户信息);
//mongo语法中find中有return promise对象,所以可以直接使用
User.find({
    username:'admin'
    })
    .then(function(user){
        if(user){
          //已存在
        }else{
          return new User({
            username:'aa',
            password:'123',
            email:'11@123'
          }).save()
        }
    })
    .then(function(ret){
    })
```
+ 自己封装jquery中的ajax函数需要手动return promise 对象
```js
//自己封装ajax带 promise对象的函数
function get(url,callback){
return new Promise(function(resolve,reject){
  var oReq = new XMLHttpRequest()
  oReq.onload = function(){
    resolve(JSON.parse(oReq.responseText))
    callback && callback(JSON.parse(oReq.responseText));//增加callback是多种形式的,可以用then,也可以用callback
  }
  oReq.onerror = function(err){[
    reject(err)
  ]}
  oReq.open('get',url,true)
  oReq.send()
})
}
//调用这个函数
get('http://....')
.then(function(data){
  //执行的代码
})
```

## ES6的书
1. ECMAScript 6 入门    阮一峰
2. 深入理解ES6    JavaScript高级程序设计的作者 尼古拉斯的卡司




