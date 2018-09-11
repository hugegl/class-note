一,node.js 初识
    学习node.js的目的就是帮助大家打开服务器端这个黑盒子;
    可以打开黑盒子的服务端技术有:java;php;python;ruby;net 语言c#;.....;node.js
    node.js的语言基础是javascript;//凡是能用js实现的,都用js实现;
    1,node.js是什么
        node.js不是一门语言,不是库,不是框架,是js运行时环境;node.js可以解析和执行js代码;
        以前只有浏览器可以解析执行js代码;仙子js可以完全脱离浏览器执行,一切都归功于node.js
        官网定义及解释:   官网地址:   https://nodejs.org    版本解释:  LTS 长期支持版;Current 体验版 
                Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine.
                构建于Chrome的V8引擎之上;
                  代码只是特定格式的字符串;引擎可以认识它,解析和执行;
                  google的V8引擎目前是公认的解析执行js代码最快的;
                  node.js的作者把google chrome中的v8引擎移植出来,开发了一个独立的js运行时环境;
                Node.js uses an event-dirven,non-blocking I/O model that makes it lightweight ad efficient.
                    event-dirven 事件驱动;
                    non-blocking I/O model 非阻塞I/O模型(异步)
                    lightweight ad efficient 轻量和高效
                Node.js'package ecosystem,npm,is the largest ecosystem od open source libraries in the world;
                    npm是世界上最大的开源库生态系统;
                    绝大多数的js相关的包,都存放在了npm上,为了让开发人员更方便的去下载使用;
                    npm install jquery;一条执行命令;
    2,浏览器中的javascript;//以前学的浏览器js的组成
        EcmaScript:基本语法;//一开始学的
        BOM;
        DOM;
    3,node.js中的javascript
        没有BOM和DOM;//服务器端不操作bom和dom
        EcmaScript;
        在node这个js执行环境中为js提供了一些服务器级别的操作api
            例如文件读写;网络服务的构建;网络通信;http服务器等的处理;
    4,主要作用
        web服务器后台:游戏服务器;接口服务器...
        命令行工具:git (c语言);Linux;window cmd的窗口;npm;hexo(node);.....
        node的命令行工具(主要使用第三方的):webpack;gulp;npm;
    5,预备知识
      html 
      css
      JavaScript
      简单的命令行操作:cd;dir 列出目录;ls 列出目录; mkdir;rm;
    6,学习资源
      书:深入浅出node.js  朴灵著;偏理论,无实践内容;
      书:node.js权威指南   api讲解,无实践内容;
      网址: JavaScript标准参考教程(alpha):http://javascript.ruanyifeng.com/
      node入门:http://www.nodebeginner.org/index-zh-cn.html
      官方api文档:http://nodejs.org/dist/latest-v6.x/docs/api
      中文文档(版本比较旧,凑合看):http://www.nodeclass.com/api/node.html
      CNODE社区:http://condejs.org
      CNODE-新手入门:http://cnodejs.org/getstart
    7,学习目的
      B/S编程模型   browser-sever  back-end  任何服务端技术这种BS编程模型都是一样,和语言无关;
                  Node只是作为我们学习BS编程模型的一个工具
      模块化编程    requireJS;   SealJS;  @import('文件路径')
                    以前认知的JavaScript只能通过script标签来加载;
                    在Node中可以像@import()一样来引用加载JavaScript脚本文件
      Node常用Api
      异步编程       回调函数;Promise;async;generator;
      Express Web 开发框架
      EcmaScript 6
      .....
二,简单的用node执行js文件
        1,打开命令行操作工具,找到要执行的js文件目录;
        //命令行操作工具用git,node,window+r打开cmd都可以;
        //也可以用插件sublime中装一个插件  terminal;
        //在sublime中找到要执行的js文件,右键,点击 open terminal here;会 直接打开命令行,定位到当前目录;
            cd 路径;
            dir 列出;
            cls 清屏;
            上箭头,调出执行记录,执行上一次执行的命令;
          在当前文件路径处,按住shift键,右键,点击在此处打开powershell窗口;
        2,执行js文件 
          命令行工具内敲:    路径>node 文件名.js   //回车即可,注意node的空格
        注意: 1)文件名,不要使用node.js命名;最好不要使用中文;
              2)没有dom和bom;和浏览器中的JavaScript不一样;
