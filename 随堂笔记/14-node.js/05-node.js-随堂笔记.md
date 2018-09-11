# 复习
1. 工作中的打开服务器   `live-server` 是node自带的
2. express
  + 定义:是一个基于node.js的web开发框架
  + 基本使用
```js
var express = require('express');
var app = express();
app.get('路由路径',function(req,res,next){
  res.send('返回的数据')
})
app.listen(3000,function(){
  console.log('open')
})
```
  + 路由注册的方式
    - app.请求方式(路径,函数)
      + 请求方式必须和方法名一致
      + 请求的路径必须和注册路径一致
    - app.all(路径,函数)
      + 请求方式不限
      + 请求的路径必须和注册路径一致
    - app.use(路径,函数)
      + 请求方式不限
      + 请求的路径只要以路由路径开头即可;
      + 如果不传递路由路径,默认为'/',所有的请求都会被这个路由处理
  + req和res新增的功能
  - req
    1. req.query  获取get请求的参数
    2. req.body  body-parser中间件
    3. req.originaUrl
    4. req.path
    5. req.get
  - res
    1.res.send
    2.res.sendFile
    3.res.render  需要配置模板引擎
    4. res.download
    5. res.status
    6. res.jsonp
    7. res.redirect
3. req.body的获取
body-parser中间件
```js
app.use(require('body-parser').urlencoded())
app.use(require('body-parser').json())
```
4. render的使用
配置模板引擎
```js
//1.设置模板引擎
app.engine('html',require('express-art-template'))
//2.设置模板文件的文件路径
app.set('views',path.join(__dirname,'路径'))
//3.设置默认后缀名
app.set('views engine','html')
```
5. 中间件
+ 中间件就是一个函数,这个函数有三个参数,req,res,next
  - app.get(路由路径,中间件函数)
  - app.all(路由路径,中间件函数)
  - app.use(路由路径,中间件函数)
+ 中间件必须做出选择:要么结束响应,要么调用下一个中间件;
6. hacker-news案例-初级版
```js
var path = require('path');
var storage = require('./storage');//自己封装的 storage 操作数据的函数
var express = require('express');
var app = express();
//配置模板引擎
app.engine('html',require('express-art-template'))
//默认会去views里面找文件
//配置默认后缀
qpp.set('views engine','html')
//配置body-parser
app.use(require('body-parser').urlencoded())
app.use(require('body-parser').json())
//指定路由规则
app.get('/index',function(req,res){
  storage.getAllNews(function(newList){
    res.render('index',{list:newList})
  })
})
app.get('/details',function(req,res){
  storage.getNewsById(req.query.id,function(news){
    res.render('details',{item:news})
  })
})
app.get('/submit',function(req,res){
  res.sendFile(path.join(__dirname,'views','submit.html'))
})
app.get('/add',function(req,res){
  storage.addNews(req.query,function(){
    res.redirect('/')
  })
})
app.post('/add',function(req,res){
  storage.addNews(req.body,function(){
    res.redirect('/')
  })
})
//静态资源托管
app.use('/resources',express.static('resources'))
app.listen(3000,function(){
  console.log('open')
})
```









# 今日内容
## mongoDB
### 数据库
1. 分类
+ 关系型数据库;表和表之间是有关联的(table)
  - MYSQL
  - MSSQL(收费)
  - Oracle(收费)
+ 非关系型数据库;集合和集合之间是没有关联的(collocation)
  - mongoDB
  - Redis
  - Memecache

### 非关系型数据库与关系型数据库的额术语对照
|关系型|非关系型|
|--|--|
|数据库(db)|数据库(db)|
|表(table)|集合(collection)|
|记录/行(row)|文档(document)|
|字段(field)|字段(field)|

### 关系型数据库和非关系型数据库的区别
1. 关系型的表之间是有联系的,非关系型没有
2. 关系型的表使用之前必须先创建好表结构,非关系型不用
3. 关系型的表使用T-SQL进行操作,非关系型用类似于JS的语法操作
4. 非关系型数据库的优点
  + 更加灵活(没有任何限制,表内的数据可以随意存储,没有字段要求)
  + 速度更快;效率更高
    - 没有了关系
    - 少了字段的各种限制
    - 一般非关系型数据库都会直接存储在内存中,所以速度会更快;
    - 自动会存储在硬盘中,永久化数据;可以很好的处理高并发现象;
5. 一般会先把数据存在非关系型数据库内,再把数据存到关系型数据库中

### 使用步骤
#### 安装
1. homebrew  使用MAC的
2. 32位的 详细看视频,版本是2.6的版本

#### 使用
1. 操作MySQL数据库的方式:命令行工具;NaviCat可视化操作工具;代码操作
2. 操作mongod负责存储数据;mongo命令行工具;NaviCat可视化操作工具;代码操作

