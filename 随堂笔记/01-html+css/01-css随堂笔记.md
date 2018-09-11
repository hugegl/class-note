音频插入
字符集


css的概念及作用     层叠样式表



    基本语法:style标签内(约定放在head内)
    
    style标签就是css的运行环境,    这对标签可以放在任何位置,约定放在head标签里
    
            书写格式:
                选择器 {
                	属性名:属性值;
                	属性名:属性值;
                	属性名:属性值;
                	...
                }
    


    字体属性:1,font-size文字大小
               取值:px    大部分数值要带单位px(像素)
               eg:font-size:100px;
             2,font-weight字体粗细
               取值:normal 不加粗(400),
                    bold加粗(700),
                    bolder更粗(了解),
                    100-900,
			      eg:font-weight:bold;
			 3,font-style字体倾斜
			   取值:nomarl 正常,
			        italic 倾斜,
			 4,font-family字体的类型,默认微软雅黑
			   取值:"Microsoft yahe"微软雅黑
			        "NSimsun"新宋体
			        中文字体需加引号,英文不用,如果英文字体有空格或特殊符号也需引号.
			    字体可以设置多个,中间逗号隔开,浏览器的解析原则从左至右从上至下,先识别出来的先显示,后续不管,如不识别就识别下一个,如果都不识别就用默认字体.不建议使用偏门字体.
			5,字体简写:
			顺序:style,weight,size/line-height,family(稍微舒服)用空格隔开
			原则:size和family一定要,不能不写,size/行高,有的话也可以这样简写,(不写就默认和字体一样大小,会覆盖前面设置的行高!!!!需注意)
			eg:font:italic bold 200px "microsoft yahe";
	开发者工具(重点)
	 调试代码,检测代码

    标签选择器:
	        标签选择器:通过标签名选中对应的元素
	                优:会选中所有满足条件都选中
	                缺:无法实现差异化选择
	        

	        (最常用90%)类选择器(class与.):英文,不可以纯数字和中文
	        类选择器,可以实现差异化选择一次申明多次调用
	                        1,申明   类选择器.eg:box{...}
							

							2,调用   类选择器eg
							:class="box"
							

							多类名选择器
							两个相同的标签,有一些共同的样式,也有一些差异化的样式
							一个元素可以调用多个类名,类名与类名之间用空格隔开
							这种选择方式方便后期维护
							eg
							:class="red box box2"


			(一般配合js使用)id选择器(id与#):
			同一个页面同一个id一次申明,一次调用
			            1,申明      id选择器
			            2,调用      id选择器


			通配符选择器(*):通通匹配的选择器,选中所有元素,效率较低,一般用于初始化



			伪类选择器:
			书写方式
			选择器:hover/active
			a就是个元素,hover/active可以用在其他元素上.
			          1,a:link       链接没有被访问的效果
			          2,a:visited    链接访问过后的效果
			          3,a:hover      鼠标移上之后的状态
			          hover这个属性可以给其他选择器 使用
			          4,a:active     鼠标按住不放时候的效果



			          简写方式:
			          a{随便什么效果}
			          a:hover {移上之后的}



	文字格式:
	    文字装饰属性:text-decoration
	                 值:1,underline     下划线
	                    2,line-through  删除线
	                    3,none          文字默认状态
	    首行缩进属性:text-indent
	                值:30px(缩进30像素)
	                   2em(相对单位,相对于当前的文字大小,2个文字的大小)
	    对齐方式属性:text-align,控制文字在元素内部水平居中,需匹配块级元素使用
	    			值:center,left,right



	行高:
	属性:line-height
	  值:1,100px(100像素,包含文字和间隙,真正的所处的位置为减去文字的大小,文字上、下各渲染剩下的一半,所以一般从文字的顶线量到下一行文字的顶线)
		 2,倍数 
		 eg:line-height:1.5;(当前文字的1.5倍)

	  小技巧:让单行文本在元素内垂直居中:让行高和容器的高度保持一致
	  


	颜色:
	属性:color
	  值:1,英文
	     2,十六进制
	     3,rgb(0,0,0)(red,green,blue的不同取值)
	     4,rgba(0,0,0,0)(red,green,blue,透明度)透明度0-1,0全透明,1代表不透明)


	注释:
	/*注释内容*/,快捷键:ctrl+/











<!-- <!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		div {
			color: gold;
			font-size: 100px;
			font-family: "microsoft yahe"
		}
        div .honer {
        	color: red;
        	font-size: 50px;

        }
        span {
        	font:italic bold 200px "microsoft yahe";
        	color: skyblue;
        }


	</style>
</head>
<body>
	<div>你好你好</div>
	<span>小达达</span>
</body>
</html>
     -->

