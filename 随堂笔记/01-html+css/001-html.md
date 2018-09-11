<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>课堂随记-表单</title>
</head>
<!-- 表单组成:
        表单域:form
              表单域作用:收集"内部"的所有表单的信息,整体提交给后台,配合submit按钮,需添加上name属性,才能将表单的内容提交出去.
            属性action(信息提交的后台地址)
        提示文本:文字
        表单:input(单标签)
                 属性:type
                    值text(单行文本输入框)
                    值password(密码输入框)
                    值name(提交给后台时显示的值,需都写上,后台提交数据时才能都提交上)
                    值radio(单选框),要想单选框生效,必须具备相同的name属性,(name="内容一致")
                    值checkbox(多选框) 
                    值file(上传文件)
                    值button(普通按钮),与value共同使用,可将值赋予在按钮上
                    值submit(提交)
                    值reset(重置)
                    值value(值),在选择性的部位均需加上value;在文本输入的地方可写可不写
                    值date(日期)
                    值range(滑块)

                    
    
    
                属性checked(默认选择项)checked="checked",如果属性值一样,只要输入属性名字即可.eg:checked="checked",checked,checked,checked
                    
                 属性:placeholder(占位符)值"显示什么文字输入什么"
            textarea(多行文本输入框/文本域)
                eg:<textarea>内容</textarea>
            button(按钮)
                eg:<button>随便什么按钮</button>
            select/option(下拉框)   option属性:selected(默认选中项),需写在option标签内
             eg:<select>
			             <option value="北京">北京</option>
			             <option value="天津">天津</option>
		           </select>
		    label(将文字和表单关联起来,点击文字相当于点击表单)实现点击文字达到选择按钮的目的,直接用label标签把需要达到效果的所有标签包起来


         
 -->
<body>
	<form action="02day-课堂随记-表单.html">
		用户名:<input type="text" placeholder="请输入用户名" value="用户名">
		<br>
		密　码:<input type="password" value="密码">
		<br>
		性  别:<input type="radio" name="gender" value="性别">男	<input type="radio" name="gender" checked="checked" value="女">女<input type="radio" name="gender" value="保密">保密
        <br>           
		爱　好:<input type="checkbox" value="爬山" checked>爬山<input type="checkbox" value="玩">玩<input type="checkbox" value="出去"checked>出去
		<br>  
		上传文件:<input type="file">
		<br>  
		自我介绍:<textarea>这个人很懒什么也没有留下</textarea>
		<br>
		省份:
		<select>
			<option value="北京">北京</option>
			<option value="天津">天津</option>
			<option  selected value="武汉">武汉</option>
			<option value="云南">云南</option>
		</select>
		<!-- value表单里面包含的内容,button普通按钮 --> 
		<input type="button" value="按钮想什么写什么">
		<br>
		<button>按钮</button>
		<br>
		<br>
		日期:<input type="date">
		<br>
		滑块:<input type="range">

		<br>提交<input type="submit">
		<br>重置<input type="reset">














	</form>
</body>
</html>
梳理:
表单:表单域,表单,提示文本


表单域:收集表单域内部的表单信息提交给后台
action属性:提交的后台地址
配合submit提交按钮
表单想要被提交需要name属性

提示文本:提示用户输入


表单:


input分类:
     text单行文本框
     password密码
     radio单选
     checkbox复选框
     file上传控件
     submit提交按钮
     button普通按钮
button 默认类型是submit,有兼容问题

select下拉框,配合option

textarea多行文本输入框/文本域




表单属性:

value 表单内部包含的值
name  表单的名字,配合form提交信息
checked 默认选中项,针对radio和checkbox
selected默认选中项,针对select,写在option内



