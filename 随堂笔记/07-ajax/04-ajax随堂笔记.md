一,反馈知识点
1)Math.max(num1,num2,num3....)使用结构
所以瀑布流案例找最大值,所以用apply的参数平铺
apply(this指向对象,[参数1,参数2,参数3...]);
eg: 
    var arr = [num1,num2,num3....]
    Math.max.apply(null,arr) 即可求出最大值
二,宽高汇总
1,js中
  body.clientWidth/Height  可视区宽/高
  body.offsetWidth/Height  页面的宽/高  ;
  box.offsetWidth/Height    盒子的宽/高;
  box.offsetLeft/Top        盒子距离最近定位父元素的距离;
  body.scrollTop/Left       页面卷曲出去的距离;
2,jQ中
  $(window).width()/height()              可视区宽/高;
  $(document).width()/height()            页面的宽/高;
  $(window).scrollTop/Left                页面卷曲出去的距离;
  offset()   返回一个对象{left:X,top:X}    当前元素到页面最顶端和最左端的距离
  position()  返回一个对象{left:X,top:X}   距离有定位父元素的距离;
-------------------------------------------------今日内容------------------------------------------
一,同源
    同源 定义:协议,域名,端口完全相同;
    同源策略:同源政策只发生在浏览器中,目前所有浏览器都实行了这个政策;
            最初的含义是:同源网站的的cookie可以共用,可以访问,否则不能访问;
    同源策略目的:保证用户信息的安全
    同源策略的限制范围:
         1)cookie,localStorage,IndexDB无法读取
         2)DOM无法获得
         3)AJAX请求在浏览器端有跨域限制;
         即AJAX发送请求也必须同源,如果在两个不同源的网站中进行AJAX请求,会报错;
二,不受同源策略限制的标签
     1)script 标签 src 
     2)link   标签 href 
     3)img    标签 src
三,跨域
    1,jsonp
    定义:json width padding
    优点:无兼容问题;
    1)第一版
      原理:
      服务器端返回一个定义好的js函数的调用,并且将服务器的数据以该函数参数的形式传递过来,
      这个方法需要前后端配合;
      1)前端 声明一个全局函数
              动态创建一个script标签,将函数名通过callback 传递给后台

      2)后台   根据callback 获取函数名
              返回函数调用 调用参数就是json数据

      开始的初步流程:
          使用script 的src引入不同源的网站
          向不同源的网站发送一个请求,返回一个文件内容,当成js来执行;
      原理总结:
       1,利用了script 标签可以跨域请求的特性,不受同源策略的限制
       2,引入一个php文件,后台返回一个函数调用,将json数据以参数的形式传递
       3,script标签会执行引入的文件文本,就相当于调用了函数,获取到了数据
       4,先声明函数,后调用函数
    2)第二版(优化)
      (1)动态创建script标签,即属性
          需求:点击按钮获取数据
          步骤: 动态创建script标签,指定src路径,追加到页面中去;
      (2)函数名指定死容易出错,不方便前后端交互;
          优化:前端将函数名作为参数传递给后端;
              eg : 前端传参:  url ? callback = 函数名;
                   后台接收:  $_GET['callback'](需要传输给前端的数据/即实参)
    3)AJAX和JSONP没有任何关系
    4)JSONP只能通过get方式请求
    2,jQ中JSONP的使用
    eg:  $.ajax({
          url:'跨域的地址',
          type:'get',
          dataType:'jsonp',//返回数据的格式是jsonp,解析还是按照json的格式来解析
          success:function(e){
            这里接收到的e,就是传递过来的跨域地址中的实参;
          }
        })
总结: 
1,同源: 域名 端口 协议相同
2,跨域:不同源网站请求数据
3,不受同源策略限制的标签 link script img scr
4,利用了script标签的src属性,跨域访问
四,XMLHttpRequest2.0版本
老版本的缺点:
    1)仅支持传输文本数据,无法传输二进制文本,比如图片视频等;
    2)传输数据时,没有进度条信息,只能提示完成与否
    3)受到了'同源策略'的限制
