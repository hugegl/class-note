# node.js简介
+ 定义:不是编程语言,是JavaScript运行环境
+ 作用:
    - 服务器端开发;web开发
    - 命令行工具的开发;CLI   command line interface;类似于git命令行中的git
    - PC端的应用开发   Electron;有公开课可以学习
+ 学习目标:
    - 了解服务端应用程序工作原理
    - 使用node.js实现动态网页开发
    - 使用node.js为网站提供数据接口 ; JSON-SERVER

# node.js官方介绍
+ Node.js is a JavaScript runtime built on Chrome's+ V8 JavaScript engine.
    - 是一个基于 Chrome的V8引擎的JavaScript运行环境(runtime);
+ Node.js uses an event-dirven,non-blocking I/O+ model that makes it lightweight ad efficient.
    - event-dirven 事件驱动;各种回调函数
    - non-blocking I/O model 非阻塞I/O模型(异步);文件读写操作
    - lightweight ad efficient 轻量和高效(并发处理比较厉害)
+ Node.js'package ecosystem,npm,is the largest+ ecosystem od open source libraries in the world;
    - npm是世界上最大的开源库生态系统;
    - 绝大多数的js相关的包,都存放在了npm上,为了让开发人员更方便的去下载使用;
    - npm install jquery;一条执行命令,引入jQ的包;


# node.js安装
+ 版本
    - LTS:长期支持版本(稳定版);适合在生产环境中使用
    - Current:最新版(测试版);适合学习和研究环境中使用
+ 如何查看node.js是否已经安装完成
    - 打开命令行工具
        + window的cmd是windows命令
        + git bashhere 是Linux命令
    - 输入 node -v 
        + 安装成功: 正常输出版本号;
        + 未安装: 不是内部或者外部命令;

# node.js的使用
## 使用REPL
命令行使用:输入命令后,需要+回车执行命令
+ 通过:REPL可以执行任何js代码
    - Read:读取用户输入的代码
    - Eval:执行用户输入的代码
    - Print:打印用户代码的执行结果
    - Loop:循环;循环REPL
+ 步骤
    - 打开CMD
    - 输入node ;//和浏览器的检查一样;
    - 退出  .exit;或者两次ctrl+c;即可退出
## 使用node执行编写好的js文件
+ 步骤
    - 打开命令行工具,如cmd或者git等
    - 输入`node '文件路径'`
    - 在visual code中,找到文件,右键,点击在命令提示符中打开,默认在当前文件中的目录中打开命令行控制工具;
+ 注意:
    - js文件名称不要使用node.js;会直接打开这个node文件
    - js文件名称不要出现特殊字符以及空格;空格在命令行内会被当做另一个命令,需要增加\转义后使用;
    - js文件名尽量不要使用中文
    - js文件名尽量全部使用小写;Linux系统下大小写敏感,window大小写不敏感;为了兼容多个系统,尽量使用小写;
    - node.js中支持js语法,没有DOM和BOM;

# node.js中常用的api
## 打印
+ process.stdout 标准输出;
+ process.stdout.write(打印内容);//打印内容,不会自动换行
+ process.stdout.write('\n');//打印换行;\n是回车的意思;
## 读写文件
### 写文件(异步的)
```js
//在使用之前需要引入fs模块;
//require('fs');返回值是一个对象,可以调用对应的方法;
var fs = require('fs');
//fs.writeFile(file,data,encoding,callback)
//file:文件路径;写文件的时候,如果写的是相对路径,则参照是当前执行命令的目录,不是node.js文件所在的目录;
使用场景:
如果想要将文件创建在执行命令的文件夹下,则直接写相对路径即可;
如果想要将文件创建在和执行的js文件同一个文件夹下,则使用__dirname来拼接路径即可;
data:写入文件的内容
encoding:文件的字符编码格式;//默认是utf8;
callback:写入完成之后的回调函数;
回调函数的参数: err 这个形参;
写入成功,err是null;写入失败,err是对象;
//如果文件存在,则会进行覆盖;如果找不到目录,则会报错 ENOENT(找不到这个实体) no such file or firectory;
```


