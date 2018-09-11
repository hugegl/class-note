同步:一次只执行一件事,一件一件的做;
异步:同时执行多件事,前一件事情不会影响后面事情的执行;
一,AJAX
1,定义:不是一个新的语言,是js里面的技术;
Asynchronous Javascript And XML:对现有语言的整合;
Asynchronous [e'sɪŋkrənəs]:异步的
Javascript:js 
And:和 
XML:有格式的字符串
2,AJAX可以发送一个基于http协议的异步请求
  常见应用:实现无刷新更新页面,
  eg:注册时提示用户名是否存在;
      百度搜索,立即显示搜索热词;
      微博评论,立即显示评论,不会整个页面刷新
二,XML HttpRequest对象(以下简写xhr)
使用ajax进行发送请求,借助一个XMLHttpRequest对象(浏览器内建对象),可以发送ajax请求;
1,创建xhr对象
    var 变量名 = new XMLHttpRequest();
2,发送请求,基于http协议,请求包含:请求行,请求头,请求体;
        1)请求行(请求方式,请求地址)
         变量名.open('type','url',是否异步默认true);
         type: get / post;
         url:路径;
         是否异步:true异步/false同步;默认true;
        2)请求头
          (1)get请求:不需要设置请求头,按浏览器默认的就行了,
              因为get 请求没有请求体,不需要再请求头中设置请求体的编码方式;
              传参: 拼接在地址栏内,即url中;拼接格式为: 地址?值=名&值=名;
              eg:  fo.php?name=pp&password=123;
          (2)post请求:需要设置请求头,
                因为 post有请求体,需要设置请求体的编码方式
                变量名.setRequestHeader( "content-type", "application/x-www-form-urlencoded" );
        3)请求体
        变量名.send(请求体);
          (1)get: 请求没有请求体 ;
              所以get的请求体设置:
              变量名.send(null);
          (2)post:要求格式:键1=值2&键1=值2;
          变量名.send('键1=值2&键1=值2');
      eg:   get 
      var xhr = new XMLHttpRequest();
      xhr.open('get','02-get.php',true);
      xhr.send(null);
      eg:   post 
      var xhr = new XMLHttpRequest();



3,readyState 标记xhr的状态
    变量名.redayState = 0 时,UNSET open尚未调用;
    变量名.redayState = 1 时,OPENED open已调用;
    变量名.redayState = 2 时,HEADERS_RECEIVED 接收到头信息;
    变量名.redayState = 3 时,LOADING 接收到响应体;
    变量名.redayState = 4 时,DONE 响应完成;
4,监听readState的变化
    readystatechange可以监听readState的变化;
    js中需要写:onreadystatechange =函数体;
    //预习视频知识点
    //HTML5中提供的onload方法,可以监听readState===4的时候,页面加载完成后执行的函数;
    结构:变量名.onload = 函数体;
5, 获取响应文本
    变量名.responseText; 获取响应文本/响应体
6,设置文本
    re = 变量名.responseText;
    将获取到的内容设置在页面中
7,查看状态码
  status;
  书写结构: 变量名.status 返回值就是响应状态码200响应成功/404/500/306等等
8,获取响应头
  变量名.getResponseHeader('key');获取单个响应头信息
  变量名.getAllResponseHeaders();获取所有的响应头信息







  案例知识点:
  1,in_array('内容',数组);
      判断内容在数组中是否存在;如果存在返回true,如果不存在返回false;
  2,location.herf = '路径';
    BOM的方法,location对象中herf属性可以跳转页面
  3,array_rand(数组,多少个);
  在数组中随机获取多少个随机的下标;
  如果写1,那么返回一个随机索引;
  如果写1以上,会返回一个数组,里面是随机索引;
  4,sleep(数字);停止几秒;
  5,scrollIntoView();让dom元素滚动到可是区域内
    结构:元素.scrollIntoView();




预习知识点:
1)http中约定报文的内容就是字符串/文件,而我们需要传递给客户端的是一个有结构的数据;
    这种时候,我们一般采用json作为数据格式;