#### 数据库服务 mongod
启动数据库服务,使用的是 mongod 命令
1. 默认存储的路径是:`data/db`;需要在想要保存数据的位置手动创建这两个文件夹,
2. 在data文件同目录下,使用启动命令启动
`mongod --dbpath 数据文件夹路径`
3. 如果看到最后一句输出为`waiting for connections on port 27017`说明启动成功了
关闭数据库服务
1. `ctrl+c`

#### 数据库操作的命令行工具 mongo
通过命令操作mongodb 使用 mongo 命令
1. 连接数据库
在cmd直接输入`mongo`
远程服务器连接`mongo --host 服务器地址 --port 端口号`
2. 退出数据库
在cmd直接输入`exit`或者`ctrl+c`

#### 通过命令行工具mongo来操作数据库
1. 查看所有的数据库列表`show databases;`;默认是admin 和local
2. 切换到指定数据库`use 数据库名称;`
3. 查看当前数据库中所有的集合`show collections;`

#### 实现增删改查
注意:在mongoDB中进行数据库操作的时候,不需要提前创建新数据库
1. 如果需创建一个新的数据库
  + 直接`use 新数据库名称`,这个数据库会在第一条数据天剑进去的时候创建出来
2. 给集合中添加数据
  + 如果集合不存在,则会自动创建,如果集合存在,则会将数据添加到对应的集合中
  + 命令行中有一个全局对象`db`,这个对象就表示当前正在使用的数据库对象;当前use的是谁db就是谁
