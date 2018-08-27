--------------------------今日内容---------------------------------
一,学生管理系统
知识点:
1)在a链接里面动态拼接下标/id,获取当前执行操作的对应那条数据返回给后台;
2)php是弱类型语言,从数据库中取出来所有字段值都是字符串格式的;
3)error 错误码4,未上传图片
4)隐藏域:type="hidden" 一般用于向后台传递一些不希望用户修改的值,这个input不会显示在桌面上
二,cookie
1,cookie和session概念
      会话:浏览器和服务器之间的交流(请求和响应);
      http协议是无状态的,多次请求之间没有关联性;
      利用cookie和session可以进行会话保持;
      会话保持:保持了用户的登录状态,即服务器端记录了用户信息,下一次访问服务器就认识该用户了;
      cookie: 浏览器端存储数据的容器;
      session: 服务器端存储数据的容器,每个用户都有自己存储的session空间;
2,操作cookie 
控制台,application,storage是浏览器的存储空间,里面有cookie,里面有刷新和清空的图标
1)原生js操作,获取很麻烦
    (1)设置,要求后面是=号连接的键值对
      document.cookie = '名=值';//一次只能设置一个
    (2)获取,一次性将所有的cookie返回,用封号和空格来分隔每个键值对'; '
      document.cookie;//练习字符串分隔
2)jQuery.cookie.js操作//这是jQuery的插件
    (1)设置,会话级别的可以不加过期天数
        $.cookie('键','值',{expires:过期天数});//设置   expires 过期时间);
        如果不设置过期时间,默认cookie是会话级别的,关闭浏览器,就会被销毁;
    (2)获取 
        $.cookie('键');
    (3)删除 
       $.removeCookie('键');
3)服务器端也可以操作cookie
将操作写在php标签中即可:<?php 内容?>
    (1)设置
        setcookie('键','值');
        setcookie('键','值',时间戳);//时间戳:什么时候到期,以1970开始的秒数;
        eg:  设置7天后过期  time()*7*24*360
    (2)获取 
        $_COOKIE 超全局变量,获取所有的cookie信息;返回值是一个关联数组
    (3)删除
      将时间戳给成过去的时间,就会销毁该cookie;//time()-1;
引申:
      1)当cookie设置时,如果包含有等号,封号,空格时,会被解析成+号,不建议用来存储到cookie中;
      2)$_COOKIE读取的是,浏览器端携带过来的cookie,携带在请求头中;
        setcookie设置的是响应头,将来让浏览器自己取设置cookie
cookie的特点总结:
    1)可以在同一个网站中多个页面共享
    2)不同浏览器的cookie不能共享
    3)cookie数据存储在浏览器中,每次请求的时候,会在请求的时候,在请求头中携带cookie里面的数据,用来会话保持;
    4)服务器端不能直接操作cookie,是通过服务器端设置响应头,在响应头中,set-cookie:name=pp,
        将来浏览器端,接收到请求,查看响应头,并根据set-cookie在浏览器端自动设置cookie;
    5)cookie默认是会话级别,一旦页面关闭,cookie就销毁了
    6)cookie存储大小4k;
三,session
定义:服务器端存储数据的容器,每个用户都有自己存储的session空间;
操作步骤
1,先开启session机制
    session_start();//表示让服务器开启session机制;
2,存储
    $_SESSION['名'] = '值';
3,获取 
    $_SESSION 超全局变量,用来获取当前请求用户的session数据
    返回一个二维数组;
4,删除
    unset($_SESSION['名']);//删除某一个;
    $_SESSION=[];//删除所有session数据
过程详解:
开启了session机制后,
    1)如果当前用户,是第一次访问服务器,会自动生成一个sessionid(是一个随机字符串);
    可以通过session_id()的返回值获取到sessionid;
    2)根据这个生成的sessionid,服务器会为该用户开启一块session存储空间;
      新建一个session文件,这个session文件的文件名就是sessionid,可以用来存储数据,文件存储在临时文件tmp下;
      $_SESSION['名'] = '值';会把'名=值'存储在这个文件中;
    3)将sessionid传递回浏览器端,
    通过设置响应头:set-cookie:PHPSESSION= sexxionid;
    将来将sessionid设置在cookie中;
    4)浏览器端解析响应头,设置sessionid到cookie中;
    5)第二次访问,cookie里面存储的数据,会在请求时携带,把sessionid携带着了;
    6)后面服务器端根据sessionid就可以找到对应的session文件,认识该用户了;
5, session_desdtory();删除/销毁服务器端的session文件
    特点总结:
    1)多个页面可以共享;
案例知识点:
1)判断当前页面的cookie中是否有sessionid
isset($_COOKIE['PHPSESSID'])


