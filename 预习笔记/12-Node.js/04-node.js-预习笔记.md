# 复习
## 
# 今日内容

## Express常用api
[官网](http://expressjs.com/)

#### 基本路由
get:
```js
app
  .get('/',function(req,res){
  res.send('ok');
  })
  .get('/public',function(req,res){
  res.send('ok');
  })
  .get('/viwes',function(req,res){
  res.send('ok');
  })//因为app.get返回的还是app,所以可以继续调用
```
post:
```js
app.post('/',function(req,res){
res.send('ok');
})
```

#### 静态服务
* 开放对应的资源
+ 写法:app.use('路径1',express.static('路径2'))
  - 路径1:url访问的路径(+需要访问的资源)
  - 路径2:开放的路径(里面的资源都可以访问)
```js
//情况一
//当以 /public/ 开头的时候,去 ./public/目录中去找对应的资源
app.use('/public/',express.static('./public/'));
//情况二
//没有第一个参数的时候,直接访问这个目录下的资源就可以了来访问 './public/';
//如访问public/index.html;在url地址栏中端口号后面直接写index.html即可
app.use(express.static('./public/'));
//情况三
//必须通过 /a/public目录中的资源具体路径来访问;
//访问 /a/public/login.html url地址栏中写  /a/login.html
app.use('/a/',express.static('./public/'));
```

#### express 结合 art-template
1. 安装
```shell
npm install --save art-template
npm install --save express-art-template
```
2. 配置
```js
app.engine('art', require('express-art-template'));
```
3. 使用
```js
app.get('/', function (req, res) {
    res.render('index.art', {
      title:'抬头',
    });
});
```
4. 示例
```js
//引入express文件
var express = require('express');
//创建app实例
var app = express();
//核心代码
app.engine('art', require('express-art-template'));
//第一个参数 'art' 当渲染以 .art 结尾的文件的时候,使用art-template 模板引擎;可以手动改为html
// express-art-template 专门用来在express 中把 art-template整合到express中;(前提是已经安装好了art-template文件)
// express为response对象提供了一个方法:render;这个方法默认是不可以使用的,需要配置模板引擎后使用
//如果默认不要views目录,可以手动设置;
//app.set('views','自定义render函数默认的路径')
app.set('view options', {
    debug: process.env.NODE_ENV !== 'production'
});

app.get('/', function (req, res) {
  //res.render('参数1',{参数2})
  //参数1:html模板名;不能写路径,默认会去项目中的views目录查找该模板文件;以'views/开始查找',所以这里写'views/'以后的路径即可
  //express约定,开发人员把所有的视图文件都方法views目录中;
  //如果engine('art')中写的art结尾,name下面也要是art结尾;前后一致
  //参数2:模板数据;可选参数
    res.render('index.art', {
        user: {
            name: 'aui',
            tags: ['art', 'template', 'nodejs']
        }
    });
});
```

#### 其他api
+ 重定向
  - 写法: res.redirect('路径')
+ 状态码简写
  - res.status(数字).send('内容')

#### 获取GET请求体数据
+ express内置了方法
```shell
req.query
# 可得到get请求的数据
```

#### 获取POST请求体数据 body-parser
1. 步骤
+ 安装
```shell
npm install --save body-parser
```
+ 配置
```js
var express = require('express')
//0.引包
var bodyParser = require('body-parser')
var app = express()
//配置body-parser
//只要加入这个配置,则在req请求对象上会多出来一个属性:body
//可以直接通过req.body来获取表单post请求体数据
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))

// parse application/json
app.use(bodyParser.json())

app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  //可以通过req.body获取表单数据
  res.end(JSON.stringify(req.body, null, 2))
})
```
#### 路由容器
1. 使用步骤
* 以学生管理系统students,入口模块以app.js为例
* 在单独的路由文件中将路由挂载到路由容器内
```js
var express = require('express');
//1.创建一个路由容器
var router = express.Router();
//2.把路由都挂载到router路由容器中
router.get('/students',function(req,res){
  //执行的代码
})
//3.把router导出
module.exports = router;
```
* 在使用的文件中,将路由容器挂载到app上
```js
var express = require('express');
var app = express();
var router = require('路由文件名');
//使用路由即可
app.use(router);
```

## nodemon
作用:修改完代码自动重启,是第三方命令行工具

### 使用步骤:
1. 全局安装
```shell
npm install --global nodemon
```
2. 使用
只要是通过 `nodemon app.js`启动的服务,它会自动监视文件变化,当文件发生变化的时候(ctrl+s的时候),自动重启服务器
```shell
#以启动app.js为例
nodemon app.js
```



# 引申
+ 模块标识中的 `/` 和 文件操作路径中的 `/`
  - 即readFile('路径')这种 
    + 文件操作中的相对路径可以省略`./`,如不写,默认是相对路径中去查找文件
    + `/`是磁盘根目录,和`c:/`或者`d:/`一样,写了就会在磁盘根目录中去找文件
  - 模块加载中的`./`不能省略,如果没有路径前缀,默认会按照找核心模块或者是第三方模块区查找,会报错
+ 配置模板引擎和获取post参数的插件body-parser 一定要在挂载路由 app.use(router)之前
+ 回调函数:获取异步操作的结果又称上层传递,下层调用
  - 如果需要获取一个函数中异步操作的结果,则必须通过回调函数来获取
  - 如果函数有多个形参,在调用的时候需要分不同的情况传递,为了方便获取参数,其他不需要传值的参数位置可以写null;
+ jQuery的Ajax方法,简写get请求
```js
$.get('路径?参数&参数',function(data){
})
```
+ ES6的方法
  - 数组方法find():
  根据条件查找元素 
  ```js
  var student = [
    {
      id:1,
      name:'pp',
    },
  ]
  [数组调用].find(function(item){
    //item就是每一项
    //当某个遍历项符合item.id === student.id条件的时候,find会中止遍历,同时返回遍历项
    return item.id === student.id
  })
  ```
  - 数组方法findIndex():
  根据条件查找元素下标
  ```js
  //当某个遍历项符合item.id === student.id条件的时候,findIndex会中止遍历,同时返回遍该元素的下标
[数组].find(function(item){
  return item.id === id
})
  ```