3. 增
  + `db.集合名称.insert({键:'值',键:'值'})` 添加一个
  + `db.集合名称.insertMany([{键:'值',键:'值'},{键:'值',键:'值'}])` 添加多个
  + 插入成功`writeResult("nInserted":1})
4. 查
  + `db.集合名称.find()`查询当前集合中所有的数据
  + `db.集合名称.find({条件})`条件查询;注意条件是对象的形式传入
    - 如查找age为18的人`db.users.find({age:18})`
  + 条件分类
    1. 大于等于  {$gte}`db.users.find({age{$gte:18}})`
    2. 等于 {}
    3. 小于 $lt
    4. 小于等于 $lte
    5. 大于等于 $gte
    6. 不等于 $ne
    7. 在...范围内 $in    `db.users.find({age{in:[1,2,3]}})`只要是1,2,3的都会被找出来
    8. 不在...范围内 $nin
    9. 等于 $eq
  + 多个条件,用,隔开即可
    - `db.users.find({age:18,name:pp})`
5. 删
  + `db.集合名称.deleteOne({条件})` 删除一个;如果符合条件的有多个,默认删除找到的第一个
  + `db.集合名称.deleteMany({条件})` 删除多个;符合条件的都删掉
6. 改
  + `db.集合名称.updateOne({查找条件},{操作对象})`修改一个;如果符合条件的有多个,默认修改找到的第一个
  + `db.集合名称.updateMany({查找条件},{操作对象})`修改多个;
  + 操作对象固定写法:  `{$set:{属性名:值}}`  
    - eg:  将name是pp的年龄改成18;
    - `db.users.updateMany({name:'pp'},{$set:{age:18}})`
  + 如果有这个字段就修改,如果没有这个字段就增加

#### 图形化工具Robo操作 mongoDB 数据库
详细看视频

#### 使用nodejs操作 mongoDB 数据库
1. 安装官方包`npm i mongodb`会把数据库的操作api叫做驱动
2. 使用步骤
```js
//1.引入mongoClient
var MongoClient = require('mongodb').MongoClient;
//2.创建数据库连接字符串
var connStr = 'mongodb://localhost:27017'
//3.连接,调用mongoClient提供的方法connect进行数据连接
MongoClient.connect(connStr,function(err,client){
//err是错误对象;如果报错就是错误对象;如果不报错就是null
//client数据库客户端对象
//增删改查
//1-1获取db对象
// var 变量名 = client.db('数据库名称');
var db = client.db('users')
//1-2通过db来操作数据库中的集合
// var 变量名 = db.collection('集合的名字');
var user = db.collection('user');//这个是为了方便看
//或者,像下面这样,使用更简洁
// db.collection('user').insert()
// db.collection('user').insertMany()
// db.collection('user').find()
//1-3 增加(同命令行操作)
user.insert({name:'pp',age:12},function(err,dbResult){
  //dbResult.result添加结束后的结果{ok:1,n:2},ok是成功,0就是不成功;n是受影响几行
})
//1-4查  toArray将查询到的数据转换成数组
//find()查询所有;find({条件})查询符合条件的
user.find().toArray(function(err,arr){
  //err是错误形参
  //arr是接收到的转成数组的数据
})
//1-5删
user.delete({age:18},function(err,dbResult){
  //dbResult.result删除的结果
})
//1-6 改
// user.update({条件对象},{操作对象})
// user.updateOne({条件对象},{操作对象})
// user.updateMany({条件对象},{操作对象})
user.update({age:12},{$set:{age:18}},function(err,dbResult){
  //dbResult.result修改的结果
})
//4. 移动要关闭数据库连接
client.close();
})
```

#### hacker-news案例
```js
//将storage模块修改成操作数据库版本即可
var MongoClient = require('mongodb').MongoClient;
var connStr = 'mongodb://localhost:27017';
var DBNAME = 'hackrnews';
var COLNAME = 'news';
module.exprots = {
  getAllNews:function(callback){
    MongoClient.connect(connStr,function(err,client){
      var db = client.db(DBNAME);
      var news = db.collection(COLNAME);
      news.find().toArray(function(err,arr){
        callback(arr);
      })
      client.close();
    })
  }
  getNewsByOne:function(id,callback){
    MongoClient.connect(connStr,function(err,client){
      var db = client.db(DBNAME);
      var news = db.collection(COLNAME);
      news.find({_id:id}).tuArray(function(err,arr){
        callback(arr[0])
      })
      client.close();
  }
    //mongoDB中的_id不是一个字符串,所以直接通过字符串是查不到的
    //所以我们查询的时候需要将字符串转换成Object类型的
    // var ObjectId = require('mongodb').ObjectId
    // //ObjectId(字符串);转成objectid即可
    // ObjectId.(id)
 addNews:function(info,callback){
    MongoClient.connect(connStr,function(err,client){
      var db = client.db(DBNAME);
      var news = db.collection(COLNAME);
      news.insert(info,function(err,dbResult){
        if(dbResult.result.ok == 1){
          callback();
        }
      })
      client.close();
    })
  }
}
```
字符串转换成Object类型的
```js
var ObjectId = require('mongodb').ObjectId
//ObjectId(字符串);转成objectid即可
ObjectId.(id)
```

## 使用 node.js 写接口
```js
var express = require('express');
var app = express();
//使用模块化写好的mongo数据库增改查
var stroage = require('./stroage-mongo');
  app.get('api/getnewslist',function(req,res,next){
  stroage.getAllNews(function(newsList){
    res.send({
      errCode:200,
      msg:'获取列表成功',
      data:newsList,
    });
  })
})
  app.get('api/getnewsdetail',function(req,res,next){
  stroage.getNewsById((req.query.id,function(news){
    res.send({
      errCode:200,
      msg:'获取详情成功',
      data:news,
    });
  })
})
  app.get('api/addNews',function(req,res,next){
  stroage.addNews(req.query,function(req.query.id,news){
    res.send({
      errCode:200,
      msg:'添加数据成功'
    });
  })
})
app.listen(3000,function(){
  console.log('open')
})
```
+ 接口文档
|项|说明|
|--|--|
|接口地址(url)|'api/getnewslist'|
|请求方式(method)|get|
|请求参数(params)|无|
|响应数据示例|
```js
{
  errCode:200,
  msg:'获取列表成功',
  data:newsList,
}
```
|接口地址(url)|'api/getnewsdetail'|
|请求方式(method)|get|
|请求参数(params)|id:<String>|
|响应数据示例|
```js
{
  errCode:200,
  msg:'获取详情成功',
  data:news,
}
```
|接口地址(url)|'api/addNews'|
|请求方式(method)|get|
|请求参数(params)|title:<String>,url<String>,text<String>|
|响应数据示例|
```js
{
  errCode:200,
  msg:'添加数据成功'
}
```

## node.js设置 CORS
```js
app.use(function(req,res,next){
  //网上搜索
    res.header('Access-Control-Allow-Origin', '*');
    res.header('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
    res.header('Access-Control-Allow-Headers', 'Content-Type');
})
```


# 引申
## 计算机系统
1. 硬件系统
  1. CPU 中央处理单元
    + 2/GHZ    20多亿次/s
    + 一级缓存;二级缓存;三级缓存
  2. 内存REM,随机访问存储
    + 电信号存储的,快,内存的读写速度是硬盘的14万倍
    + ddr3 ddr4 ddr5 ,
  3. 硬盘ROM,只读存储
    + 机械单元存储
  4. 主板
  5. i/o设备
2. 软件系统
  1. 操作系统
    + PC端
      + windows
      + linux
      + unix
      + OS
    + 移动端
      + IOS
      + 塞班
      + windows
      + phone
  2. 应用软件
  + 浏览器
  + 编辑器
  + 微信
## 修改页面标题
1. document.tittle = '值';
## 表单提交事件
```js
$('form').submit(function(){
  //执行的代码即可,一般发送ajax请求
  //$(this).serialize();表单数据序列化
  //需要return false;不然页面会跳转,阻止默认行为
})
```





