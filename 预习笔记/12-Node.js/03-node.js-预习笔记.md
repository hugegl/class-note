# 反馈
## 前端入门书籍:
《JavaScript 高级编程》第3版
《JavaScript 语言精粹》
## 软件版本;涉及到软件工程学:
X(新增功能比较多,甚至可能去除了某些功能).X(加入了新功能).X(修复bug,提升性能)
一般是客户端软件,技术框架开发者比较理解的多;
做网站很少涉及到版本的概念,网站的目的就是快,最新的;
## each 和 forEach
forEach()是ES5中原生JavaScript方法,所有数组均可使用的方法,EMS5;IE8不支持;
each()是jQ封装的方法,通过$('对象')返回出来的伪数组调用;1.1.0版本的可以兼容IE8;
调用: 
* $.each([变量的数组],function(i,v){执行代码});//遍历传进来的数组;
* $('div').each(function(i,v){执行代码});//遍历获取到的div伪数组;
jQ对象调用forEach方法
```js
//slice(start,end)  截取数组,start开始end结束,包括start,不包括end;返回值是截取的数组,如果不传参数,默认把原来的数组返回
[].slice.call(jQ对象);//将函数slice的this改变成指向jQ对象,最后返回出来一个数组,就可以调用forEach方法了.
```
## 网页中所有的路径都是url路径,不是文件路径
# Node中的模块系统
## 使用node编写应用程序主要就是在使用:
### EcmaScript语言
和浏览器不一样,没有BOM和DOM
### 核心模块
* 文件fs 
* http服务的http
* yrl路径操作
* path路径处理
* os操作系统信息
### 第三方模块
art-template 
必须通过npm来下载才可以使用
### 自定义模块
自己创建的模块
# 什么是模块化
文件作用域
通信规则;加载require;导出
# commonJs模块规范
## 在node中的JavaScript有模块系统
模块作用域
* 使用require方法用来加载模块
- require('fs');不加/路径是加载内置模块,如果加载第三方或者自定义模块,需要传路径类似./;fs是模块标识符,非路径模式的
* 使用exports接口对象来导出模块中的成员
- 默认使用对象中的成员只能通过.成员拿到;
- 如果某个模块需要直接导出某个成员,而不是通过挂载的方式,需要使用以下方式:
- module.exports = 成员;
### 加载 require
语法:
`var 变量名 = require('参数')`
参数有两种
+ 模块标识符 
 - 核心模块,如`fs`,`http`,`path`等
 - 核心模块已经被编入到二进制文件中,在exe中;
 - 第三方模块,如`art-template`等;
+ 路径
 - 自定义的文件`./aa.js`,`../bb,js`等,以路径开始的,根目录`/`和`c:/`基本不用;后缀名`.js`可以省略
两个作用:
* 执行被加载模块中的代码
* 得到被加载模块中的`exports`导出接口对象
#### 加载规则
* 优先从缓存加载,不会重复加载
* 核心模块
* 路径形式的文件模块
* 第三方模块
* 深入浅出Node.js(三):深入Node.js的模块机制;书作者朴霖《深入浅出Node.js》
##### 加载第三方模块
第三包和核心模块的名字不可能一样;
加载原理: 既不是核心模块,也不是路径形式的模块;
完整的查找规则是:
+ 以art-template为例`当前文件所处目录中的node_modules/art-template/package.json`找到`main`属性;main属性的值就记录了art-template的入口模块,然后加载这个第三方包,本质上最终加载的还是文件
+ 如果package.json文件不存在或者main指定的入口模块也没有,则node 会自动找该目录下的`index.js`;index.js就是默认备选项;
+ 如果以上条件不成立,则往上一级目录中的node_modules目录中查找,直到找到根目录,如果还是没有,最后报错`can not find module XXX`
注意:
* 一个项目有且只有一个node_modules,放在项目根目录中,项目中所有的代码都会加载到第三方包
### 导出exports
* node中是模块作用域,默认文件中所有成员只在当前文件模块有效
* 如果需要被外界访问,将成员挂载到`exports`接口对象上
导出多个成员,通过`exports.`调用
```js
//方法一
exports.a =123
exports.b = 'string'
exports.d = function(){
      //函数体
}
//方法二
 module.exports = {
       '成员名':'值',
       '成员名':'值',
       '成员名':'值',
 }
```
导出一个成员,通过`module.exports`访问,拿到的就是导出的值
```js
 module.exports = '单个成员';
 //后者会覆盖前者
 module.exports = '覆盖内容';
```
#### exports 和 module.exports 原理解析
exports 是 module.exports 的一个引用
```js
console.log(exports === module.exports )// => true
exports.foo = 'bar'
//等价于
module.exports.foo = 'bar' 
```
默认
```js
var module ={
    exports:{

    }  
}
exports = module.exports;
//如果直接给exports赋值,只是断开了exports和module.exports的连接,exports的指向发生改变,并不会被return出来;
//但是重新exports = module.exports,又是建立了连接,后面在给exports赋值还是会return出来
//模块最后return 的是module.exports;
```
## npm
命令//详细见随堂笔记
+ 初始化
 - `npm init`默认安装,有向导
 - `npm intit -y`一路都是yes,跳过向导
+ 下载包
 - `npm install --save 包名`和`npm install  包名 --save`都可以安装包,并保存到依赖项中dependencies
+ 升级npm
 - `npm install --global npm`
### 淘宝镜像和cnpm
[网址](http://npm.taobao.org/)
+ 手动安装,不想安装cnpm,又想使用淘宝的服务器来下载
 - `npm install 包名--registry=https://registry.npm.taobao.org`
+ 每次手动加参数麻烦,可以把这个选项加入到配置文件中
 - `npm config set registry https://npm.taobao.org --global`
 - 查看npm配置信息`np config list`
配置完后,以后可以通过`npm install`通过淘宝的服务器来下载
# Express
是http的第三方框架,Node中有很多,这边以Express为主;
快速,开放,轻量,为node.js开发的web开发框架 
## 基本使用步骤
1.安装
2.引包
```js
var express = require('express')
```
3.创建服务器应用程序
```js
var app = express()
```
4.当服务器收到请求的时候,执行回调函数
```js
//当服务器收到get请求 / 的时候,执行回调函数
app.get('/',function(req,res){
      //拿到get的查询字符串参数
      req.query;//返回值是个{name=pp,age=18},只能用来获取get请求的参数
      //使用模板引擎,查看art-template官方文档,art-template结合express使用
      res.render('文件名',{模板对象})
      res.send('ok');
})
//公开指定目录,公开public目录
app.use('/public/',eapress.static('./public/'))
```
5.相当于server.listen
```js
app.listen(3000,function(){
      console.log('open');
})
```
# 引申
* node.js默认服务端的东西都是不开放的,想开放的需要自己写代码允许用户访问;
* php是默认让Apache代理了服务器,默认www内的文件都开放;
* 状态码 301永久重定向 浏览器会记忆;302临时重定向 浏览器不会记忆

















