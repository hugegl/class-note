一,复习
    1,操作表单元素的属性:像disable,checked,selected这类在html中,只需要写属性名的属性,在js中,用true/false老控制
    2,操作元素的样式:
    行内:元素.style.属性名 = '属性值(单位)'
    类名: 元素.className = '类名',直接赋值会覆盖原来的类名
    3,操作标签的自定义属性:
    获取:元素.getAttribute('属性名'),返回值时:属性值
    设置:元素.setAttribute('属性名','属性值')
    移除:元素.removeAttribute('属性名')
二,节点
    定义:一个html页面上的所有内容都是节点
    包括:文档节点,标签/元素节点,文本节点,属性节点,注释节点
1,节点类型的属性
        nodeName:   大写(标签名)    小写(属性名)  文本(text)
        返回值:节点的名称
        nodeType:  1(标签)   2(属性)       3(文本)
        返回值:节点的类型        
        nodeValue:   null     属性值      文本内容
        返回值:节点的值  
        
        注释节点:name(#conment),type(8),value(注释内容)
2,节点层级的属性
        1)元素.childNodes     
        返回值:伪数组,存储元素的所有子节点
        2)元素.children    ie6-8可能会返回注释节点
        返回值:伪数组,存储所有的子元素/子标签节点
        3)元素.parentNode 
        返回值:一个父节点(父元素/父标签)
    4)元素.parentElement     (课堂未说)
    返回值:一个父元素
        5)元素.nextElementSibling 
        返回值:返回下一个兄弟元素
        6)元素.previousElementSibling 
        返回值:返回上一个兄弟元素
-----------------拓展其他找子节点--------------
        7) firstChild           第一个子节点
        8) firstElementChild    第一个子元素   ie9+支持
        9) lastChild            最后一个子节点
        10) lastElementChild    最后一个子元素   ie9+支持
        11) nextSibling         下一个兄弟节点
        12) previousSibling     上一个兄弟节点
        13) nextElementSibling         下一个兄弟元素   ie9+支持
        14) previousElementSibling     上一个兄弟元素   ie9+支持

3,操作节点的方法
    1)在后面添加子节点,像追加,有剪切的效果
        结构:父元素.appendChild(子节点)
        注:子节点直接写,不是字符串
    2)在前面插入子节点,有剪切的效果
        结构:父元素.insertBefore(a,b)
        注:a要添加的子节点,b参考的子节点,效果为a插入到b的前面
    3)移除节点
        结构:父元素.removeChild(子节点)
    4)替换节点
        结构:父元素.replaceChild(新的子节点,被替换的子节点)
    5)克隆节点
        结构:元素.cloneNode(true/false);如果不写,默认传了一个false
             注意:false 是浅拷贝,克隆元素本身
                  true  是深拷贝,克隆元素里面的所有内容

 总结:
 1)添加节点:appendChild,insertBefore(新节点,参考节点)
 2)替换:replaceChild(新节点,被替换的节点)
 以上这三个都有剪切的效果
 3)移除节点:removeChild
 4)克隆节点:cloneNode(true/false)  传true就是克隆所有,不传就是只克隆节点本身
 
三,dom树
      定义:一个html页面上的所有内容都是节点,当浏览器加载一个html页面的时候,会把页面中的所有内容加载到内存中,按照他们的关联关系组织管理起来,他们的这种关联关系,看起来像一棵树,所以我们把他们在内存中的存储形式称之为是dom树
      小结:如果元素在dom树上,会渲染,不在dom树上就不会渲染出来(先记,后续随知识点增加会变化)
四,动态创建元素
1,innerHTML      效率低,如果放在for循环内会增加浏览器渲染的时间,最好一次性渲染,不要每次(加一点)渲染,字符串转换成元素需要时间,所以较慢
    结构:innerHTML = '标签内容'
    可以识别标签,可以用来动态创建元素,并且直接渲染到页面上
    即创建元素,又添加到dom树上
2,document.createElement('标签名')     效率高
    专门用来创建元素,返回值是新的元素,但是这个元素不在dom树上
    需配合操作节点的方法把新创建的标签添加到dom树上
    只创建元素 
3,document.write('html形式的字符串')(慎用)
    只能用document调用,只能加到body里面
    直接写在script标签里面
    注意:如果这个写在script标签内,不会覆盖原来的内容
         但写在点击事件函数内,会覆盖点击事件所有的body内容



引申:
打印标签时:
      console.log('打印内容')   浏览器的优化行为,当做标签打印在控制台上
      console.dir('打印内容')   以对象的形式打印内容
for(;;){}这样写也是符合语法的,;;前后不用写也可以
点击事件后动态创建的元素有样式或别的什么功能的,需写在动态创建函数内部,不然没有触发事件,先渲染,再触发事件,则不会渲染出来









