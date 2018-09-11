# 复习
1. hacker-news案例
## 基础版(代码供参考,未测试)
```js
var fs = require('fs');
var path = require('path');
var mime = require('mime');
var url = require('url');
var http = require('http');
var server = http.creatServer();
var tempplate = require('art-template');
server.on('request',function(req,res){
  var urlObj = url.parse(req.url,true);
if(req.url=='/'||req.url=='/index'){
  fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,newsList){
    newsList = JSON.parse(newsList||'[]');  
    fs.readFile(path.join(__dirname,'views','index.html'),function(err,data){
     var render = template.compile(data.toString());
     var result = render({list:newsList});
     res.end(result)
    })
  })
}else if(urlObj.pathname=='/details'){
   fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,newsList){
     var news = newsList.find(function(v,i){
       return v.id = urlObj.query.id;
     })
    fs.readFile(path.join(__dirname,'views','index.html'),function(err,data){
     var render = template.compile(data.toString());
     var result = render({item:news});
     res.end(result)
    })
  })
}else if(req.url=='/submit'){
  fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,newsList){
    newsList = JSON.parse(newsList||'[]');  
    fs.readFile(path.join(__dirname,'views','submit.html'),function(err,data){
     var render = template.compile(data.toString());
     var result = render({list:newsList});
     res.end(result)
    })
  })

}else if(urlObj.pathname=='/add'){
  var news = urlObj.query;
  fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,newsList){
    newsList = JSON.parse(newsList||'[]');  
    news.id = newsList.length==0?1:newsList[newsList.length-1].id+1
    newsList.push(news);
    fs.writeFile(path.join(__dirname,'data.json'),'utf8',function(err){
      res.setHeader('location','/');
      res.statusCode = 302;
      res.end();
    })
  })
}else if(req.url.indexOf('/resourses')==0){
res.setHeader('content-type',mime.getType(req.url));
 fs.readFile(path.join(__dirname,req.url),function(err,data){
   res.end(data)
 })
}else{
  res.statusCode=404;
  res.statusMessage = 'Not Found';
  res.end('Not Found')
}
})
server.listen(3000,function(){
  console.log('open')
})
```
## 优化版(代码供参考,未测试)
```js
var fs = require('fs');
var path = require('path');
var mime = require('mime');
var url = require('url');
var http = require('http');
var server = http.creatServer();
var template = require('art-template');
//封装获取所有的新闻数据
function getAllNews(callback){
   fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,data){
    data = JSON.parse(data||'[]');  
    callback && callback(data);
  })
}
//封装根据id获取新闻数据
function getNewsById(id,callback){
   getAllNews(function(newList){
     var news = newList.find(function(v,i){
       return v.id == id;
     })
     callback && callback(news)
   })
}
//封装添加数据的函数
function addNews(news,callback){
 getAllNews(function(newList){
   news.id = newsList.length==0?1:newsList[newsList.length-1].id+1
   newList.push(news);
   fs.writeFile(path.join(__dirname,'data.json'),JSON.stringify(newsList),function(err){
    callback && callback()
   })
  })
}
server.on('request',function(req,res){
  var urlObj = url.parse(req.url,true);
  //封装渲染函数
  res.myRender = function(url,obj){
    fs.readFile(path.join(__dirname,'views',url+'.html'),function(err,data){
      var result = data;
      if(obj){
        var render = template.compile(data.toString());
        result = render(obj);
      }
     this.end(result)
    })
  }
  //封装重定向函数
  res.redirect = function(url){
      this.setHeader('location',url);
      this.statusCode = 302;
      this.end();
}

if(req.url=='/'||req.url=='/index'){
   getAllNews(function(newList){
    res.myRender('index',{list:newsList})
   })
}else if(urlObj.pathname=='/details'){
   getNewsById(urlObj.query.id,function(newList){
    res.myRender('details',{item:news})
   })
}else if(req.url=='/submit'){
  res.myRender('submit')
}else if(urlObj.pathname=='/add'){
   addNews(urlObj.query,function(){
     res.redirect('/');
   })
}else if(req.url.indexOf('/resourses')==0){
res.setHeader('content-type',mime.getType(req.url));
 fs.readFile(path.join(__dirname,req.url),function(err,data){
   res.end(data)
 })
}else{
  res.statusCode=404;
  res.statusMessage = 'Not Found';
  res.end('Not Found')
}
})
server.listen(3000,function(){
  console.log('open')
})
```
## 模块化版(代码供参考,未测试),下课整理??????
```js
//文件1,主模块,构建http服务器
var http = require('http');
var server = http.creatServer();
var extend = require('extend');
var router = require('router');
server.on('request',function(req,res){
  extend(req,res);
  router(req,res);
})
server.listen(3000,function(){
  console.log('open')
})

//文件2,构建路由规则
var handler = require('./handler');
module.exports = function(req,res){
  if(req.url=='/'||req.url=='/index'){
    handler.indexHandler(req,res)
  }else if(urlObj.pathname=='/details'){
    handler.detailHandler(req,res)
  }else if(req.url=='/submit'){
    handler.submitHandler(req,res)
  }else if(urlObj.pathname=='/add'){
    handler.addHandler(req,res)
  }else if(req.url.indexOf('/resourses')==0){
    handler.staticHandler(req,res)
  }else{
    handler.notFoundHandler(req,res)
  }
}


//文件3 handler ,制定路由具体执行的事情
module.exports = {
  indexHandler:function(req,res){

  },
  detailHandler:function(req,res){

  },
  submitHandler:function(req,res){

  },
  addHandler:function(req,res){

  },
  staticHandler:function(req,res){

  },
  notFoundHandler:function(req,res){

  },
}
//文件4 extend ,增强req,res的功能
module.exports = function(){
    res.myRender = function(url,obj){
    fs.readFile(path.join(__dirname,'views',url+'.html'),function(err,data){
      var result = data;
      if(obj){
        var render = template.compile(data.toString());
        result = render(obj);
      }
     this.end(result)
    })
  }
  res.redirect = function(url){
      this.setHeader('location',url);
      this.statusCode = 302;
      this.end();
  }
  req.urlObj = url.parse(req.url,true);

}
//文件5 storage ,数据操作的模块
module.exports = {
//封装获取所有的新闻数据
getAllNews : function (callback){
   fs.readFile(path.join(__dirname,'data.json'),'utf8',function(err,data){
    data = JSON.parse(data||'[]');  
    callback && callback(data);
  })
},
//封装根据id获取新闻数据
getNewsById : function (id,callback){
   getAllNews(function(newList){
     var news = newList.find(function(v,i){
       return v.id == id;
     })
     callback && callback(news)
   })
},
//封装添加数据的函数
addNews : function (news,callback){
 getAllNews(function(newList){
   news.id = newsList.length==0?1:newsList[newsList.length-1].id+1
   newList.push(news);
   fs.writeFile(path.join(__dirname,'data.json'),JSON.stringify(newsList),function(err){
    callback && callback()
   })
  })
}
}

var fs = require('fs');
var path = require('path');
var mime = require('mime');
var url = require('url');
var http = require('http');
var server = http.creatServer();
var tempplate = require('art-template');

server.on('request',function(req,res){
  var urlObj = url.parse(req.url,true);
  //封装渲染函数

if(req.url=='/'||req.url=='/index'){
   getAllNews(function(newList){
    res.myRender('index',{list:newsList})
   })
}else if(urlObj.pathname=='/details'){
   getNewsById(urlObj.query.id,function(newList){
    res.myRender('details',{item:news})
   })
}else if(req.url=='/submit'){
  res.myRender('submit')
}else if(urlObj.pathname=='/add'){
   addNews(urlObj.query,function(){
     res.redirect('/');
   })
}else if(req.url.indexOf('/resourses')==0){
res.setHeader('content-type',mime.getType(req.url));
 fs.readFile(path.join(__dirname,req.url),function(err,data){
   res.end(data)
 })
}else{
  res.statusCode=404;
  res.statusMessage = 'Not Found';
  res.end('Not Found')
}
})
server.listen(3000,function(){
  console.log('open')
})
```
2. 模块化
  + 定义模块
    - js文件可以作为一个模块
    - 模块有模块作用域
  + 引用模块
    - require(参数)
    - 参数:包名
    - 参数:路径
  + 导出项的设置
    - module.exports
    - exports
  + 导入(引用模块并且接受其导出项)
    - `var 导出项 = require(参数)`

