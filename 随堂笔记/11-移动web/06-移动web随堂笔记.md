一,复习
1,bootstrap 实现响应式布局框架
引入框架,用类名控制样式及布局;
  实现响应式技术 媒体查询
  响应式布局方式:栅格系统;
  栅格系统:
  容器:   .container   具有响应式版心的容器;默认带15px的左右padding
  容器:   .container-fluid   100%的容器;
  行:     .row     默认带-15px的左右margin
  列:     .col-屏幕-n   一行12列;
          屏幕:   lg md sm xs;
  列偏移:    col-屏幕-offset-n  ;  整体向右偏移n列;
  元素偏移 :   col-屏幕-push-n   ;当前元素向右偏移
               col-屏幕-pull-n   ;当前元素向左偏移
  列和列可以互相嵌套;一列里的一格也可以说是里层列的一行;
  响应式栅格:同一个盒子在不同屏幕上,布局方式也不一样;
  eg:   在大屏幕中占3格,中屏幕中占4格 小屏幕中占6格;
  <div class="col-lg-3  col-md-4 col-sm-6"></div>    //若果不写栅格系统,默认元素占一行;
  响应式显示和隐藏:  visible-屏幕   在哪个屏幕显示;
                    hidden-屏幕    在哪个屏幕隐藏; 
二,今日内容-微金所案例
1,css样式查找,大盒子的第二个类名;
2,轮播图需要单独补touch事件;
  使用jQuery注册touch事件,返回的事件对象是jQ的事件对象;
  jQ对jQ的事件对象进行了封装,需要这样取出来原始的事件对象:
    e.originalEvent.targetTouchs[0].clientX;
3,轮播图控制的方法   看插件的文档;按照内部指示填对应参数即可
  $('.carousel').carousel('参数');
  参数:  prev  上一张;
         next  下一张;
         pasue  停止播放;
         cycle  继续播放;
         更改轮播图播放的时间
4,a标签的href属性和data-target都 指向控制的模板;
5,如果有个盒子
    position:absolute;
    top:6px;
再设置bottom:0px; 这样不会起作用;需要先写个top:auto;//让前面top设置的值不在控制元素,让其他的去控制元素;
三,rem用于布局
  流式布局:百分比布局 实现移动宽度自适应;
  响应式布局:一个页面在多个设备完美布局;
  rem单位进行布局:实现盒子宽高自适应的布局;
    1,rem定义: root+em的意思;根标签的字体大小;网页中的根标签就是html标签的font-size属性;
    2,em单位可以实现宽高自适应布局,但是em既要用于设置自身的字体大小,又要用于子盒子布局,会导致布局混乱,不建议使用;
      解决方法:找一个不用于布局标签font-size属性作为布局单位,就是html标签;
      html标签字体大小就是rem;
    3,实际工作中设计稿是以px为单位的;用户的屏幕宽度是用@media媒体查询出来px;它们与rem之间的换算是:
      eg: 设计稿640px  设置1rem = 100px;
      当前设备的1rem值= (当前设备宽/设计稿宽度*100)px;
    4,用js动态获取当前屏幕的宽度,动态设置rem的值;
    已知:设计稿宽度;设置html的1rem = 100px;
        1)获取当前屏幕的宽度: window.innerWidth;
        2)动态设置rem的值:   
        document.querySelector('html').style.fontSize =  window.innerWidth/设计稿的宽度 * 100;
    注意,引入rem的js文件,要在页面开始加载之前;先把rem算好,再渲染页面;
    5,用rem布局时,如果遇到0.3这种小数,会出现精度丢失的问题 ,0.300004,会造成盒子掉下来的情况;
    所以用百分比结合rem;百分比布局外面的大盒子,字体和图片用rem;
四,总复习
1,web的开发方式
  1)pc端+移动端页面;//之前已经写好pc端
    优点:页面结构清晰,方便维护;
    缺点:成本较高;pad上适配用户体验稍差,可能还要处理新设备的兼容问题;
  2)响应式;//用于新网站
    优点:可以兼容任何设备;
    缺点:代码结构冗余;网页的加载速度慢;考虑兼容问题较多;
2,移动端布局和pc端布局的差异
  1)屏幕
    pc端屏幕大,pc端基于版心,盒子是宽高固定的布局方式;
    移动端屏幕小,全屏布局,自适应的布局方式;设置视口;
  2)兼容
    pc端要考虑低版本和高版本的兼容;
    移动端只需要考虑高版本的兼容;-webkit-前缀;
  3)布局思想:只要在任何状态下,网页不乱;
3,移动端技术
  1)屏幕 
    pc端1px = 1物理像素;
    移动端 1px = 1物理像素//1倍屏;
          1px = 2物理像素//2倍屏;
          1px = 3物理像素//3倍屏;
        解决方法:设计图会有2倍图/3倍图解决;使用时进行图片压缩;
          background-size;如果是img就指定width/height;
  2)视口  移动端虚拟的布局区域;
  要写出和屏幕一样宽的页面
      设置视口将width = device.width;
      initial-cale = 1.0;
      user-scalable = no;
      maximum-scale=1.0;
      minimum-scale=1.0;
  3)触屏事件
    事件类型:
        touchstart
        touchmove
        touchend
        touchcancel
    获取触屏数据,即事件对象中的数据: 
     targetTouches:记录目标元素上的数据
     changeTouches:记录触屏状态改变时的数据
     Touches:屏幕上所有触屏的数据
     获取坐标:  e.targetTouches[0].clientX/Y;
  4)tap封装
    在移动端先触发touch,click有300ms的延迟;
    利用touch事件先触发的现象,将移动端的点击事件封装成tap事件;条件:触屏过程中手指未移动过,触屏时间<150ms;
4,布局
  1)单位
    px :宽高固定的布局;
    em :设置字体,首行缩进;
    百分比 :流式布局,宽度自适应;高度是固定的;
    rem :宽高自适应;html的font-size属性;根标签字体的大小;
    使用步骤:先用px写页面;将px换算成rem;使用媒体查询或者js,根据屏幕的宽度动态设置rem的大小;
  2)技术
    BFC:
      触发BFC  overflow:hidden;float:flet;position:fixed/absolute;display:table/table-cell;
      BFC的特点  BFC内部元素的布局不会影响外部元素布局;BFC的盒子不会和浮动元素有交集;
    圣杯布局/双飞翼布局//两边固定,中间自适应
      方式:BFC;padding+定位;伸缩布局(左右宽高固定用px,中间的flex=1);
    媒体查询
      响应式布局:一个页面能够在任何设备上完美布局
      语法:@media screen and(max-width:2000px) and(min-width:992px){执行代码};//处于这个屏幕区间就使用这个样式,如果不满足,就不起作用;
      栅格系统
          使用栅格系统进行布局 布局完成,意味着响应式已经实现;完成布局细节;
5,less
  嵌套
  变量
  函数
  混入
  计算
  导入
6,插件
  echart      图表工具,数据可视化;
  isroll.js   触屏滑动的插件,布局特点:外面盒子短,里面盒子长超出外部的盒子,实现滚动效果;
  swiper.js   移动端触屏轮播图插件;
  zepto.js    移动端类似于js的工具库;
  bootstrap   移动端优先,响应式布局框架; 

7,先整体布局,后细节
  布局过程中,优先使用块级元素,浮动,定位;行内块是最后的选择,行内块有默认边距(个人建议)    









