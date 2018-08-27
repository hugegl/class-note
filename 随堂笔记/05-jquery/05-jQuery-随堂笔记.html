---------------------------------复习----------------------------------
1,链式编程原理:在进行设置的性操作的时候,方法内部return this
一,隐式迭代
1,偷偷的遍历,对于设置性操作,将获取到的元素都设置上相同的操作;获取性操作,获取第一个元素的值
2,需要给每个元素设置上不同的操作,需要手动遍历
3,each()  作用:遍历获取到的jQ对象
    each(function(index,ele){,里面用this表示当前遍历的元素函数体})//index是下标;ele是对应这个元素,都是用来接收的,都是形参名
二,链式编程 
1,可以使用.一直调用下去;只有进行设置性操作,返回jQ对象,可以继续链式编程下去;获取性操作,返回的获取的值,不能继续链式
2,prevObject/end()  找到上一次返回的jQ对象
三,多库共存
1,解决$的冲突问题
var 变量名 =  jQuery.noConflict()  返回的是$函数,可以用变量名接收,变量名可以代替$的作用
四,jQ插件
1,js 文件,依赖于jQuery,在jQ的基础上,添加了一些方法
2,jQ的原型      $.fn    方法内的this指向:谁调用的方法,this就指向谁
五,现有的插件
1,jQuery.color.js 支持让animate做颜色的动画
2,jQuery.lazyload.js  做图片的懒加载
六,制作插件
1,在方法内return this;
七,封装jQ
1,沙箱:防止全局污染的问题
(function(window,undefined){
  var jQuery = function(){

  }
  window.jQuery = window.$ = jQuery
})(window)
2,传参window:1,减少对window的查找过程;2,有利于代码压缩
3,传参undefined:解决undefined在ie678中被篡改的问题
---------------------------------今日内容----------------------------------
一,封装jQ
(function(window,undefined){
var jQuery = function(selector){
  var version = '666',//版本号
  var arr = [];
  var push = arr.push;
return new jQuery.fn.init(selector)

}
//往jQuery的原型上添加方法
//jQuery.prototype.html = function(){函数体}
//原型替换
jQuery.fn = jQuery.prototype = {
  //添加constructor属性,指向构造函数
  constructor:jQuery,
  //这个init才是jQuery构造函数
  //1,获取元素 
  //2,dom对象转成jQ对象
  //3,创建元素
  //4,入口函数
  以下是1.7的版本的写法:
  init:function(){
    
    //selector  用来获取元素
    var  elements = document.querySelectorAll(selector)//获取到的是伪数组
    //this指向实例对象
    this[0] = elements[0]//这样只能存第一个
    //用遍历来将获取到的元素添加到this实例对象上去
    <!-- for(var i= 0,i < elements.length;i++){
      this[i] = elements[i]
    }
    //手动给实例对象添加lenght属性
    this.length = elements.length -->
    //优化for循环
    //借用push方法  call(obj,1,2,3)   apply(obj,[1,2,3])
    //借用数组的push两种写法:  [].push     Array.prototype.push
    [].push.apply(this,elements)//前面用了var push = arr.push,这边可以直接用push(不用写[].push)
    //this:借用push的方法,elements:要添加到this上去的元素
    //数组的push方法内部维护length属性
  },
  jquery:version,
  html:function(){函数体},
  css:function(){函数体},
  width:function(){函数体},
  //需要添加很多函数方法的时候
  extend:function(o){
    for(var k in o){
      this[k] = o[k];
    }
  }
  jQuery.fn.extend({
    方法名:函数体,
    方法名:函数体,
    方法名:函数体,
    方法名:函数体,
  })
}
以下是1.7以后版本的写法:
jQuery.fn.init=function(){函数体}
//修改init构造函数的原型指向,改成jQuery.prototype
jQuery.fn.init.prototype = jQuery.fn;//只能修改原型的指向,不能将指向改成new出来的实例对象
window.jQuery = window.$ = jQuery;
}(window))



二,工厂模式
定义:是设计模式当中的一种
实例创造的特点:必须通过new构造函数,才能得到一个实例对象
封装new构造函数的函数结构:   function 工厂函数名(变量名){return new 构造函数(变量名)}
三,jQuery的版本获取
   1.7的版本:    $('选择器').jquery   返回值是当前使用的jQuery版本
四,
extend:拓展
         var obj = {
        name:'哈哈',
        age:18,
        }
        var obj2={
          height:170,
          color:'red',
        }
  把obj2的属性放到obj里面去
  1)遍历后放进去   for(var k in obj2){ obj[k] = obj2[k]}      
        obj[k] 给obj添加k属性,obj2[k]拿到obj2中看属性的值;
  2)   obj.extend = function( ooo){
    for(var k in ooo){ this[k] = ooo[k]}
  }
  以后添加的话直接调用方法    obj.extend(obj2)/obj.extend(obj3)