# 今日内容

## Express框架
基于Node.js平台,快速,开放,极简的web开发框架

### 使用步骤
  1. 创建一个项目文件
  2. `npm init`
  3. `npm install express`
  4. 新建一个js文件
  5. 初体验
  ```js
  //1.引包
  var express = require('express');
  //2.创建express实例
  var app = express();
  //3.通过实例监听指定端口
  app.listen(3000,function(){
    console.log('open');
  })
  //4.直接注册路由规则即可
  app.get('/',function(req,res){
  res.send('你好世界');//
  //req和res是原生的对象,框架对这两个对象进行了增强操作;
  })
  ```

### 路由注册的方式
路由:根据不同的url地址,返回不同的内容
1. app.'方式名'()
  + 请求方式必须和方法名一致
  + 请求的路径也必须和注册路由的路径一模一样
  ```js
  app.get('路由路径',function(req,res){
    
  })
  app.post('路由路径',function(req,res){

  })
  app.delete('路由路径',function(req,res){

  })
  ```
2. app.all()
  + 任意请求方式都可以
  + 请求的路径必须和注册的路径一致
  ```js
  app.all('路由路径',function(req,res){

  })
  ```
3. app.use()
  + 任意请求方式都可以
  + 请求的路径只要以注册的路由路径开头即可
  ```js
  app.use('路由路径',function(req,res){
    //如果'路由路径'是'/',可以省略不写
  })
  ```
