## 复习
  * node.js模拟phpStudy
  ```js
  var http = require('http');
  var server = http.createServer();
  var fs = require('fs');
  var path = require('path');
  var mime = require('mime');//需先下载
  server.on('request',function(req,res){
    res.setHeader('content-type',mimie.getType(req.url))
  fs.readFire(path.join(__dirname,'public',req.url),function(err,data){

  })
  })
  server.listen(3000,function(){
    console.log('open')
  })
  ```
  + Request对象属性
    - req.url
    - req.headers
    - req.rawHeaders
    - req.method
    - req.httpVersion
  + 请求参数的获取
    - get请求参数获取
    ```js
    var url = require('url')
    var urlObj = url.parse(req.url,true)
    //urlObj.pathname
    //urlObj.query
    ```
    - post请求参数
    ```js
    var buffeList = [];
    var querystring = require('querystring')
    req.on('data',function(chunk){
      buffeList.push(chunk);
    })
    req.on('end',function(){
    var res = Buffer.contcat(buffeList)
    res = res.toString
    var params = querystring.parse(res)
    })
    ```
  + NPM
  1. 初始化一个package.json
  `npm init`
  `npm init -y`
  2. 下载包
  `npm i 包名`
  `npm install`
  `npm install --production`
  `npm i 包名@版本号`
  `npm i 包名@版本号 包名@版本号 包名@版本号`
  3. 卸载包
  `npm uninstall 包名`
  4. 保存依赖信息
  dependencies
  `npm i 包名`
  `npm i 包名 --save`
  `npm i 包名 -S`
  devDependencies
  `npm i 包名 --save-dev`
  `npm i 包名 -D`
  + package.json
    - 包括两个属性, name 和 version
    - name不能有中文,空格特殊字符等
    - version 版本号
    - scripts:shell命令的别名,运行`npm run 别名`
  + NRM
  切换npm服务器镜像
    - `nrm ls`展示所有服务器
    - `nrm use 服务器名称`
    - `nrm current`
    - `nrm test`
    - `nrm add 服务器名称 地址`
    - `nrm test 服务器名称`
  + Hacker-News 案例
    ```js
    var http = require('http')
    var server = http.createServer()
    var mime = require('mime')
    var path = require('path')
    var url = require('url')
    server.on('requset',function(req,res){
      //少了urlObj那一部分,下课后补齐
      var urlObj = url.parse(req.url,true)
      if(urlObj.pathname=='/index'|| urlObj.pathname=='/'){
        fs.readFile(path.join(__dirname,'views','/index.html'),function(err,data){
          res.end(data)
        })
      }else if(urlObj.pathname == '/details'){
  //同其他的路由,地址
      }else if(urlObj.pathname == '/submint'){
  //同其他的路由,地址
      }else if(urlObj.pathname.indexOf('/resouces')==0){
        res.setHeader('content-type',mime.getType(req.url))
        fs.readFile(path.join(__dirname,req.url),function(err,data){
          res.end(data)
        })
      }else{
        res.statusCode=404;
        res.end('未找到')
      }
    })
    server.listen(3000,function(){
      console.log('open')
    })
    ```

## 今日内容
## Hacker-News 案例
1. 基本实现功能
  + 使用文件保存数据
    - 使用json文件保存,读取的时候用字符串转换即可
  + 写入数据,先读出旧的数据,转成数组,更新数组,转成json字符串后写入到文件中
  + 模板引擎在node.js中使用
    - 以文件作为模板
    - `template(文件路径,对象)`
    - 以字符串变量作为模板
    - `var render = template.compile(字符串)`
    - `render(对象)`
2. 优化
  + 封装数据操作的方法,跟数据相关的方法都封装成方法,(异步结果需要使用回调函数传参)
  + 封装渲染函数,跟渲染相关的
3. 
### 数据持久化
使用json格式的文件存储
1. 读取数据
  + 读取文件,使用JSON_parse('字符串')将读取到的字符串转成对象
2. 写入数据
  + 读取文件,拿到数组
  + 在数组后面追加新元素,元素的内容由用户提供,通过post拿到数据;id需要自己写,找到最大的id+1即可(如果长度是0,则id是1)
  + 将准备的新数组JSON_stringify(数组)转换成json字符串,将数据写入到文件中;
### 在node.js中使用模板引擎
模板引擎art-template是腾讯写的,前后端均可使用(浏览器端,node.js)
+ 其他模板引擎
  - ejs
  - pug
1. 使用步骤
+ 安装art-template
`npm install art-template`
+ 引入文件
```js
var template = require('art-template')
```
+ 准备模板
  - 以文件作为模板
    `template('文件路径',对象)`
  - 以字符串变量作为模板;浏览器端也可以使用
  ```js
    //根据模板字符串创建渲染函数
    var render = template.compile('要渲染的字符串');//返回值的是一个渲染函数
    //调用函数渲染
    var result = render('要渲染的数据对象');//返回值就是拼接好的数据,????是字符串格式吗????
  ```
### 在node.js中重定向
  1. 步骤
  + 设置状态码;使用302临时重定向
  `res.statusCode = 302`
  + 设置状态新新
  `res.statusMessage = 'Found'`
  + 设置响应头中location,告诉浏览器需要跳到哪个页面去
  `res.setHeader('location','/')`
  + 结束响应
  `res.end()`