三,常用api初识
      浏览器中的JavaScript是没有文件操作的能力;不认识node的文件;
      nodezhong de javascript具有文件操作的能力;
      1,fs是flie-system的简写,就是文件系统的意思
            在node中如果想要进行文件操作,就必须引入fs这个核心模块
            在fs这个核心模块中,就提供了所有的文件操作相关的API
            例如fs.readFile就是用来读取文件的
      2,引入核心模块;使用require方法加载fs核心模块
          var fs = require('fs');//var 变量名 = require('fs');//必须是fs
      3,读取文件
            语法:   fs.readFile('参数1',参数2,)
            参数解释:
                参数1:要读取的文件路径
                参数2:回调函数;此回调函数接收两个参数//形参,名字随意
                      error      如果读取失败,error就是错误对象;如果读取成功,error就是null
                      data       如果读取失败,data就是undefind没有数据;如果读取成功,data就是读取到的数据;
                          eg: fs.readFile('文件路径',function(error,data){
                                //<buffer 68 65 6c 6f 20 6e 0a>
                                //文件中存储的起始都是二进制数据 0 1
                                //看到的是二进制转换成16进制了;2进制和16进制只能计算机认识,人类不认识;
                                //所以可以通过toString方法,转换成人类识别的字符
                            console.log(data);//直接打印出来是16进制的数据;
                            console.log(data.toString();)
                                //一般用error加if判断成功与否
                            if(error){//如果失败error就是对象,转成boolen值就是true,会进入判断;
                              console.log('读取失败了';)
                            }
                          })  
      4,写文件 
          语法:fs.writeFile('参数1','参数2',参数3)
          参数解释:
            参数1: 要写入的文件路径
            参数2:要写入的内容  
            参数3:回调函数;此回调函数接收1个参数  
                  error  写入成功,error是null;写入失败,error就是错误对象
      5,http 
            使用node构建web服务器;
            在node中提供了一个核心模块:http;
            http这个模块的职责就是帮你创建编写服务器的
            1)加载http核心模块
            var 变量名 = require('http');//http必须是http
                eg:  var http = require('http');//变量名叫http有语义性;
            2)使用http.creatServer()方法创建一个Web服务器;返回的是一个Server实例
                引入模块之后返回的值调用creatServer()方法;
                eg: var server = http.creatServer();
            3)服务器
                通过创建web服务器方法后,返回的实例调用对应方法;
                  提供对数据的服务:发送请求;接收请求;处理请求;发送响应(给个反馈)
                //注册监听request事件;所有事件都会触发这个事件
                  server.on('Request',function(参数1,参数2){
                    //当客户端请求过来,就会自动触发服务器的request请求事件,然后执行第二个参数:处理函数
                    //执行的回调函数内代码
                    参数1:request请求对象,可以用来获取客户端的请求信息;
                          例如请求路径:
                                request.url  ;是端口号后面的东西
                                //http:127.0.0.1:3000/  路径是/;默认是/;浏览器的默认行为会加载网页的favicon.ico(不用管);
                                //http:127.0.0.1:3000/a  路径是/a
                              请求的客户端的端口号:
                                request.socket.remotePort;
                              请求的客户端的二地址:
                                request.socket.remoteAddress;//ip地址和端口号
                    参数2:response响应对象,给客户端发送响应消息;//服务器会和发送请求的客户端地址和端口号自动建立连接,返回数据;
                          有一个方法:write可以用来给客户端发送响应数据
                          write可以使用多次,但是最后一定要使用end来结束响应,否则客户端会一直等待;
                          语法:   response.write('发送的内容')  
                                  response.end()   //告诉客户端,我的话说完了,你可以响应给用户了;
                              eg:     response.write('你好啊')
                                      response.write('很好很好')    
                                      response.end()
                          用write()和end比较麻烦,可以使用end('发送的内容')简写;结束的同时发送响应数据;
                          注意:1)响应内容只能是二进制数据或者字符串,数字,对象,数组,boolen等等都不可以;
                               2)浏览器默认发送的数据,其实是utf-8编码的内容;
                                 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统默认的编码去解析;
                                 中文的操作系统默认是gbk;
                                 解决方法,设置响应头内的内容样式中的编码方式charset为utf-8;
                                 response.setHeader('Content-Type','text/plain;charset=utf-8');
                                在http协议中,Content-Type就是用来告知对方我给你发送的数据内容是什么类型;
                                Content-Type的查询网址:http://tool.oschina.net/;点击HTTP Mine-type;然后搜索不同资源对应的content-type;
                                text/plain;//普通文本;不会解析html标签
                                text/html;//html格式的文本;浏览器能解析html标签;如果你发送是html格式的字符串;
                                        则也要告诉浏览器,我给你发送的是text/html格式的内容
                                image/jpeg;//.jpg文件;图片不需要指定编码charset;编码只针对字符;图片不需要;
                                3)一个请求对应一个响应,如果在一个请求的过程中,已经结束响应了,则不能重复发送响应;
                                    没有请求就没有响应;
                            })  
            4)绑定端口号,启动服务器
                server.listen(端口号,回调函数);
                端口号:3000/5000/8000都可以;
                      如果用80端口;可能容易被其他程序占用;//默认浏览器会使用80端口号
                      如果当前端口号被占用了,就无法启动;
                回调函数:启动服务器需要时间,启动后会执行启动完成的回调函数;
                    eg:   server.listen(3000,funciton(){
                        执行代码;打印日志信息;
                    });
                //启动之后不能在命令行工具内输入普通的命令行代码;
                //已经变成了服务器,在等待浏览器端发出请求,然后响应请求;
            5)在命令行内关闭服务器
                ctrl+c;关闭服务器,回到普通命令行代码;
            注意:服务器代码在修改后一定要重启服务器才能生效