### 写文件(同步,了解)
        fs.writeFileSync(file,data,encoding)
### 读写文件(异步的)
     fs.readFile(path,encoding,callback) 
        path:要读取的文件路径
        encoding:文件的字符编码格式,默认是null;如果不传,读取到的内容是buffer对象,就是数据的16进制表示形式;
        callback:读取完成之后的回调函数 
             回调函数的参数:err:读取成功err是null;读取失败,err是对象;????
                          data:读取成功 是对象;失败是undefind;  
### 写文件(同步,了解)
        fs.readFileSync(file,encoding);//返回值就是读取到的内容
          
## global对象(全局变量);可以在官网查看;
    在global对象中的所有内容,都可以不引用而直接使用,如果global中没有,就需要引入后使用;
    在node.js中打印对象,如果对象的嵌套层级比较少,就直接看;如果嵌套层级很多的建议看官方api;
## path模块(路径模块)
    通过字符串拼接的方式,很麻烦,所以引入path模块
            1)使用步骤
                var path = require('path');
                path.join('路径1','路径2','路径3'....);//返回值就是拼接好的目录,会自动处理/\的问题;
            __dirname:当前正在执行的js文件所在的文件夹路径//是一个全局变量,可以直接使用
__filename:当前正在执行的js文件的路径//是一个全局变量,可以直接使用

## http模块
1)使用步骤
  (1)引入模块
      var http = require('http');
  (2)创建一个http服务实例
      var server = http.creatServer();
  (3)使用server实例监听指定的端口
      server.listen(端口号,回调函数);//放在监听request事件之前和之后对执行结果都没有什么影响;放在前面看着清晰一些;
  (4)给server对象注册一个事件request;request事件的触发时机,当服务器接收到浏览器的请求后就会触发这个事件;所有的请求都会进到这个事件中;
    server.on('request',function(request,response){
      request;请求相关的所有内容,都在request中;
          request.url;返回值是浏览器端请求服务端的url地址详细信息;
                      包括路径和参数;/路径?name=pp&age=18;
                      路由(Route):根据不同url路径返回不同的内容;
                      路由规则:根据不同url路径返回不同的内容这段代码;
      response;响应相关的所有内容都在response中;
            在接收到浏览器的请求之后,必须对浏览器作出响应,否则浏览器就会一直处于挂起状态(peeding);
            response.write('响应内容');//通过response对象提供的方法,就可以给浏览器响应数据了;可以调用多次;
            response.end();//结束响应,在响应数据完毕之后,得通知浏览器,响应结束了;会拼接前面所有的write内容;
            简写:
            response.end(参数);一定放在最后;
                参数:字符串;
                    buffer对象,就是16进制的数据形式;所以readFire返回的data可以直接传递给end;
            设置响应头的两种方法:
                  response.setHeader(键,值);//设置响应头;一次只能设置一个;响应头里也不能支持中文
                  response.writeHead();这个方法可以用来设置响应头,并且一次可以设置多条,还能设置状态码;
                          response.writeHead(状态码,'ok',{
                            'content-type':'text/html;charset=uts-8',//浏览器端大小写都识别的
                            'name':'pp',
                          })
                注意:响应头必须在write方法之前设置,否则会出错;
            response.statusCode = 状态码;响应头必须在write方法之前设置,否则会出错;接收number属性;
            response.statusMessage = '提示信息';响应头必须在write方法之前设置,否则会出错;不能是中文;
    })


# 引申:
1,DNS域名解析服务,如果域名找不到是访问不了,提示IP找不到;页面找不到是404;
  浏览器在请求DNS之前会先去本地的hosts文件中查找域名对应的ip地址;
  本地的hosts文件在C:/windows/System32/dirvers/etc/hosts
2,服务器端的外围运行程序
   Apache;TIS;Nginx;TomCat;
   在服务端会给Apache设置一个根目录;可以供客户端访问的文件;
   Apache在服务器端一直监听80端口,当浏览器端有请求到服务端的时候,由Apache解析处理;
   解析完成后,去网站根目录中找到对应的文件,通过php模块,执行php文件内的代码;返回给浏览器;
   //php文件找php模块,其他java等就找对应的模块执行;如果涉及到数据库操作,则再进行数据库操作;最后将执行之后的结果返回给浏览器;
   读取文件的操作是Apache在做;