## node.js模块化

### 模块化概念
+ 定义: 将代码按照一定的规则拆分成一个个小单元(模块)的过程,称之为模块化
+ 意义: 
  - 便于代码维护
  - 便于代码复用

### 模块化标准
标准的意义在于让模块更加通用,有以下几种:
+ AMD:异步模块定义 Async module Defineation;如require.js,依赖前置
+ CMD:通用模块定义 Common module Defineation;如sea.js,依赖延迟  as lazy as possible
+ CommonJS:node.js模块化标准

### node.js中的模块分类
1. 核心模块(内置模块),如fs path url http querystring
2. 第三方包模块,如mime art-template moment
3. 目录模块
4. 文件模块

### node.js如何定义模块
1. 一个js文件就是一个模块
2. 每个模块都有自己单独的作用域


### node.js如何引用模块
1. 使用require(参数)方法
  + 参数`路径`,自定义模块,后缀名`.js`可以省略;自定义模块又叫文件模块/目录模块
    - 按照路径查找对应的文件,如果找到就直接引入
    - 如果没有找到,找文件名对应的 .js .json .node
    - 如果没有找到,就找路径对应的文件夹
      + 如果找到对应的文件夹,判断当前文件夹中是否有package.json文件,则找main属性,
        - 如果main属性不存在,就找以index开头的 .js .json .node文件
        - 如果main属性存在,则以main属性的值引入;
      + 如果没有,就找以index开头的 .js .json .node文件
    - 如果没有找到就报错
  + 参数`模块名`,核心模块/第三方包模块
    - 查找顺序
      + 当require函数接收到一个包名称的时候,
      + 会先去核心模块中是否有对应的模块,如果找到了就直接使用
      + 如果没有找到,就是node_modules中查找对应的模块,如果找到了就直接使用
      + 如果没有找到,就会去上一级目录中的node_modules中找,如果找到了就直接使用
      + 如果没有找到继续往上找,直到找到根目录(磁盘根目录),如果找到就直接使用
      + 如果还没有找到就报错`can not find module XXX`
      + package.json中的main的属性,告诉require函数在引入当前包的时候,具体引用哪个文件
      + 如果main属性没有值,name默认去找index.html,如果没有就报错;
2. 引用模块会执行模块里面的代码
3. 引用模块会得到导出项




### 自定义模块导出项的设置和接收
提供给外界使用
1. module.exports
+ 默认module.exports是一个空对象;//{}
+ module.exports.挂载名 =导出项;//{挂载名:导出项}
+ module.exports = 导出项;//导出项
```js
//1.设置导出项
module.exports.名 = 导出内容;
module.exports = 导出项
//2.获取导出项
//module.exports是什么,require之后的返回值就是什么
var 导出项 = require('模块路径');
```
2. exports 和 module.exports
module.exports和exports都可以用来导出内容,但是exports只能给对象中添加属性来导出内容,不能直接用来赋值,因为最后导出的是module.exports;给exports重新赋值,只是切断了exports和module.exports的联系,并不能变成导出项
```js
module.exports.名 = 导出内容;
exports.名 = 导出内容;
//上述两个方法效果一样
exports = 导出内容;//无效,因为最后导出的是module.exports
```


## 引申
### JSON_parse('字符串')
  - 如果传进来是空的,会报错,所以` JSON.parse('字符串' || '[]')`
### ES5中数组方法的整理
  1. find();找数组中符合条件的第一个元素
  ```js
    ['数组'].find(function(v,i){
      //v是每一项元素,当前正在遍历的元素
      //i是对应下标
      return boolen; 
      //return条件符合是true,就返回当前正在遍历的元素,return后面的boolen是动态计算的,true就返回;false就继续遍历
      //如果找不到返回undefind
    })
  ```
  2. forEach();遍历数组
  ```js
  ['数组'].forEach(function(v,i){
  //v是每一项元素,当前正在遍历的元素
  //i是对应下标
  //数组中有多少个,遍历多少次
  })
  ```
  3. map();映射数组
  ```js
  var ['新数组'] = ['数组'].map(function(v,i){
  //v是每一项元素,当前正在遍历的元素
  //i是对应下标
  //数组中有多少个,遍历多少次
  return v*2;//将结果追加到新数组中
  })
  ```
  4. some();判断数组中是否有任意元素满足指定条件
  ```js
  ['数组'].some(function(v,i){
  //v是每一项元素,当前正在遍历的元素
  //i是对应下标
  return v % 2 ==0;
  //只要有一个元素符合条件.就返回true,不再继续遍历
  })
  ```
  5. every();判断数组中是否所有元素满足指定条件
  ```js
  ['数组'].every(function(v,i){
  //v是每一项元素,当前正在遍历的元素
  //i是对应下标
  //数组中有多少个,遍历多少次
  })
  ```
  9. filter();在数组中找所有满足条件的元素
  ```js
 var ['新数组'] =  ['数组'].filter(function(v,i){
  //v是每一项元素,当前正在遍历的元素
  //i是对应下标
  //数组中有多少个,遍历多少次
  return v % 2 !=0;//会把所有符合条件的追加到新的数组中去;
  })
  ```

### 代码优化
  + 将冗余的代码方法,封装成函数,直接调用,使代码简洁
  + 写代码分模块操作的原则是单一职责

### 前端渲染和后端渲染