+ 注意同一个路径同一种方式注册的,只能第一个生效,匹配到第一个之后就不再继续往下找了

### express 中 req 和 res 对象新增的功能
1. res对象
  + res.sendFile('参数') 向浏览器返回文件;参数是文件路径
  + res.send(参数) 向浏览器响应数据
    - 参数
      + 字符串
      + 对象
      + 数组
      + 数字会被当成状态码使用
      + buffer对象
    - 里面自动调用res.end();
    - res.send方法只能调用一次
    - 如果send里面是undefind则,自动处理成空字符串
  + res.download('路径',filename) 提供文件下载
    - 路径:被下载的路径地址,必传参数
    - filename:用户默认保存的名字,可选参数
  + res.status(数字);设置状态码,可以进行链式编程
  + res.json(参数)(了解)
    - 参数:对象
  + res.jsonp(参数);可以返回jsonp格式的数据,请求的时候需要传递callback参数(用作函数名,必传,如不传则返回普通的json数据)
    - 参数:对象
  + res.redirect('路径') 重定向
  + res.render('模板文件名称',数据对象);需要配合模板引擎使用
```js
var express = require('express');
var app = express();
var path = require('path');

//0.下载模板引擎
//先下载 art-template;再下载express-art-template

//1.指定对应的模板引擎
//app.engine可以用来未指定的后缀的模板指定对应的模板引擎
//app.engine('模板文件的后缀名',对应的模板引擎提供的内容)
app.engine('html',require('express-art-template'))

//2.设置模板文件所在的目录;如果不设置,则默认会去views文件中找
//app.set('views',path.join(__dirname,'指定文件路径'))views是固定的
app.set('views',path.join(__dirname,'aaaa'))

//3.设置模板文件的默认后缀(为了省略调用render方法的时候文件的后缀名)
app.set('view engine','html');

app.get('/',function(req,res){
//res.render('模板文件名称',数据对象)
  res.render('index',{item:items})
})
app.listen(3000,function(){
  console.log('open')
})
```
  + res.sendFile('文件路径');向浏览器响应文件
2. req对象
  + req.baseUrl  ???补视频
  + req.body 获取post请求,需要配合中间件 body-parser 使用
