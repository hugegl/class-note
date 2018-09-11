主讲html5和css3
一,背景系列
	1,多重背景(背景放多张图片,用,隔开)
		1)background:url(路径) 0 0 no-repeat,url(路径) 0 0 no-repeat;
多重背景时,如果有颜色要求,颜色应写在最后面的一组图片上.
	2,背景图片基准点(起始点,默认值除了边框开始的pandding的起始点)
		1)属性:background-origin
		 (1)值padding-box;     默认值,从padding起始点开始
		 (2)值content-box;      从内容的起始点开始
		 (3)值border-box;       从边框的起始点开始,边框会盖在背景图上面.
	3,背景缩放
		1)属性backgound-size
		 (1)值:1个值像素       宽,会等比缩放
		       2个值           单独缩放
		 (2)值:百分比          参照的是当前盒子的大小
		 (3)值:contain         自动缩放,和盒子的宽或者高保持一致.哪个先碰到盒子的边框,就停止整体缩放,留白.
		 (4)值:cover           等比缩放,撑满盒子,会自动裁切.
		 	让盒子里的图片自动随屏幕缩放技巧:eg:    width:50%             继承父级宽度50%
		 											padding-top:50%;      与父级padding值相距50%(视觉效果为高度50%)



二,盒子阴影
属性:box-shadow
值:1)水平偏移/x轴偏移    			取值像素,可以是负值
   2)垂直偏移/y轴偏移    			取值像素,可以是负值
   3)模糊程度/羽化程度   			取值像素
   4)阴影的尺寸大小(扩展半径)     	取值像素,会向外扩张此值
   5)颜色                			默认是黑色,和所有颜色取值一样
   6)内外阴影            			默认是外阴影(outset)不要写,写了会语法错误;内阴影(inset). 




三,文字阴影
属性:text-shadow
值:类似盒子
值:1)水平偏移/x轴偏移    取值像素,可以是负值
   2)垂直偏移/y轴偏移    取值像素,可以是负值
   3)模糊程度/羽化程度   取值像素
   4)颜色                默认是黑色,和所有颜色取值一样


阴影可以写多个,中间用,隔开.
阴影简写:水平偏移 垂直偏移 模糊程度 阴影大小 颜色 内外阴影.





四,内减盒子模型
属性:box-sizing控制盒子模型内减
  值:1)border-box        		自动内减去padding和border,botton,submint,test等等几个(天生就是自动内减)
     2)content-box默认值 		手动内减



五,过渡系列   本身不是动画,是控制某一个属性值变化到另一个值得过程
属性:transition   那个元素需要过渡,就写在谁身上
  值:1,过渡的属性
  	 2,过渡的时间(s/ms)
  	 3,过渡的曲线(加速,减速,先快后慢,先慢后快)可以打开开发者工具调,调好后,把属性值复制下来即可.
  	 	1)默认值ease
  	 	2)ease-out
  	 	3)ease-in
  	 	4)ease-in-out
  	 	5)linear   匀速
  	4,过渡的延迟时间(默认0s)
简写:用,隔开;
后者:过渡属性写all    但是会增加加载的负荷



旋转属性:transform:rotate(360deg)  360度旋转.
盒子透明:opacity:0;   取值1不透明,0透明,中间递减.

六,2D转换   transform
移动
	1,属性:transform:translate(值);
			translate移动(默认X)   移动至什么什么位置.
			translateX水平移动
	       translateY垂直移动
	       移动方向类似于相对定位,relateve;
	    值:1)像素,一个值为X移动;2个值为X和Y值.
	       2)百分比,参考值是自身的宽和高.可以有负值.
旋转,行内元素不行,块级和行内块可以.
	2,属性:transform:rotate(值deg);
	    值:1)数字,deg指角度
	       2)
	3,属性:transform:origin(值);控制旋转中心点
	   		   值:1)方位名词
	   		      2)像素 10px 10px;      x轴和y轴走多少像素
	   		      3)百分比               具体参照的值自学!!!!
缩放
	4,属性:transform:scale(值)
		值:1)数字,或者带小数点的数字,倍数
		scaleX,scaleY(也可以x和y轴的缩放)



斜切
	5,属性:transform:skew(值deg)
		值:1)数字,deg指角度
		   2)transform:skewX(x轴斜切)默认值
		     transform:skewY(y轴斜切)



2D转换-总结:
transform:值
1)translate移动
	    水平,垂直  translateX   translateY   translate(x,y)    	百分比参照的是自身盒子的宽高,可以配合绝对定位实现水平垂直居中,	移动是移动至



2)rotate旋转
        沿着某个点旋转   这个点可以控制     transform-origin:控制中心点


3)scale缩放
		缩放的是倍数,没有单位,直接是数值,可以单个方向控制  scaleX   scaleY


4)skew斜切
		控制的是斜切的角度


其他补充
(1)多个2D效果共存

多个2D效果连写,中间用空格隔开(可以不用空格隔开,为了美观,一定不要用,!!!)
eg:transform:sacle(2) rotate(360deg);旋转并缩放

(2)当多个场景下面,有多个2D效果共存的时候,需要复制前面已经存在的2D效果

eg:
选择器 {transform:tranlate(-50%,-50%) rotate(0)}
选择器:hover{transform:tranlate(-50%,-50%) rotate(360deg)}
       在原来的的位置处旋转360度



	