label标签:将表单和文字关联起来,点击文字相当于点击表单.
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>额外知识</title>
</head>
<body>
	<!-- 容器标签/布局时用,无语义
          div一行只能用一个
          span一行可以多个
	 -->
	<div>装任意内容</div><div>装任意内容</div>
	<span>随便装什么</span><span>随便装什么</span><span>随便装什么</span><span>随便装什么</span>
     

    
    (牢记,默写) h5新增的6大结构标签(增加语义),使用方式与div一样,后期布局经常使用,兼容性 ie 6 7 8不支持,后期有方法
    详细请查阅文档,在线查阅:w3school
    离线,查看老师的离线文档
     <header>网站头部区域</header>
     <footer>网站底部区域</footer>
     <nav>导航</nav>
     <aside>侧边栏</aside>
     <article>文章页</article>
     <section>区块</section>



    (了解)h5新增表单属性
    placeholder占位文本,用来提示用户当前表单应该输入的内容,和value有本质不同,value时表单本身的值,会提交给后台,placeholder则不会


    autofocus自动获取焦点

    autocomplete="on"自动补全,可不写,默认值为on,off关闭该功能,前提该字段必须成功提交过一次


    required自动验证表单不能为空

   (熟记) <input placeholder="占位文本">
    <input autofocus>
    <input autocomplete="on">
    <input required="required">自动验证表单不能为空




    (了解)h5新增表单

    <input type="range">滑块
    <input type="date">日期,日期表单在手机端可以使用,可以唤醒手机自带的控件
    <input type="number">手机端唤醒数字键盘
    <input type="color">颜色
    <input>




</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>视频\音频</title>
</head>
<body>
     音频使用和视频文件基本一致.
     视频

        一、借助第三方网站播放
            1,上传视频至第三方网站
            2,点击分享,复制通用代码/html代码
            3,直接粘贴到html内
          优点:兼容性高
          缺点:广告
        二、h5新增的播放视频   使用场景:手机端
            标签:video播放视频
            属性:src路径
                 autoplay自动播放
                 controls播放控件
                 loop循环播放
            <video src="视频路径" autoplay     controls    loop></video>
          优点:方便,无广告
          缺点:兼容性
        格式:mp4,ogg,webm
        兼容写法:(需准备三种不同格式的视频)
         video+source配合使用
                从上至下查找,如果找到能识别的,        如果不识别,继续往下查找,        知道找到自己识别的那一个,如果都不识别,最终会将a标签识别出来.
        <video autoplay loop controls>
        	<source src="路径.mp4">
        	<source src="路径.ogg">
        	<source src="路径.webm">
        	<a href="http:www.baidu.com">你的浏览器太低端了,赶紧升级吧</a>
        	<input type="text">
        </video>
       




	
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>02day-课堂随记</title>
</head>
<body>
    <!-- 表格组成:
            table
            tr
            td
                快捷键删除行:光标移动到表格中间,ctrl+X删除此单元格
            表头标签:th(增加语义性)可替代td
            表格头部部分:thead(加强语义)
            表格身体部分:tbody(加强语义)
        属性:  border:表格边框线
           cellspacing:单元格与单元格间距
           cellpadding:内容与单元格的间距(上下左右均有)
           width:宽
           hight:高
           align:对齐方式(可加在table,tr,td标签内),值:left,right,center
           合并原则:1.左起向右,向下的顺序,写在第一个标签内;2.合并完后需要把被合并掉的单元格删除.
           rowspan:跨行合并,eg:roespan="3"(向下合并3个单元格)
           colspan:跨列合并,eg:colspan="5"(向右合并5个单元格)
        从属关系:table/tr/td,只有td可以包裹任意标签
        

     -->
	<table border="1" cellspacing="0" cellpadding="5" width="500" hight="10" align="center">
	<!-- 表格标题:caption实际工作中少用(了解即可)写在thead上面,渲染在表格头部 -->
	<caption>表格的标题</caption>
		<thead>
		    <tr align="center">
		    	<th>单元格1</th>
		    	<th>单元格2</th>
		    	<th>单元格3</th>
		    	<th>单元格4</th>
		    	<th>单元格5</th>
		    	<th>单元格6</th>
		    </tr>
		</thead>
		<tbody>
		    <tr>
		    	<!-- rowspan跨列合并 -->
		    	<td colspan="3">单元格1</td>
		    	<!-- rowspan跨行合并 -->
		    	<td rowspan="2">单元格5</td>
		    	<td>单元格6</td>
		    	<td>单元格7</td>
		    </tr>
		    <tr>
		    	<td>单元格1</td>
		    	<td>单元格2</td>
		    	<td>单元格3</td>
		    	<td>单元格6</td>
		    	<td>单元格7</td>
		    </tr>
		    <tr>
		    	<td>单元格1</td>
		    	<td>单元格2</td>
		    	<td>单元格3</td>
		    	<td>单元格5</td>
		    	<td>单元格6</td>
		    	<td>单元格7</td>
		    </tr>
		</tbody>
	</table>
</body>
</html>