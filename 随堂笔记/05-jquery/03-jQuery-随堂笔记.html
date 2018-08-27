-------------------------------复习--------------------------------------
一,操作样式
1,css('name','value')设置单个样式
2,css({
  'name':'value',
  'name':'value',
  ....
})设置多个样式,
设置样式时,获取的元素都设置上相同的样式
3,css('name')获取样式
获取时,只获取第一个样式
二,操作类名
1,addClass('name')增
2,removeClass('name')删
3,hasClass('name')查,只要有一个元素有指定的类名就返回true
4,toggleClass('name')改,切换类名
二,操作属性
1,attr()
    attr('name','value')设置单个属性
    attr({
      'name':'value',
      'name':'value',
      ....
    })设置多个属性
    attr('name')获取属性
    removeAttr('name')移除属性
2,prop()
对于表单元素checked,selected,disabled属性去使用prop
3,:checked
获取被选中的表单元素
三,动画效果
三组基本动画
1,show,hide,toggle   不传参没有动画效果
2,sildeDown,sildeUp,sildeToggle   不传参,有动画效果,取值nomoral  400ms
3,fadeIn,fadeOut,fadeToggle     不传参,有动画效果,取值nomoral  400ms
自定义动画
1,animate({},[speed],[easing],[callback]),{}必写,后面三个参数选填
四,动画队列
定义:给元素增加多个动画,会他添加到元素的动画队列中,依次执行
stop([clearQueue],[jumpToEnd])停止当前正在执行的动画
clearQueue:是否清除动画队列,默认false
jumpToEnd:是否跳转到当前动画队列的最终效果,默认false
五,创建节点
1,$('节点名')
-------------------------------今日内容--------------------------------------
一,节点操作
1,添加节点
    (1)最后一个子元素添加
        append('selector')  对js 中appendChild()的封装
        结构:   父元素.append(子元素)   把子元素添加到父元素里面去,作为最后一个子元素
             注: 1)子元素可以是页面上存在的元素,存在剪切的效果
                2)子元素也可以是新创建的元素,有新增一个标签的效果    eg:   $('div').append('<p>新增内容</p>'),在div里面新添加一个p元素
        appendTo('selector')
        结构:   子元素.appendTo(父元素) 把子元素添加到父元素内,作为最后一个子元素
        注意:参数'selector',可以是选择器,也可以是传入的某个元素如$('元素')
    (2)第一子元素添加
        操作的方法同append
        prepend('selector')
        结构:父元素.prepend(子元素)  把子元素添加到父元素里面去,作为第一个子元素  
        perpendTo('selector')
        结构:子元素.perpendTo(父元素) 把子元素添加到父元素内,作为第一个子元素
    (3)兄弟元素添加
        after()
        结构: 参考元素.after(新元素)   把新元素做为兄弟元素放在参考元素的后面
        before()
        结构: 参考元素.after(新元素)   把新元素做为兄弟元素放在参考元素的前面
2,清空元素
(1)清空
结构:  元素.empty()     清空元素内部的所有元素和元素身上绑定的事件,自身会保留(清理门户)
(2)删除
结构:  元素.remove()      自身删除,包括自己内部的子元素(自杀) 
3,克隆节点
(1)克隆
clone(boolen)
结构:   元素.clone()   克隆一个元素,返回值是克隆出来的新元素
  常用写法:  元素.clone().appendTo(父元素)
boolen:  true   克隆元素和内部元素,连同元素身上的事件一起克隆
        false   只克隆元素和内部元素,默认值是false
二,特殊属性的操作
    1,表单元素的特殊属性操作
    val()方法    传参就是设置,不传参就是获取
    设置:   val('设置的内容')   
    获取:  元素.val()  返回的值就是元素的value值
三,html和text方法
    html同js中的innerHTML,能识别标签,优化了兼容性问题
    text同js中的innerText,不能识别标签
    设置结构: html('参数')         
    html('')利用空字符串去覆盖原来的内容,达到清空内部元素
            (不推荐,清空元素的事件没有移除,经常使用内存容易溢出)
    获取结构: html()
四,width和height方法
    传参就是设置,不传参就是获取
    设置获取宽高
    css获取的是一个字符串,而且带px单位,这样不利于计算
    width和height获取的是数字,
    设置:  元素.width(num) 给元素的width设置成num
    1,width()                    width
    2,innerWidth()               width+padding 
    3,outerWidth()默认是false     width+padding+border
    4,outerWidth(true)            width+padding+border+margin

    获取网页可视区的宽/高  其实就是获取window的宽高
    $(window).width()
    $(window).height()
五,scrollTop和scrollLeft
    原生js中是window.pageYOffset|| document.documentElement.scrollTop ||document.body.scrollTop
    window.pageYOffset  现代浏览器提出的,只能获取,不能设置
    document.documentElement.scrollTop  实际就是html,ie支持,
    document.body.scrollTop  实际就是body,google浏览器不支持
    jQ中 scrollTop()用来设置和获取页面垂直方向卷曲的距离
    获取:   $(window).scrollTop()
    设置:   $(window).scrollTop(参数)
    Left和Top用法相同