3,url组成
  协议名称://域名:端口号/路径?参数
4,浏览器的工作原理
  浏览器组成:
      1)用户交互部分(UI) user interface
      2)网络请求部分(Socket);Socket底层的通信方式;WebSocket浏览器端的Socket;
      3)渲染引擎,浏览器内核(Render Engine)
      从服务器端请求回来的内容,就是html代码,渲染引擎将html代码进行处理之后,
      在浏览器中展示出来课件的图形化的网页;
        工作原理:(不同浏览器的顺序不一样,但是步骤都一样)
          (1)解析HTML代码,构建DOM树
          (2)根据DOM树,构建渲染树
          (3)解析CSS样式
          (4)对渲染树进行Layout操作(整合)
          (5)绘制整个页面 Paint
      多核浏览器指浏览器拥有多个渲染引擎,多个渲染引擎并不能同时工作提高效率,多核的目的只是为了处理兼容性问题;
      4)JavaScript引擎(谷歌V8)
      5)数据存储部分(Storage)
5,静态网页和动态网页
    静态网页:服务器在接收到浏览器的请求之后,直接将请求的文件返回给浏览器,不执行任何操作代码;
    动态网页:就是在服务器端,会执行相应代码,将执行之后的结果,返回给浏览器;
6,环境变量
    当装完node.js之后;不是内部或者外部命令;
    我的电脑,右键,属性,高级系统设置,环境变量,在系统变量内找到path,点击新建;将安装好node.js的路径增加上去;//这里面的%是变量;
    可以在任意路径下打开命令行工具,都可以打开到node.exe这个文件;
    本质就是使用命令行工具打开node.exe这个文件,运行node.js这个环境;
    作用:将文件所在的目录路径添加到环境变量中之后,在当前系统中的任意位置,都可以访问到这个目录中的文件了;
7,案例,打印三角形;
  双重for循环;
8,console.log();打印会自动换行;
9,浏览器中的js有dom和bom;服务端的js有特定的方法,不能互相混用;
10,对象.toString('参数');参数传编码格式,不传默认是utf-8;
11,\和/;window下是\,如果是\就用两个\\转义一下;如果是/用一个就可以了;
12,js中异常处理语句
    异常:一旦出现异常,则代码执行中断
    异常处理语句:将异常捕获,避免代码执行被中断;
    语法: 日常开发中使用较少;一般用在框架和类库中;
          try{
            //可能出错的代码,都放在try语句块里
          }catch(e){
            //catch中放的就是出错之后要执行的代码;形参e;
            e就是出错时报错信息;
          }
    完整形态://一般finally会省略
          try{
            //疑问代码
          }catch(e){
            //出错后执行的代码
          }finally{
            //不管怎样都执行
          }
    注意:文件操作函数中的异常无法直接被try catch捕获;如果要捕获,需要将try catch语句放在回调函数内使用;
13,函数中throw
    throw '内容';//将错误信息抛出;内容中写什么就抛出什么;谁调用就抛给谁
    throw new Error('内容');
14,content-type;
浏览器在接收到服务器响应的数据之后,会根据content-type来进行对应的处理;
content-type;//如果不设置,谷歌浏览器会自动猜你返回的是什么,然后解析出来;其他的会默认解析成普通字符串;一定要设置;
    content-type的值:最全的在网上查询;
      text/html 
      text/css 
      application/json
15,views(视图)
16,Lorem(一大段文字)一个模板,用来测试自己的网页的效果;
17,app.js;约定俗成的名字,用来放置js代码;
18,需要容器的语言: php;容器就是php需要的Apache;node.js不需要容器
19,md的操作:
      引入图片: ![图片的tittle](图片地址)
      引入链接:[链接名称](网址)
      一级标题: #
      二级标题: ##
      三级标题: ###
      代码段:    ```js
                代码内容
                ```
                ```shell
                代码内容
                ```
      高亮显示: `高亮内容`    



