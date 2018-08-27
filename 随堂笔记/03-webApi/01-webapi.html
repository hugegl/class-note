一,简介
1,webAPI: 
2,DOM:文档对象模型,把页面上的标签抽象成对象,通过操作对象来实现操作标签的目的
3,元素:html中的标签在DOM中称为元素
  1)常用操作
     (1)获取元素
     (2)操作元素
     (3)动态创建元素
     (4)给元素注册事件
4,网页中几个基本对象
    doucument对象       =>整个页面     通过doucument直接获取整个页面
    doucumentElement    =>html标签    通过doucument.doucumentElement获取html标签
    body                =>body标签    通过doucument.获取body标签
    div         
二,获取页面中的元素
通过document调用,在整个页面中找
    1,批量获取页面上指定的标签
        定义:通过标签名获取多个元素,也可以通过元素获取
        结构:doucument/element.getElementsByTagName('标签名')
        返回值:伪数组,存储了页面上符合标签名所有的标签,包括子级
        可通过元素调用标签伪数组
        通过元素调用,在元素下面找
            1,通过元素调用
            定义:在元素的范围内找
            需先通过document获取到该元素
            结构:
            元素1.getElementsByTagName('标签名')
            获取对应的某一个元素:getElementsByTagName('标签名')[下标]
                               元素1[下标];   //与上面的对应,从伪数组的下标获取对应的某一个元素
            eg: 
            var a = getElementById('id名');
            var b = a.getElementsByTagName('标签名');    获取a元素下面的所有标签
        如果找不到,返回一个空的伪数组
    2,获取页面上指定的标签
        定义:通过id名获取元素
        结构:doucument.getElementById('id名')
        返回值:一个元素
        如果找不到返回null
        全局唯一,通过document调用
    引申:直接写id名,浏览器会自动获取到
    eg: 
        conosle.log(box);也可以直接获取到id名为box的元素(上线后不推荐使用)
        浏览器自动帮我们做的事:  var box = document.getElementById('box');
    3,获取body标签:  doucument.body
    4,获取html标签:  doucument.doucumentElement
引申:  获取元素的其他方式:
   1,通过name属性获取元素   opera和ie会返回id为此名字的元素(兼容问题)不能通过元素调用
    结构:document.getElementsByName('class的名字')
   返回值:伪数组,找不到返回空的伪数组
   2,通过类名获取元素      ie9以上才支持
    结构:document/elemenet.getElementsByClassName('class的名字')
   返回值:伪数组,找不到返回空的伪数组
   3,通过选择器查找元素   ie8+可以用(推荐使用)   也可通过元素获取
    结构:document/element.querSelector('与css的选择器一模一样')
    返回值:返回所有符合条件的第一个
    结构:document/element.querSelectorAll('与css的选择器一模一样')
    返回值:伪数组
三,事件
  定义:当触发某一个条件的时候会执行一段代码
  结构: 元素名.on事件名 = 函数
  事件三要素:事件源,事件名,事件处理函数
  事件源:给谁注册事件,谁就是事件名
  事件名:要注册什么事件,那个事件名就是什么   eg:点击事件名是:click
  事件处理函数:事件触发的时候会被调用的函数
  1,点击事件
    结构: 元素名.onclick = function(){
      //执行代码
    }
练习引申:
1)点击btn按钮,点击是切换图片
   (1)获取btn,img元素
   (2)给btn注册点击事件
   (3)在事件处理函数中,修改img的路径地址(修改img的src属性)
   (4)来回切换图片,在注册事件函数外面声明flag = true;
       注册事件函数内用if...else判断语句,修改flag属性和执行函数
        eg:
        var btn = document.getElementById('btn');
        var img = document.getElementById('img');
        var flag = true;//注意,此标记需写在函数外面,不然每次执行函数都默认把flag赋值为true
        btn.onclick = function(){//true默认是a图片
                  if(flag){ //flag默认值是true
                    img.src = 'images/b.jpg';
                    flag = false;
                  }else{
                    img.src = 'images/a.jpg';
                    flag = true;
                  // console.log(flag);
                  }
                }
2)a链接注册点击事件
        (1)阻止a链接的默认行为,在事件函数最后一行写 return false;
        (2) 如果a的href属性里面写javascript:  
        这个javascript代表协议,作用:改变了a的默认行为,会执行javascript后面的代码;
        void 是js中的一个关键字 作用:什么都不做
        eg: 
        <a href="javascript:void(0);" ></a>     
        <a href="javascript:void 0;" ></a>     
        <a href="javascript:;" ></a>     
3)美女相册
for循环,利用this指向点击的对应对象,谁触发点击事件,this就指向谁
       var links = 获取到a链接的伪数组
       var img = 获取到img大图的元素
       var p = 获取到 p标签
       for(var i = 0;i < links.length;i++){
           links[i].onclick = function(){
               img.src = this.href;
                p.innerText = this.title;
                return false;
           }
       }
4)来回切换9张图片
       (1)获取img元素
       img.src


四,操作元素的属性(非表单元素)
结构: 
     (1)获取元素(通过document)
     (2)获取属性      结构 :元素.属性名
     (3)给属性赋值    结构 :元素.属性名 = 值
五,innerText和innerHTML   获取元素的文本和内容(包括标签)
1,innerText
    获取返回值:文本,所有文本,包括子级的
    赋值:只能是文本,不能是标签;如果赋值标签会解析成文本,不能识别成标签去渲染
2,innerHTML 
    获取返回值:内容,包括文本,包括标签
    赋值:可以是文本,也可以是标签;如果赋值标签会解析成标签,可以识别成标签去渲染
    赋值可以赋值单标签
相同点:   1)innerText和innerHTML   赋值会覆盖原来的内容
         2)一般用来获取双标签中的内容,单标签的不能获取,可以用属性的方法获取
兼容问题:
        1)innerHTML是非标准属性(非w3c标准),但所有的浏览器都支持
        2)innerText属性存在兼容问题,早期的火狐浏览器不支持,使用textContent替代






