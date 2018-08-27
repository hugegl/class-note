--------------------复习--------------------------
1,jQ:js库,里面提供很多功能
2,版本:1.X   2.X   3.X    min和不带min
3,入口函数: $(document).ready(function(){内容})
           $(function(){})
4,$:来源于jQ,是个函数,参数不同,作用不同:函数(入口函数);选择器(获取元素);DOM对象(DOM对象转jQ对象)
5,DOM对象:通过原生js方法获取到的元素就是DOM对象
  jQ对象:通过jQ提供$()获取到的元素就是jQ对象
  DOM对象转jQ对象==>$(DOM对象)
  jQ对象转DOM对象==>通过下标[index],get(index)
6,选择器:
   css选择器
   过滤选择器:      :odd  奇数
                    :even  偶数
                    :first  第一个
                    :last   最后一个
                    :eq(index)  指定下标
  筛选选择器:      children()    子代
                  find()      后代
                  siblings()   兄弟元素
                  next()     下一个兄弟元素
                  prev()      上一个兄弟元素
                  parent()     父元素
                  eq(index)          指定下标
方法:    index()    获取当前元素在所有兄弟元素中的索引
         show()      显示元素
         hide()      隐藏元素
         css()       设置/获取元素的样式
         text()      设置/获取元素的内容
--------------------今日内容--------------------------
一,css操作
进行设置性操作的时候,会给获取到的所有的元素都设置相同的样式
1,设置单个样式操作   css(name,value)
      $('元素').css('样式名','样式值')
2,设置多个样式操作   css({})
      $('元素').css({  //传对象的时候,name的''加不加随意
        样式名:'样式值',
        样式名:'样式值',
        样式名:'样式值',
        ...
      })
      注意:
      1)样式名写的注意点    'font-size'或者fontSize
      2)样式值       '30px'或者30   '30%'
3,获取元素样式     css('name')
    进行获取性操作的时候,获取第一个元素的对应的样式值即可;
    获取的时候获取的是第一个的样式值,因为jQuery里面默认获取到的这个伪数组中第一个的值,不会隐式迭代
二,class操作
1,添加类名          addClass('name')
2,移除类名          removeClass('name')
3,判断是否有类名    hasClass('name')   
    返回值true(有这个类名)/false(没有这个类名)
    只要有一个元素有指定的类名就返回true
4,切换类名         toggleClass('name')
有就删除,没有就添加

四,属性操作
1,设置和获取元素的属性   attr()
  设置单个属性   attr('name','value')
  设置多个属性   attr({      //传对象的时候,name的''加不加随意
                name:'value',
                name:'value',
                name:'value',
                ...
              })
2,获取元素对应的属性   attr('name')            
3,移除元素的属性      removeAttr('name')
4,获取和设置表单的属性      prop()
表单上一些属性值为boolen类型的属性  使用 prop('name','value')
  jQ版本1.6以后的版本,使用attr去获取checked,selected,disabled这些表单属性的时候,获取不到值,
  可使用prop('name',true/false)达到效果
  有一些文档和博客上写的:  标签上的自定义属性用attr方法;对于标签固有的属性用prop方法(如src,title,checked,disabled,selected,width)
 使用建议: attr方法使用的比较多,但是对于checked,selected,disabled只能使用prop方法


五,动画效果
1,显示和隐藏
    1)显示:
    show(speed,'easing',callback)
        不传参,没有动画效果,主要修改的是元素的width,height,opacity
        speed:动画时长,动画速度,可选参数
               直接写数字,默认单位是ms;
               字符串参数:'slow'/600ms;'normal'/400ms;'fast'/200ms;如果传递是上面三个之外的字符串,默认取400ms
        easing:动画效果,可选参数
                默认值是swing,意思是秋千,先慢,再快,再慢
                linear,匀速
        callback:回调函数,可选参数
                  动画效果结束后执行的代码
    2)隐藏:
    hide(speed,easing,callback)
        同show的参数
    3)切换
    toggle(speed,easing,callback)
        同show的参数
        如果是展示的,就隐藏;如果是隐藏的就展示出来
2,滑入和滑出
   1)滑入:
   slideDown(speed,easing,callback)
        同show的参数
        不传参,有动画效果,默认值是normal ==>400ms
        从上往下缓慢展示,改变的是height
  2)滑出:
  slideUp(speed,easing,callback)
        同show的参数
  3)切换:
  slideToggle(speed,easing,callback)
        同show的参数
3,淡入淡出
不传参,有动画效果
  1)淡入
  fadeIn(speed,easing,callback)
        同show的参数
  2)淡出
  fadeOut(speed,easing,callback)
        同show的参数
  3)切换
  fadeToggle(speed,easing,callback)
        同show的参数
4,自定义动画
animate(obj,speed,easing,callback)
参数:
1)obj,必写参数
  是一个对象,对象里面写上你需要做的动画样式,可以设置多个样式,同时一起做运动
  eg:  animate({
    left:30,
    top:20,
    ...
  })
2)speed,easing,callback 三个参数同show()方法的参数,都是可选参数
注意:做动画的元素要配合定位使用,不然没法脱离标准流动起来
六,动画队列
  回调地狱:在动画函数的回调函数内嵌套很多层,会形成回调函数
1,定义,优缺点:
  定义:给元素的动画队列里面添加多个动画,依次来执行动画队列里面的动画
  动画队列:来实现依次执行的效果,就是链式编程的写法
  结构:元素.动画效果().动画效果()....
  优点:可以实现依次执行动画的效果
  缺点:如果元素动画频繁的触发,就会不停的去做动画队列里面的动画
  
2,停止当前正在执行的动画:stop(),如果元素的动画队列里面有后续动画,就执行后续动画去了
  stop(clearQueue,jumpToEnd)
  clearQueue:是否清除动画队列,true/清除;默认值是false
  jumpToEnd:跳转到当前正在执行动画的最后效果,true/跳转;默认值是false
七,jQuery节点操作
1,创建节点
      $('html标签')
2,添加节点
      $('父元素').append(创建的节点)







案例知识点
美女相册:
    1,注册事件虽然可以注册在a外面的li上面,事件冒泡用return false也可以阻止a链接的默认行为,
      但是直接注册给a,查找起来更方便,更好控制;
    2,阻止a链接的默认行为
        1)return false;//必须放在函数的最后一行
        2)e.preventDault();//可以放在函数的随意一行
全选反选案例:
    3,控制台上,三个小点,最下面可以disable javascript,阻止此网页的js效果
    4,选择器:
      :checked        被选中的个数   eg: input:checked     获取选中的input的元素
    5,比较选中的长度和总的长度是true还是false,可以省略if判断语句
    直接将结果赋值给全选的input标签.
京东轮播案例:
 开启定时器一定要用变量接收一下,再重新开启定时器的时候写变量名接收的时候,不要写var ,写了var就是局部变量,外面访问不到,无法接收
手风琴案例:
 jQ中通过css设置的样式会给所有元素设置上相同的样式,所以给每个li设置不同的背景图片,需要手动遍历
查找元素的过程,很消耗性能,一般var 一个变量接收一下比较好,一般在变量名前面加$区分一下
插件网站:www.jq22.com
素材网站:www.17素材网











