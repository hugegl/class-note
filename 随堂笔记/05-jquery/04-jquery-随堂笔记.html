-------------------------------复习------------------------------
一,创建节点
    1,$('html标签')
二,添加节点
    append  appendTo  preprnd prependTo after before
三,删除,清空,克隆
    remove()  删除自身
    empty()    删除子元素
    html('')   不建议使用
    clone(参数)     克隆;参数,是否克隆事件?true为克隆
四,方法
    val()               获取/设置表单元素的value属性值
    html() text()       设置/获取元素的内容,html能识别标签,传参就是设置,不传参就是获取
    width()/height()    设置和获取元素的宽高的,contaner
    innerWidth()/innerHeight()    设置和获取元素的宽高的,contaner+padding
    outerWidth()/outerHeight()    设置和获取元素的宽高的,contaner+padding+border,默认值是false
    outerWidth(true)/outerHeight(true)    设置和获取元素的宽高的,contaner+padding+border+margin 
    $(window).width()/height()      获取可视区的宽/高
    scrollTop/Left    设置和获取页面垂直/水平卷曲的距离
    scroll 事件,可以监听页面实时的scrollTop/Left值
    让页面缓慢的回到顶部 $('html,body').animate({scrollTop:0})
    offset()获取元素距离页面的位置,返回值是{left:XX,height:}
    position()获取元素距离有定位父元素的位置,返回值是{left:XX,height:}
五,事件发展历程
    1,以事件名的方式注册的简单事件,如 click(),缺点:不能移除,无法解绑
    2,bind()   用法bind('事件名',事件处理函数)   解绑:unbind()  ,缺点:不支持动态绑定,新创建出来的元素没有绑定的事件
    3,delegate()     用法delegate('子元素','事件名',事件处理函数),缺点:不能让父元素来触发
    4,on()   在jQ1.7版本以后统一用on()注册事件
    用法:   on('事件名',['selector'],[data],事件处理函数)
    事件名和时间处理函数是必选,子元素和data是可选的
    data:携带的数据,给事件处理函数里面去使用,通过事件对象e.data
    'selector':选择器,有有事注册事件委托,没有就是给元素自身注册事件,可选
    5,off()解绑on注册的事件????????
        off()解绑元素所有的事件
        off('事件名')解绑元素所有的指定事件
        off('事件名','selector')解绑委托事件
    6,触发事件
    1)以事件名调用,如click()
    2)trigger('事件名')
六,jQ的事件对象
    把原生js的事件对象给封装了,处理了兼容性的问题
    keyCode  
    e.stopPropagation()阻止事件冒泡
    e.preventDefault()阻止浏览器的默认行为
    return false  jQ里面可以阻止事件冒泡,阻止浏览器的默认行为,原生js里面只能阻止浏览器的默认行为
    七,节流阀
    让事件有限制的触发
-------------------------------今日内容------------------------------
一,昨日知识点补充
1,on注册事件的时候,事件对象data,不要传字符串,其他都可以,如果传字符串可能会被误认为是选择器(第二个参数必须要有就是事件委托的选择器)
二,隐式迭代
    jQ在设置性操作的时候,会给所有元素设置成相同的值
    jQ在获取性操作的时候,只获取第一个元素的值
    如果想要手动遍历iQ对象,可以使用each()方法
    1,隐式迭代
    定义:偷偷遍历,偷偷循环
    在进行设置性操作的时候,会把所有获取到的元素设置上相同的操作
    2,each()
    结构: each(fn)
    fn:函数,让每一个jQ对象都来执行这个函数
          function(index,item){
            函数体
          }
          index:形参,jQ对象对应的下标 
          item:形参,jQ对象对应的每个元素,是个DOM对象
          注意:在这个函数里面,可以使用this来表示当前遍历的元素
三,链式编程
      原理:设置操作的时候,返回的是一个jQ对象,因此可以继续使用链式编程
      获取操作时,获取的是具体的值,并不是jQ对象,不能调用jQ的方法
      总结:在进行设置性操作的时候,返回的是一个jQ对象,这样才可以继续链式编程下去;
      在进行获取性操作的时候,返回的是获取的值,就不可以调用jQ的方法
