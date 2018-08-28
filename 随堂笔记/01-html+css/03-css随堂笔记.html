快捷键:   bd+    +tab键边框

清除列表的圆点:
list-style: none;

其他:在量一个盒子的时候,有时候很难直接量盒子内容的大小,更多的是直接量整个盒子的大小,后期添加padding的时候需要在weight的基础上减去padding值,如果一个盒子没有weight,通过继承得到的宽度,这个盒子在添加padding的时候浏览器会自动减去padding值,不会撑大当前盒子.


一、css三大特性
1,继承
    跟文字相关的属性可继承,高度不继承
    a标签自身有特定的样式,不能通过继承,所以需要单独设置,    比如color text-decoration
   


2,层叠性
   权重相同,后渲染的出效果



3,优先级

    继承 < 通配符 < 标签选择器 < id选择器 <行内 < ! important 
      注意:important值只对单条属性起效果,    而不是整个选择器;且继承过来的important没有作用
    
    权重
        继承或者* 的贡献值          0,0,0,0
        每个元素（标签）贡献值      0,0,0,1
        每个类，伪类贡献值          0,0,1,0
        每个ID贡献值                 0,1,0,0
        每个行内样式贡献值          1,0,0,0
        每个!important贡献值        正无穷
    
    权重可叠加,但不会进位  



二、内盒模型width & height+padding+border
    外盒模型width & height+padding+border+margin
1,width & height:宽高,即内容

2,padding:内边距
  语法:padding:值
  (1)1个值     上下左右
  (2)2个值     上下,左右
  (3)3个值     上,左右,下
  (4)4个值     上开始顺时针
  单独写语法:padding-方位:值
  注意:1)行内元素写左右padding,不要写上下padding.一般控制文字的上下用line-height
       2)块元素宽度的继承,继承的是width的大小
       3)行高是撑不开行内元素的
  前期写的时候,把盒子的高写上,方便自己看得到盒子的位置,后期要把高度删掉,容错率会更高.

3,border:边框
  1)border-color边框颜色
  2)border-width边框大小
  3)border-style边框样式
        值:solid实线
           dashed虚线
           dotted点线
           double双实线
  4)简写
        四条边框:border:大小 样式     颜色;控制上下左右四条边框
        单独边框:border-方位:值;top,bottom,left,    right.
  5)边框圆角border-radius
        1个值:(1)像素         值越大,越圆.
               (2)百分比           参照当前盒子完整的宽和高
        2个值:左上开始对角线,右上左下(对角线)
        注意:边框圆角并不依赖于边框
        3个值:左上,对角线,右下
        4个值:从左上开始顺时针
    胶囊型,圆形,口袋形,哆啦A梦测试(了解),
  6)不要某一条线
  border-方位:none;


  细线表格:border-collapse:collapse;添加在table上
    eg: table {
        	border:1px solid #ccc;
        	border-collapse:collapse;(合并细线表格)
        
        }
        td {
        	border:1px solid #ccc;
        }
    transparent透明


4,margin:外边距(和padding基本一致)
语法:margin:值
  (1)1个值     上下左右
  (2)2个值     上下,左右
  (3)3个值     上,左右,下
  (4)4个值     上开始顺时针
  单独写语法:margin-方位:值
注意:1)行内元素写左右margin,不要写上下margin.
     2)margin:0 auto;(上下为0,左右自动)使有宽度的块元素盒子水平居中)垂直目前auto做不到
       text-align:控制块盒子内部的文本或者行内块水平居中




三、清除内外边距
    body,p,h1-6等标签,系统默认有padding和margin,为了更好的布局,一开始会利用通配符清除浏览器和常用标签的内外边距.
    * {
    	padding:0;
    	margin:0;
    }
    





四、外边距的bug
    1,相邻块元素垂直外边距的合并
    现象: 当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom,
    下面的元素有上外边距margin-top,则他们之间的垂直间距不是margin-bottom与margin-top之和
    而是两者中的较大者;这种现象被称为相邻块元素垂直外边距的合并(也称外边距塌陷);
    上下两个盒子的,左右没有此现象(已亲测)


    2,嵌套块元素的  
    对于两个嵌套关系的块元素，如果父元素没有上内边距及边框，则父元素的上外边距会与子元素的上外边距发生合并，
    合并后的外边距为两者中的较大者，
    即使父元素的上外边距为0，也会发生合并。
    解决方法:1)不要给子元素margin-top,给父元素padding-top
    		     2)可以为父元素定义1px的上边框或1px的上padding
    		     3)overflow:hidden
    
五:其他
做一个盒子,里面有字,左边离文字15px的
解法:1)给文字text-indent:15px;
     2)给文字加padding-left,大盒子减去15px;
     3)把weight的宽度设给父盒子,让子盒子继承父盒子的宽度,把padding-left设置给子盒子.
    












