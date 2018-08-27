一,复习
1)addEventListener,ie8的兼容写法,封装函数事项
结构:   function add(ele,eve,fn,tf){
  //判断当前浏览器是否可以使用addEventListener
        if (ele.addEventListener){
          //如果能进来,表示支持
      ele.addEventListener(eve,fn,tf);
        }else{
          //证明不支持addEventListener
      attachEvent('on'+eve,fn);
        }
}
2)事件委托案例增加知识点:
本来是事件委托给父级元素,但是不小心点到父级元素会执行全部内容
在事件处理函数中判断事件目标是谁?如果事件目标是ul则不执行下面的代码
结构:    ul.onclick = function (e) { //e随便传一个形参进来,接收事件处理函数执行时候的对象,用以获取事件处理函数时执行的对象的对象
  e = e ||window.event;   //如果不写形参e,可以写event,因为chrome浏览器比较强大,一方面把事件对象传递到了事件处理函数中,另一方面他也把事件对象赋值给了window.event 

  if(e.target == ul){
    return;  //如果点的是ul就return了,函数不继续执行;
  }else{
    console.log(e.target.innerText);
  }
}

3)方法,属性
方法: 函数的小名
函数: function
属性:针对的是对象,对象身上的属性,对象中严格来讲其实都是属性,只不过当我们给属性赋值为函数的时候,又把这个属性称为方法

4)注册事件的其他方式:
  addEventListener('事件名',事件处理函数,boolean值)
  (1)可以给同一个元素多次注册同一个事件
  (2)还可以控制事件触发的阶段
5)移除事件:
  (1) on事件名 = null;
  (2) removeEventListener
6)事件对象
   (1)事件类型type
   (2)事件目标target
   (3)鼠标在浏览器可视区的坐标clientX/clientY
   (4)鼠标在页面的坐标pageX/pageY
   (5)键盘按键对应的数字 keyCode
   (6) 阻止事件传播 stopPropagation()
   (7)阻止默认行为 preventDefault()
7)事件流:
  捕获阶段
  目标阶段
  冒泡阶段
8)新增事件
  keydown  按下时  不区分大小写
  keyup    抬起时
  keypress 按下时  区分大小写
----------------------今日内容----------------------
一,BOM
    定义: browser Object Model 浏览器对象模型
    俗语:把浏览器抽象成对象,通过操作对象来实现操作浏览器的目的,在js中,把浏览器抽象成了window对象
    只要是window身上的属性或者方法都可以直接使用,window.可以忽略
    如: window.alert()  alert()
        window.document    document
二,页面加载的两个事件
   1, window.onload   页面中所有内容都加载完毕了才触发(页面上的所有内容,包括外链,包括路径等等,是指dom树以及所有的外部文件)
      eg : 
      window.onload = function(){
        //执行代码,等页面都加载完了,才会执行代码
      }
   2, window.onunload   页面关闭的时候触发,以前用来清理用户关闭时清除缓存的
三,  location对象
定义:浏览器的地址栏中的地址(url)
window.location,也是window对象身上的
  
    1,  url
      定义:Uniform Resoure Locator,统一资源定位符(网络中的地址)
      组成: 
  协议://主机名(域名):端口号/路径?查询字符串#锚点
      scheme  协议名        http://                           规定浏览器和后台交互怎么沟通,怎么接头的
      host    主机名/域名   www.xxxx.com 包裹了的ip地址,好记    通过主机名找具体的服务器
      port    端口号        80                                具体找的哪一个应用程序
      path    绝对路径      路径                              具体找到那个文件
      query   查询字符串     ?后面是要查询具体的信息用 & 隔开     用来发给后台做判断的
      fragment 锚点         #后面的内容                       发给后台做判断的
    2, location对象
       2,1  属性
        属性名:          属性值:
        href           地址栏中相对完整的url的字符串(记忆)
        search         url查询字符串的部分,即?后面的东西(记忆)
        host       域名/主机名+端口号
        hostname       主机名
        hash           锚点内容,即#后面的内容
        pathname       路径
        port           端口号
      2,2  方法
       location.assgin('url字符串')     用于页面跳转  有浏览记录历史,可以后退
       location.replace('url字符串')    用于页面跳转   不记录历史,不能后退
       location.reload()               刷新页面,参数不传,默认false,刷新页面;传true强制刷新页面,不会加载缓存的数据,一定从服务器拿数据
    引申:  如果给href属性赋值,也可以达到页面跳转的效果,跟assign类似
四,  history对象
        优点:减少向服务器发送请求的现象,优化性能
        方法:
        1) back()       返回上一个页面
        2) forward()    前进至下一个页面
        3) go()         参数是正数,则前进正数的步数;参数是负数,则后退至负数的步数
五,  navigator对象
1,属性  userAgent
作用:识别客户端设备和设备当中浏览器的字符串
返回值  字符串,客户电脑的操作系统,版本,客户浏览器的设备,型号等
   引申:苹果手机和安卓手机的内置浏览器内核都是 webkit 
六,定时器
  设置定时器
    1,setInterval(回调函数,间隔时间/毫秒)     每隔一段时间就调用一次
    2,setTimeout(回调函数,间隔时间/毫秒)     时间到了以后只调用一次
    注:回调函数,是时间到了之后调用函数的意思
  先设置定时器,再执行下面的函数,执行完下面的代码之后再看设置的时间,到了之后再回调函数,执行函数体
    解决方法:把回调函数改成有名字的函数传进去,提前调用一遍函数即可.  
    返回值:该定时器的id
  清除定时器
    1,clearInterval(id)
    2,clearTimeout(id)
    注:1)清除定时器和设置定时器要一一对应,传的参数是那个定时器的返回值,即id值,设置定时器的时候,就会返回这个定时器的id,我们只需要申明一个变量接收一下就可以了
       2)定时器的id一定是一个非零的数字
       3)如果用反了也可以,因为是浏览器的容错率造成的,但是不一一对应的话不严谨,最好一一对应
案例引申:
盒子移动至400案例,执行按钮点击事件函数体内:
    1)为了避免添加多个定时器的问题,所以每一次设置新的定时器之前要把原来的清除掉
    2)判断一下是否有定时器,有的话再清除定时器,如果有定时器那么转boolean值为true,如果没有这个id那么boolean值为false
    3)把var 定时器id   申明在点击事件函数外面,只申明一次;如果在事件函数体内,那么每次执行都有一个新的id,存不住以前的值,那么在之前清理就清理不掉
时间案例
    1)transform : rotate (360deg) ;  旋转360度
    2)  .getHousrs()  获取小时(24小时制); .getMinutes() 获取分钟 ;.getSeconds() 获取秒钟
    3)分针转动的角度/分钟一个小时转动的角度 == 时针应该偏移的角度/时针一个小时走的角度
    4)得到对应的值后,需要加上当前秒针/分针的偏移量,再加给分针/时针,达到和钟表一样的效果,而不是直接偏移,有缓冲的度数

    
 今日拓展:
    window的属性
    name    值:默认是一个空的字符串
    top     值:指向window本身
    注:
    1)在全局声明一个变量,其实就相当于给window增加了一个属性
    2)如果全局有name变量,不管你赋值的是什么类型,都会转换成字符串
    3)如果全局有top变量,不管你赋值是什么,top永远指向window
    结论:在全局不要使用name和top 
之前遗留拓展:  标签上的自定义属性
自定义属性:
设置结构:
 data-属性名='属性值'  //直接在行内设置
js中结构:
获取:
 元素.dataset.属性名
元素.dataset 可以打出这个元素下的所有用   data-   设置的属性
设置:
元素.dataset.属性名 = '属性值'