四,end()方法
    五角星案例引出
    prevObject属性,写的时候不用加(),直接写;
    jQ对象中有一个属性叫prevObject,作用:找到上一次返回的jQ对象
    所以jQ封装了一个方法,将prevObject属性进行封装了,这样不会将方法和属性混在一起写了
    eg:  
      $(this).text('★').precAll().text('★').prevObject.nextAll().text('☆')
      $(this).text('★').precAll().text('★').end().nextAll().text('☆')
五,多库共存
    场景:引入别的库,可能会造成$符号冲突的情况
    1,jQuery也可以达到$的效果
    2,解绑$的控制权,并返回功能,用新的变量接收即可以重新使用jQuery函数
    var 变量名  = jQuery.noConflict()
六,jQuery插件
1,jQ提供的animate默认值支持做数字型的动画,不支持颜色的动画
 jquery.color.js   让js的animate支持做颜色动画
2,定义:插件其实就是个js文件,这个js文件依赖于jQuery,并且在jQuery的基础上增加了一些功能
3,使用步骤:
  1)引入jQ库
  2)引入插件
  3)使用插件
5,jquery.lazyload.js  懒加载
img标签有了src属性,会立即去加载资源
    1)引入js插件,用data-original属性替换掉src属性;
    2)建议给需要懒加载的图片加个公共类: class = "lazy";
    3)应该给图片宽高
    4)调用lazyload()方法
    结构    在js代码中写:
            $('img.lazy').lazyload()
   lazyload({
     placeholder:路径,//路径是图片路径,就是在加载的过程中会先加载占位图片
   })
七,封装插件
    jQ实例对象可以使用原型上的属性和方法
    插件原理:在jQuery的原型上添加了插件提供的方法
    1,jQuery原型:
      (1)jQuery.prototype
      (2)jQuery.fn 
      (3)$.prototype
      (4)$.fn
    2,添加方法:
    eg:   
    $.fn = function(color){
    //this:谁调用的this就指向谁
    this.css('backgroundColor',color);
    //返回当前的jQ对象,目的是为了链式编程 
    return this;
    }
    3,封装手风琴插件
    传入对应的形参,实参,在对应的位置修改,注意this指向(谁调用,指向谁),注意有一些数据时动态计算的不能写死
八,jQuery框架封装
  jQuery的实质是函数自调用(也称沙箱)
  (funciton(window,undefined){
    var jQuery = funciton(){
      函数体
    }
  window.jQuery = window.$=jQuery;//把jQuery和$暴露给window,变成全局变量
  })(window)
  传参window的好处:
  1,可以减少对window的查找过程
  2,有利于代码压缩
  传参undefined的目的:
    在ie7中undefined可以被赋值
    函数在定义形参的时候,在调用的时候没有传实参,那么这个形参就是undefined
  1,解决ie6,7,8中undefined被篡改的问题








案例知识点
1,弹幕效果
如果元素没有添加到容器内,去获取它的宽高(元素.width()),是没有值的,所以应该先appendTo('父元素')之后再做动画
2,prevAll()   获取当前元素前面所有的兄弟元素
3,nextAll()   获取当前元素后面所有的兄弟元素
4,jQ的容错率特别高,如果传入的是undefind,返回的还是jQ对象,可以继续调用jQ的方法,不会报错

总结兄弟元素:
    siblings(),获取所有的兄弟元素,不包含自己
    next(),获取当前对象的下一个元素
    prev(),获取当前对象的上一个元素
    nextAll(),获取当前对象的后面的所有兄弟元素,不包含自己
    prevAll(),获取当前对象的前面的所有兄弟元素,不包含自己
5,表格删除案例
元素.parents()          获取当前元素所有的父级,返回值是一个对象,包含所有的父级元素
元素.parents('参数')   获取指定参数的父级元素