新版本的功能:
    1)可以设置timeout超时时间
        (1)允许设置超时时间;
        书写结构:XML对象.timeout = num;
        单位是毫秒,如果num毫秒内时间没有回来,就认为是超时了
        (2)如果超时触发timeout事件;
        书写结构:XML对象.ontimeout = 函数体;
        如果超时了,会触发这个事件;
    2)可以使用formData对象管理表单数据
            $.ajax中的
          类似于$(选中表单整体).serialize();
      (1)仅支持post请求
      (2)不需要设置请求头,浏览器会自动设置
      (3)通过new Formdata() 创建实例
        参数:form 表单元素
              如果没有传参,表示没有手机form表单数据
              如果传了form元素,将来就会收集表单元素中所有设置了name属性的值,进行提交
      (4)这个formData可以作为send的参数
        eg:  
            var xhr = new XMLHttpRequest();
            xhr.open('post','路径');
            var form = document.getElementById('form');
            var formData = new FormData(form);
            xhr.send(formData);
            后期获取后端传回数据即可
       (5)formData有一个append属性,可以追加属性名,属性值;
       结构: formData实例对象.append(名,值)
      input的file属性,这个对象下面有一个files属性,
      该属性的值是一个伪数组,有长度,有下标,每一项是一个对象,这个对象存储了每一个图片的信息,
      如果input属性是单个的话,第一个下标就是上传的图片的对象;
      如果input属性是多个的话,则这个伪数组中就存储了选中的多个图片对象;将input框内添加multiple属性即可
            书写结构:  
                    formData实例对象.append('属性名',属性值);
        eg:异步文件上传,实时显示图片渲染到页面
        <input type="file" id="fileI">
        var fileI = document.getElementById('file');
        fileI.onchange =function(){
            var file = fileI.files[0];
            var xhr = new XMLHttpRequest();
            //formData必须是post请求
            xhr.open('post','路径');
            //formData不用设置请求头
            var formData = new FormData();
            formData.append('file',file);//参数解释????
            xhr.send()
        }
    3)允许请求不同域名下的数据(跨域)
    4)允许上传二进制文件
    5)可以获取数据传输进度的信息
    书写结构:xml对象.upload.onprogres = 函数体;
    xml对象的成功后返回对象的属性:loaded 已上传的部分
                                total表示整个文件大小
    用于监听文件上传进度的信息
            文件上传显示进度条,将文件上传的信息实时的接收并且渲染到进度条的宽度上;
五,跨域资源共享(CORS)兼容ie10+
cross-origin-resource-sharing;
跨-域-资源-共享;
服务器必须允许跨域;
允许跨域在服务器需要的代码:
*:表示所有域名;如果指定域名,就将*改为指定域名即可;
header('Access-Control-Allow-Origin:*');
只允许http://www.study.com访问网站的数据
header('Access-Control-Allow-Origin:http://www.study.com');
具体流程:  浏览器发送跨域请求给服务器,服务器查找当前域名是否被允许,如果允许就返回数据;否则就忽略;
结论:跨域行为是浏览器的行为,服务器与服务器之间不存在跨域问题;
六,jsonp仅支持get请求,数据量有限,大数据需要用cors;
cors需要服务器允许跨域,浏览器才能跨域访问;
七,实现跨域的两种方式
jsonp:优点没有兼容问题;缺点,只支持get
原理:前端动态创建script标签进行访问后台;
     后台返回函数调用,将参数作为函数的参数进行传递给前端,在前端调用;
cors:优点简单方便,get和post都可以;
缺点:只兼容ie10以上



案例总结:
1,change事件
作用:监听当前select被选择时,内容改变时触发;
2,在控制台输入   $0  表示当前选中的元素;
3,console.dir(对象)  打印对象
4,toFixed(num)  保留num位的小数
5,scrollIntoView()这是js的方法,如果jQ要用,需要转换成js对象后使用;






