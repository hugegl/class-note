一,反馈问题
	1,定位的盒子,如果没有top和left,默认从当前位置开始为起始点;
		定位的关键点:
			基准点:  固定定位:浏览器窗口;绝对定位:有定位父元素;相对定位:自己;
			边偏移 :  left top bottom right
	2,box-sizing:值;  指定width和height属性是设置给盒子模式的哪个盒子(content-box和border-box)
	值:border-box;内减模式,布局更方便
		content-box;默认值;外加模式
二,复习
	1,布局基本原则:大盒子包着小盒子  a标签可以包一切,但是不能包自己;
	2,布局时,宽高的百分比是直接继承自父元素,如果父元素是行内,行内元素是没有宽高的,所以无法继承行内元素宽高,会向上级找行内块级或者行内块去继承;
		li>a>img    li:width:100%;img:width:100%;    img继承a的宽,a是行内元素,没有宽高,所以img会往上找到li,继承li的宽;
		ul>li>img     img能继承li的宽
	3,设计师给了设计稿是2倍或者3倍图,在使用进行压缩:background-size width
	4,视口:移动端虚拟的布局区域,在写移动页面前,要将视口调整为当前设备的宽度
		<meta  name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no,minimum-scale=1.0,maximum-scale=1.0">
	5,less:
		变量  @变量名
		混入
		函数
		嵌套
		导入
		计算
	6,京东
		css初始:
		-webkit-tap-highlight-color:transparent;
		-webkit-appearance:none;
		box-sizing:border-box;
	7,流式布局:百分比布局,宽度自适应,高度固定;
		圣杯布局:中间的盒子width:100%;
				父盒子:设置padding值
				左右盒子:定位;
三,京东案例
	1,em 是一个字的大小
	rem 是rootem,就是html标签的字体大小;
	2,获取页面卷曲的距离
		window.pageYOffset
	3,处理对webkit的兼容;
		css3中需要添加webkit的前缀;
		css中用 -webkit-transform
		js中用驼峰命名法:   webkitTransform
	4,移动端不推荐使用1.1;2.4版本的jQuery;
		大量代码用来处理IE678的兼容问题,在移动端引入后会出现代码冗余;
		解决办法:1)用原生js;2)用移动端的插件  zepto.js;
	5,过渡的时间一定要小于定时器的间隔时间,否则transitionend事件触发不了;
	6,touch事件组
		touchstart:手指放上触发
		touchend:手指离开触发
		touchmove:手指移动触发
		touchcancel:系统取消touch事件的时候触发,比如电话,短信等;
	事件对象中有 伪数组;用电脑模拟数组长度是1;只有一个触摸点,用真机检测看触摸的手机出发点;
			changedTouches; 	记录触屏状态改变时的数据;touchend可以获取
			targetTouches;  只记录目标元素上触点的数据;touchend无法获取;项目中使用较多
			touches;  记录当前屏幕上所有触点的数据;touchend无法获取
			这些伪数组中:radiusX/Y是触发点半径大小;
			pageX相对于页面
			clientX相对于可视区
			screenX相对于屏幕坐标值




























