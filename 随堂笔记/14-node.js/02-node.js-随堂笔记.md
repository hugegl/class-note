## 复习
+ 浏览器和服务器的通信过程
+ 浏览器的工作原理
+ 浏览器的五大请求部分
UI
Socket
Render Engine 
JavaScript Engine
Storage
+ web开发的本质
1.请求
2.处理
3.响应
+ Node.js
不是主流的web开发语言,目前用来做命令行工具的比较多
版本:LTS;Current
+ 执行Node.js
1.REPL;类似浏览器端的检查工具
2.执行js文件;在命令行工具内输入`node 文件名.js`
+ process.stdout.write
1.不会自动换行
+ global对象
+ 文件读写
1.fs.writeFire('路径','写入内容','编码格式',回调函数)
1.1 回调函数的形参 err;写入成功err是null
1.2编码格式;默认utf-8
2.fs.readFire('路径','编码格式',回调函数)
1.1 回调函数的形参 err data;写入成功data是对象,err是null
1.2编码格式;默认null,不传默认读出来是buffer对象
+ 路径 __dirname __filename
+ path.join
path.join('路径1','路径2',....)
+ 创建简单的http服务器
```js
var http = require('http')
var server = http.createServer();
server.on('request',function(req,res){
  res.end('响应结束')
})
server.listen(3000,function(){

})
```
+ 设置响应头的方法
1.res.setHeader(键,值) 一次只能设置一个响应头
2.res.writeHead(statusCode,statusMessage,{键:值}) 一次能设置多个响应头信息
这个两个方法必须在write之前调用
+ response的其他方法
response.write(参数)向浏览器返回数据 接收的参数:字符串,buffer对象
response.end(参数)参数同write
response.statusCode =值;
response.statusMessage = 值;
+ request.url
获取请求地址中的路径+参数
+ 路由
根据不同的url地址,返回不同的数据
## 今日内容

### MIME类型

