一,复习
1, offset系列
结构:offset属性
1)offsetLeft  距离定位父元素的左偏移量
2)offsetHeight  元素的高度(content+padding+boeder)
3)offsetParent   离自己最近的定位父元素
4)offsetTop     距离自己最近父元素的上偏移量
5)offsetWidth  元素的宽度(content+padding+boeder)
2,client系列:
clientWidth   元素的可视区的宽度(content+padding)
clientHeight   元素的可视区的高度(content+padding)
3,scroll系列
scrollLeft   元素内容左边滚动出去的距离(可赋值,直接写数字)
scrollTop   元素内容上边滚动出去的距离(可赋值,直接写数字)
scrollWidth    元素内容的宽度
scrollHeight    元素内容的高度

4,浏览器可视区的宽高
window.innerWidth
window.innerHeight

5,整个页面滚动出去的距离
window.pageXOffset   /window.pageYOffset

6,监听元素的滚动条:   元素.onscroll
7,监听浏览器的滚动条:   window.onscroll
--------------------------今日内容---------------------------------------
一,回顾简单动画案例
按钮,从0移动到400px
二,封装动画函数
封装按钮处理事件(让一个元素从左往右,从右往左移动)
作用:让一个元素从左往右,或者从右往左
element:传入一个元素
target:元素的目标位置 数字
step:  步数
1)  元素.timeid   直接把timeid放到元素的身上,元素是对象,这个是把timeid当做对象的一个属性存储在元素身上
2)回调函数:
定义:封装函数中有一个参数是函数,要求用户调用封装函数时,传入一个函数
判断到了目标后调用函数,并且判断是否转入的是个函数(可以不传函数,那么久不进来,也不会报错,函数为true,不传函数时false)
三,轮播图
1)全局申明一个变量,存储当前展示的哪张图片的下标
默认为0,在下标点击时,随时修改全局存储的下标
2)在代码中调用点击事件/已经注册过的事件,只需要写:
     该元素.on事件();   //也是触发了该事件
 