四,其他
1,node中的js
  1)EcmaScript;没有dom和bom;
  2)核心模块
      node为JavaScript提供了很多服务器级别的api,这些api绝大多数都被包装到了一个具名的核心模块中;
      例如:文件操作的fs核心模块;http服务构建的http模块;path路径操作模块;os操作系统信息模块...
      使用核心模块方法:
            //引入核心模块
                eg:
                  var fs = require('fs');               
                  var http = require('http'); 
                  var os = require('os'); 
                  var path = require('path');
            //使用方法;//方法不常用的可在官网中找,很详细; 
                eg:
                  os.cpus();//获取当前机器的cpu信息;
                  os.totalmen();//获取当前机器的内存大小;返回值是字节;
                  path.extname('路径名');extension name扩展名;输出这个路径的扩展名;
  3)用户自定义模块
                  在node中,模块有三种:
                    (1)具名的核心模块,例如fs,http
                    (2)用户自己编写的文件模块,相对路径必须加./;否则报错,会被当成核心模块;
                          eg:  require('路径/XX.js');  //表示加载并执行路径内的文件;可以省略后缀名.js(推荐)
  4)第三方模块
  5)模块作用域
    在node中,没有全局作用域,只有模块作用域,即文件作用域;
    外部访问不到内部,内部访问不到外部;
方法:
1,require();
  作用:1)加载文件模块并执行模块内的代码;
      2)拿到被加载文件模块导出的接口对象;//加载文件后,返回值就是这个对象;
                    //每个文件模块中都提供了一个对象: exports;//import导入,export导出
                    默认exports是一个空对象;可以把需要被外部访问的成员,挂载到对象中;

引申:
1,端口号和ip地址
  ip地址用来定位计算机,端口号用来定位具体的应用程序;
  所有需要联网通信的软件都必须具有端口号;
  端口号范围是0-65536之间;
  在计算机中有一些默认端口号,开发的过程中最好不要去使用;如http服务的80;使用一些简单好记的都可以,如3000,5000,等,没有什么含义;
  可以开启多个服务,但是端口号要不一样才可以;一台计算机中的一个端口号只能被一个程序占用;
2,url
 统一资源定位符;一个url最终其实是要对应一个资源的;
3,http-fs示例
 1) 结合fs发送数据;
 2)content-type:不同的资源对应不同的content-type是不一样的;
    图片不需要指定编码,一般值为字符数据才指定编码;
4,总结
  在node中没有全局作用域的概念;
  在node中,只能通过require方法来加载执行多个JavaScript脚本文件;
  require加载只能是执行其中的代码,文件与文件之间由于是模块作用域,所以不会有污染的问题;
  模块完全是封闭的,外部无法访问内部,内部也无法访问外部;
  模块作用域优点:可以加载执行多个文件,可以完全避免变量名冲突污染的问题;
           缺点:模块与模块之间进行通信,可以用exports;每个模块都提供了这个空对象,如果想被外部访问,可将需要访问的内容挂载到这个对象上;
           通过require这个模块,返回值就是这个对象,可访问到挂载到这个对象上的所有内容
  核心模块,由node提供的具名模块,有自己的特殊标书,如:fs,http,os,path,
        所有核心模块在使用的时候,需要先require加载后使用返回的对象,调用需要使用的方法;
  content-type:服务器吧每次响应的数据类型正确的告诉客户端;具体参考网站;
         对于文本类型的数据,需加上编码,防止中文乱码;
  通过网络发送文件,发送的不是文件,本质上发送的是文件内容;浏览器收到响应后,就会根据content-type进行对应的解析处理;