定义:是一个第三方模块
作用:根据文件名称获取对应的content-type
使用步骤
```js
//初始化npm
npm init -y
//下载并安装mime
npm install mime
//引入模块
var mime = require('mime');
//常用方法
//mime.getType() 根据文件路径或者文件后缀名,获取content-type
mime.getType('aaa.js');//返回值就是对应的content-type;
mime.getType('a/b/aaa.js');
//mime.getExtension()根据content-type返回对应的文件后缀名
mime.getExtension('text/css');
```
[npm官网](www.npmjs.com)
### 使用node.js模拟phpstudy
```js
var http = require('http');
var fs = require('fs');
var path = require('path');
var server = http.creatServer();
var mime = require('mime');
server.on('request',fucntion(req,res){
res.setHeader('content-type',mime.getType(req.url));
  req.url = req.url=='/'?'/index.html':req.url;
  fs.readFile(path.join(__dirname,req.url),function(err,data){
    if(err){
      res.statusCode=404
      res.end('Not Found')
    } else{
      res.end(data)
    }
  })
})
server.listen(8888,fucntion(){
console.log('服务器开启成功)
})
```
### server事件request中回调函数内形参request对象的其他方法
```js
var http = require('http');
var server = http.createServer();
server.on('request',function(req,res){
//req.url是请求地址+参数,返回格式是字符串
//req.headers是请求报文中的请求头信息,是一个对象,包含请求报文的所有信息
//req.rawHeaders是请求报文中的请求头信息,是一个数组;(不推荐)
//req.httpVersion浏览器发送的http请求协议的版本号
//req.method获取请求方式GET/POST....
})
server.listen(3000,function(){
  console.log('服务器开启了');
})
```
### node.js获取请求参数
#### queryString模块
```js
var querstring = require('querystring');
querystring.parse('name=pp&age=18');//返回值就是{name:pp,age:18}
```
#### url模块解析参数
写法:
* url.parse(url,boolen)
* 参数url:要进行解析的路径
* 参数boolen:
* true会把整个对象中的query属性的值解析成对象;
*  false会把整个对象中的query属性的值解析成字符串;默认值
```js
var url = require('url');
  url.parse(url,boolen)
  url
  boolen;
```
#### get请求
get的参数在url地址栏内,所以,只要拿到url中的内容,通过字符串操作,即可得到参数
```js
var http = require('http');
var server = http.createServer();
var querstring = require('querystring');
server.on('request',function(req,res){
  //方法1自己截取字符串
  //方法2 queryString模块
  if(req.url.indexOf('?') != -1){
    var str = req.url.split('?')[1];//返回值name=pp&age=18
    var params = querystring.parse(str);//返回值是对象{name:pp,age:18}
  }
  //urlObj是一个对象,里面有pathname:路径部分内容;query:参数部分内容,默认情况是一个字符串//会自动处理没有传参数的情况
  var urlObj = url.parse(req.url,true);
   urlObj.query;//就是{name:pp,age:18}
   urlObj.pathname;//就是url的地址部分
})
server.listen(3000,function(){
  console.log('开启服务器');
})
```
### post请求
post请求在请求体中;没有大小限制,如果数据很大,是分多次发送给服务器的
```js
var http = require('http');
var server = http.createServer();
var querystring = require('querystring');
server.on('request',function(req,res){
  //0.定义一个数组,存放每次接收到的数据
  var bufferList = [];
//1.给req注册一个事件data事件;当有post请求的数据发送到服务器的时候,就会触发这个事件
req.on('data',function(chunk){
  //post请求的数据可能会分多次发送给服务器,每次发送给服务器都会触发data事件
  //每次发送的数据可以通过chunk来接收,chunk是一个buffer对象
  //每次有新数据来就将数据添加到数组中
  bufferList.push(chunk);
})
req.on('end',function(){
  //end事件会在post数据发送完毕之后触发,如果要获取数据,在end事件中获取;
  //需要将数组中所有的buffer对象合并成一个
  //buffer.concat方法进行buffer对象合并
  var result = Buffer.concat(bufferList);
  //如果想存起来直接用fs.writeFile('路径',result,function(){});直接写入文件即可;可以写入图片,视频等等;
  //如果要转成字符串则直接将 result.toString();
  result.toString();
  //将字符串转换成对象
  querystring.parse(result.toString());
})
})
server.listen(3000,function(){
  console.log('开启服务器');
})
```
### npm
+ 定义: node package manager
+ 三个组成部分
  - npm服务器:存储着npm中所有的包
  - npm网站:[npm网站](https://www.npmjs.com)负责浏览包的;直接搜索即可
  - npm命令行工具:上传和下载npm服务器上的包
+ npm安装 只要安装好了node ,npm就安装好了
#### npm命令行工具
在node装完之后,全局就有一个npm可以使用
+ 初始化一个package.json文件当前项目的描述文件
  - 右键新文件,自己输入文件名
  - 命令行工具内执行命令;一个项目只需要执行一次
  `npm init`
  `npm init -y`-y就是-yes,使用默认值创建
  - 作用 描述包的信息的
  有合格的package.json的文件夹就是一个包;官方定义:一组被package.json描述的文件;
  合格的定义:必须有两个属性name version
   - name 不能有中文,空格,大写字母,特殊字符;不能和现有的包同名
   如果有,则npm init命令执行会报错,报错之后,package.json中的name属性值为空,需要手动补全
   - version 版本信息
   版本概念:一般版本号都是包含3个数字,中间用.隔开
   格式: 主版本号.次版本号.修订版本号
   主版本号:当代码功能更新,更新之后,不兼容之前的版本了,那么需要更新主版本好
   次版本号:当代码功能更新,更新之后依然兼容之前的版本,知识新增了某些功能
   修订版本号:当你代码更新,更新的只是修复了某些bug或者优化了某些功能的时候更新修订版本号
  - 描述文件信息解释
  ```js
  {
  "name": "Desktop",//名字
  "version": "1.0.0",//版本
  "description": "",//描述信息
  "main": "text.js",//入口文件
  "scripts": {//shell命令,可以通过    npm run 命令别名    进行执行
    "test": "echo \"Error: no test specified\" && exit 1"//shell命令(在cmd或者git中输入的命令),复杂命令的别名
    //执行 npm run test命令就是执行npm echo \"Error: no test specified\" && exit 1
  },
  "keywords": [],//关键字,方便在npm网站上进行搜索
  "author": "",//作者
  "license": "ISC",//开源协议,自己指定即可
  "dependencies": {//依赖项(运行时依赖项)
    "mime": "^2.3.1"
  },
  "devDependencies":{//开发依赖项
    "键":"值,
  }
}
  ```
  - 执行scripts中的shell命令
  `npm run 别名`
  有的特殊命令的时候,可以省略run如 `npm start` `npm stop` ``;可以查看官网??????晚自习查看视频21,补全网址
  - dependencies 和 devDependencies
  dependencies:运行时依赖项,在将代码上传到服务器时,这个包仍被需要
  devDependencies:开发时依赖项,只需要开发时需要,上传到服务器的时候不需要
  储存依赖项的目的:为了代码共享的时候比较方便;方便多人共同开发;
  代码分享的时候,不需要分享node__modules,只需要分享自己的代码和package.json,其他人根据package.json下载所有的依赖项
  命令`npm install`这条命令会自动根据package.json中保存的包信息进行下载(默认下载两种依赖项dependencies+devDependencies)
  `npm install --production`只下载dependencies(依赖项)
  - 如何将依赖项的信息保存到 dependencies 和 devDependencies 中
  老版本的npm中,依赖项信息不会自动保存,需要自己保存
    1.将依赖项的信息保存到 dependencies;
    `npm install 包名称 --save`
    `npm install 包名称 -S`简写
    `npm install 包名称`
    2.将依赖项的信息保存到 devDependencies
    `npm install 包名称 --save-dev`
    `npm install 包名称 -D`简写
+ 下载包(本地安装)  下载的包会放在当前项目中
`npm install 包名称`默认下载最新版
`npm install 包名称1 包名称2`一次下载多个包
`npm install 包名称@版本号`下载指定版本的包
`npm i 包名称`简写
+ 卸载包
  - 手动,点击,删除
  - 命令
  `npm uninstall 包名称`

### 全局安装

  当使用一个包,这个包会提供一个全局命令的时候,这个包就需要被全局安装
  命令 `npm install 包名称 -g`-g是--global,全局的意思
  常用的需要全局安装的包
  `live-server`轻量级的服务器包
  `less`用来将less转换成css的代码

### nrm

npm服务器在国外,下载速度较慢,可以设置npm,让其下载包从国内服务器上进行下载
+ nrm安装
  命令`npm install nrm -g`
+ 使用
 1.查看所有的可用的服务器列表`nrm ls`
 2.查看当前正在使用的服务器`nrm current`
 3.切换到指定的服务器`nrm use 服务器名称`
 4.测速命令
 `nrm test 指定服务器名称`测试指定服务器的命令 
 `nrm test`测试所有服务器的命令

 ### hacknews案例

 ```js
 var http = require('http');
 var server = http.createServer();
 var fs = require('fs');
 var path = require('path');
 var url = require('url');
 server.on('requset',function(req,res){
   //通过url模块将url封装成对象
   var urlObj = url.parse(req.url,true)
//1.设置路由规则
if(req.url=='/'||req.url=='/index'){
  fs.readFile(path.join(__dirname,'public','index.html'),function(err,data){
    if(err){
      res.statusCode=404;
      res.end('访问失败');
    }else if(){
      res.end(data);
    }
  })
}else if(urlObj.pathname=='/submint'){

}else if(req.url.indexOf('/public')===0){

}
 })
 server.listen(3000,function(){
   console.log('开启服务器')
 })
 ```

##引申
+ gulp 自动化构建工具[网址](https://www.gulpjs.com.cn/)