```js
//安装body-parser
var bodyParser = require('body-parser');
//注册use事件,在事件函数中body增加到req对象上,增加参数的获取
app.use(bodyParser.urllencoded());//处理urllencoded格式的数据
app.use(bodyParser.urllencoded({extended:false}));//默认是true,需要传成false,内部会用querystring模块去转成对象;不传参数的,会用qs模块(一个第三方模块)已经被废弃了;新版本的可能会移除;报错警告:deprecated,可能会淘汰的警告
app.use(bodyParser.json());//处理json格式的数据
//在下游就可以通过req.body获取到post请求的参数,这里是通用路径,所以后面的不同的路由规则均可获取到带有body属性的req对象
req.body;//返回值就是post请求的参数
```
自己封装body-parse,处理不同格式的
```js
//x-www-form-urlencoded 拿到的数据key=value&key=value
//application/json 拿到的数据是 {key:value,key:value}
//req.get('content-type');//获取请求路径的content-type
var querystring = require('querystring');
var express = require('express');
var app = rexpress();
app.use(function(req,res){
  var bufferList = [];
  req.on('data',function(chunk){
    bufferList.push(chunk)
  })
  req.on('end',function(){
    var result = Buffer.contcat(bufferList);
    result = result.toString();
    //通过req.get('content-type')获取发送请求的数据的格式
    if(req.get('content-type').indexOf('json') != -1){
      req.body = JSON.parse(result);
    }else if(req.get('content-type').indexOf('urlencoded') != -1){
      req.body = querystring.parse(result);
    }else{
      req.body = {};
    }
  })
})
```
  + req.query 获取get请求参数
  + req.originUrl 获取原始的url地址,类似于req.url
  + req.path 获取请求路径的,类似于UrlObj.pathname
  + req.params  获取路由参数
    - 路由参数
    - 在注册路由规则的时候,可以指定路由路径中的某一部分作为参数
  + req.get(key');获取请求头中key对应的信息
  ```js
  //利于SEO
  //定义的路由规则为    '/details/:id'
  //用户访问的时候    '/details/具体的id值'
  //1.设置一个占位符
  app.get('/details/:id',function(req,res){
    //req.params拿到的对象    {id:具体的id值}
  })
  //1.设置一个可有可无的占位符
    //用户访问的时候    '/details/具体的id值';
    //用户访问的时候    '/details';
  app.get('/details/:id?',function(req,res){
  })
  //2.设置多个占位符
  //用户访问的时候    '/details/1/pp';
  app.get('/details/:id/:name',function(req,res){
    //req.params拿到的对象    {id:1,name:'pp'}
  })
  ```

### 路由挂载Router
  ```js
  //文件1 主文件 
  var router = require('./router');//./router是router的文件路径
  //引用router路由挂载
  app.use(router);

  //文件2  router文件
  //router 对象 ,可以用来注册路由规则
  var router = express.Router();
  //将路由规则挂载到router对象上
      router.get(......)
      router.post(......)
      router.use(......)
      router.get(......)
  module.exports = router;
  ```


### 托管static
```js
//express.static是express中唯一提供的内置中间件
//用户可以通过   /index.html访问到public下面的文件
app.use(express.static('public'));//public是要托管的静态资源的文件夹名字
//用户可以通过   /public/index.html访问到public下面的文件
app.use('/public',express.static('public'))
```

### 中间件
1. 概念:就是一个函数,这个函数有三个参数,req,res,next
  + req请求对象,是不会变的,对象中的内容会增减
  + res响应对象,是不会变的,对象中的内容会增减
  + next用来调用下一个对象
2. 中间件函数中必须选择next的去向
  + 结束本次响应过程
  + 调用下一个中间件
  + express中默认有个中间件,这个中间件是用来执行的是404;
  + next();调用与否是要和本次路由规则一样的,才会被执行
```js
app.get('/index',function(req,res,next){
  next();
  //调用下一个和这个路由规则一样的函数,如果有就执行,如果没有就404
  //在本次函数中给req和res增加的东西,在下一个路由规则中也可以被使用
})
app.get('/index',function(req,res,next){
 res.send('第二次index页面');
})
```
## 框架和类库
### 框架 Framework
整个应用程序的逻辑全部由框架控制,我们只提供相应的代码,这些代码框架会自动在合适的时机进行调用;
1. 控制反转(ToC).控制权反转
2. 框架原则: dont call us,we will call you ;(好莱坞原则)
### 类库 Library
类库中只提供方法,这些方法具体在哪里调用,需要用户自定义;



# 引申