引申:页面缓慢回到顶部   $('html','body').animate({scrollTop:0})
     选择器:    :selected  获取被选中的表单元素(下拉框)
               :checked   多选框,单选框
六,offset和position 
    原生js  offsetLeft/Top 有定位父元素的左/上距离
    jQ中 
    1,  offset()用来获取元素距离页面的距离
        返回的是一个对象{top:XX,left:XX}
    2,  position()用来获取元素距离最近一个有定位父元素的距离;
                 如果最近父元素没有定位就一直往上面找
        返回的是一个对象{top:XX,left:XX}
七,jQuery事件机制
1,简单事件注册
    以事件名的方式注册的事件,如:   元素.click(事件处理函数)   元素.mouseover(事件处理函数)
    优点:同一个事件重复注册,不会存在覆盖问题
    缺点:无法解绑
2,bind()   解绑unbind()
  结构:bind('type',fn)
       'type':事件名;可同时注册多个事件,用空格隔开,但是事件处理函数是同一个
       fn:事件处理函数
解绑事件: 
    unbind()     解绑元素注册的所有事件
    unbind('事件名')     解绑元素注册的指定事件
    优点:可以解绑
    缺点:不支持动态绑定,如果元素是动态创建出来的,那么动态出来的元素没有这个事件
3,delegate()
注册委托事件,用来解决动态绑定
事件委托:把事件注册给父元素,让元素去触发,原理:事件冒泡
结构:
    父元素.delegate('子元素','事件名',事件处理函数)
解绑事件:
    父元素.undelegate()解绑元素所有的事件委托
    父元素.undelegate('子元素','事件名')解绑元素指定的事件委托
4,on()   jQuery  1.7以后都使用这个(推荐使用)
    统一了上面三个事件
    结构:
        on(type,selector,data,fn)
            type:事件名,必填
            selector:选择器,注册事件委托的,选填;如果有就是事件委托,如果没有该参数就是给元素本身注册事件
            data:携带的数据,传递给事件处理函数的,选填
            fn:事件处理函数
    简单事件  元素.on('事件名',事件处理函数)
            是给元素本身注册的
    委托事件  父元素.on('事件名','子元素',事件处理函数)
            事件是注册给了父元素,但是只能由指定的子元素才能触发,后面动态增加的子元素也能触发
    解绑事件 off()
    结构:元素.off()         解绑元素身上的所有事件
        元素.off('事件名')  解绑元素身上的指定事件
        注:解绑委托事件   父元素.on('事件名','子元素')
5,触发事件
    1)以事件名的方式直接调用
       元素.事件名()
    2)trigger()方法
    元素.trigger('事件名')
八,jQuery事件对象
    使用同js的事件对象,在事件处理函数中传入一个形参即可接收
    1,  e.data  是个{},携带的数据 
        在事件处理函数中,可以通过jQ的事件对象e,e.data获取到这个值;originalEvent对象里储存了原生js的事件对象的属性,
        jQ封装了一些新的方法存在事件对象上并解决了兼容性问题
    eg:   $('div').on('click',{name:'li',age:19},function(e){
        e.data
    })
    2,  e.stopPropagation()阻止事件冒泡
    3,  e.preventDefault()阻止浏览器默认行为
    4,  return false; 既能阻止事件冒泡,又能阻止浏览器默认行为;原生js的return false只能阻止浏览器的默认行为,不能阻止事件冒泡;
    





案例知识点:
1, 新增过滤选择器
 :selected   筛选出select下拉框中选中的元素
2,表单元素的value属性的操作(input/textarea)
获取结构:表单元素.val()
设置结构:表单元素.val('内容')
3,trim()  字符串的方法,去除字符串两边的空格
4,事件:
   focus()  获取焦点事件
   blur()   失去焦点事件
   $(window).scroll()   页面滚动条监听事件
5,小火箭返航
    $(window).scrollTop(0),这里是jQ里面封装了scrollTop方法,处理了兼容问题;
    所以在设置动画的时候这样写:
     $('html,body').animate({
       scrollTop:0,   
     })
    因为window.pageYOffset只能获取,不能设置
    document.documentElement.scrollTop 实际就是html,但是有兼容问题
    document.body.scrollTop 实际就是body,但是有兼容问题
6,设置固定定位时需要考虑到在定位的时候会脱离标准流,下面的内容会跑上去被挡在定位元素的下面,
  需要自己设置margin,回到标准流之后要记得手动改回原来的margin
7, 音乐导航案例
 让音频/视频播放    play(),jQuery方法没有封装,是h5提供的,只能由DOM对象进行调用
 让资源重新加载     load(),每次都重新加载,不然每次重复开始之后,音/视频会一直播放结束
 按住不放key.down会一直触发(在google浏览器)
 节流阀: 立一个flag做一个标记,控制走向
 在事件触发的外面立一个flag = true;
 按下的时候:
     if(!flag){
         return;
     }
    flag = false;
抬起的时候:flag = true;
google浏览器如果页面刷新直接移入会报错:用户没有第一次交互,只要在空白的地方点击一下,就可以触发移入和移出事件了




