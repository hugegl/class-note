一,复习
url:统一资源定位符
url组成:协议://域名:端口号/路径?查询字符串#锚点
location对象
    属性:href返回url,给href赋值可以页面跳转
         search返回查询字符串
    方法:  assign('url')  跳转页面记录历史
           replace('url') 跳转页面不记录历史
           reload(true/false)   true强制刷新,不传false普通刷新
history对象:
      forwad()向前一步
      back()向后一步
      go(+num/-num) +num向前mun步

navgitor.uesrAgent  返回用户设备和浏览器信息的字符串
定时器
      设置:  setInterval(回调函数,时间)  每隔一段时间执行一次,返回值是定时器的id
             setTimeout(回调函数,时间)   只执行一次,返回值是定时器的id
      清除:clearInterval(定时器id)
          clearTimeout(定时器id)
------------------------------------------今日内容------------------------------------
一,offset系列
只可以用来获取,不可赋值
结构: 元素.offset属性
      1,  offsetParent:返回当前元素最近的定位父元素
         与区别:ParentNode:返回直接父元素;offsetParent:定位父元素;
      2,  offsetWidth:返回当前元素的宽,包括自己的内容(contant),padding,border;包括外链式嵌入式所有的最终渲染在页面上的宽
      3,  offsetHeight: 返回当前元素的高,包括自己的内容(contant),padding,border;
      4,  offsetLeft:返回距离offsetParent的左偏移量
      5,  offsetTop:返回距离offsetParent的上偏移量
     
二,client系列
只可以用来获取,不可赋值
结构:   元素.client属性    
      1,   clientWidth:元素可视区域的宽(没有边框),边框内部的宽度,包含contant和padding
      2,   clientHeight:元素可视区域的高(没有边框),边框内部的高度,包含contant和padding
      3,   clientLeft:返回元素左边框的宽度
      4,   clientTop:返回元素上边框的宽度
三,scroll系列
scrollLeft和Top可以赋值,默认滚动条的位置,直接赋值数字,不需要写单位
scrollWidth和Height不可以赋值
定义:操作滚动条
结构:   元素.scroll属性
      1,   scrollWidth:元素内容的宽
      2,   scrollHeight:元素内容的高
      3,   scrollLeft: 元素中内容左侧滚动出去的距离
      4,   scrollTop:元素中内容顶部滚动出去的距离
四,获取浏览器可视区的大小
只能获取,不可赋值
      1,  window.innerWidth  浏览器可视区的宽
      2,  window.innerHeight  浏览器可视区的高
      ------以上两个ie8有兼容问题------
      解决:document.documentElement.clientWidth
          document.documentElement.clientHeight
五,浏览器中页面滚动出去的距离
只能获取,不能赋值
1,  window.pageXOffset    浏览器中整个页面左侧滚动出去的距离
2,  window.pageYOffset    浏览器中整个页面顶部滚动出去的距离
------以上两个ie8有兼容问题------
解决:document.docuementELement.scrollLeft
      document.docuementELement.scrollTop
监听浏览器的滚动条
结构:   window.onscroll = 事件函数
注意:浏览器的滚动条拉动后,再刷新,滚动条还在拉动过的地方;元素的刷新后回到初始位置




事件:
1)scroll事件
定义:监听滚动条滚动的事件
结构:元素.onscroll = 事件函数
2)mousedown事件
定义:鼠标按下事件
结构: 元素.onmousedown = 事件函数
3)mouseup事件
定义:鼠标松开事件
结构: 元素.onmouseup = 事件函数
4)mouseenter鼠标进入(可阻止冒泡,推荐使用)
5)mouseleave鼠标离开(可阻止冒泡,推荐使用)



案例引申:
鼠标拖拽案例:
  1)按下移动事件,在鼠标按下的事件(mousedown)中注册鼠标移动事件(mousemove);
  在鼠标移动的事件处理函数中给要拖拽的元素设置位置
  2)把鼠标按下(在按下的事件内获取)减去鼠标移动(在移动的事件内获取)的差值赋值给需要移动的盒子,达到鼠标移动多少,盒子移动多少的目的
  3)在鼠标按下时,需要移动的盒子距离定位父元素的坐标(在按下的事件内获取),用初始的位置加上鼠标移动的距离,即盒子需要移动的距离,
  再把距离赋值给需要定位的盒子(在鼠标移动事件里)即可
  4)鼠标移动事件如果注册在移动的盒子上面,鼠标移动过快,鼠标会离开盒子,到空白的页面上
  用户体验差,可以把鼠标移动事件注册在document上面,因为鼠标移动时不会超出document范围
  5)在鼠标抬起事件(mouseup)中移除鼠标移动事件
   给移动的盒子注册mouseup事件,如果鼠标移动过快,鼠标在盒子外部抬起就无法触发此事件,用户体验差,
   需把mouseup事件注册在document身上,万一鼠标跑出盒子,在外部鼠标抬起,也会触发鼠标抬起事件,以此来停止鼠标移动事件
覆盖层拖拽案例:
   1)  offsetLeft和offsetTop获取到的是元素的位置(包括与父元素的距离和自己的margin)
   后面重新给盒子定位赋值的时候,只赋值了(父元素的距离+鼠标移动的位置),但是在最后渲染的一瞬间,css中的margin又作用到盒子身上,
   解决方法:在给元素赋值移动的位置时,把自身css样式中的margin的减去
放大镜案例
  1)小盒子移动的距离/小盒子可以移动的最大距离==大图移动的距离/大图可以移动的最大距离
  2)在ie8中有冒泡影响,导致小盒子闪,所以ie8有两种事件不会冒泡
   (1)mouseenter鼠标进入(可阻止冒泡,推荐使用)
   (2)mouseleave鼠标离开(可阻止冒泡,推荐使用)












