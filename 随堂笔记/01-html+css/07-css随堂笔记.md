一、自己制作font小图标
1,设计师做好小图标,导出svg的格式
2,小云图标,多色和单色看图标的情况而定.
3,添加到我的项目,就可以多次下载在一个文件里面.
4,在线链接,可以不用下载,直接在线使用.


二、小效果细节补充
1,滑动门(三个浮动盒子,中间平铺)
2,鼠标悬停样式cursor
  1)值:pointer   		小手
       default   		箭头
       move      		拖拽
       text      		文本
       url(路径),       链接图片加载失败后的替换样式
3,外边框input的   outline
	1)值one          去掉选中之后的蓝边框
4,去掉textarea的自动缩放
	1)resize:none


三、品优购
1,文件夹:css,images,upload,fonts,js,
2,css文件分类:
	(1)normallize.css样式初始化css文件,将各大浏览器之间的样式全部统一
	(2)common.css  公共样式文件,页面的头部和尾部一样
3,link引入三个css文件(前面两个,还有自己样式的css文件)顺序不能乱,先初始化,再公共样式,最后是自己的样式.(权重一样,后渲染的出效果)
4,ico小图标(类似淘宝title里面的小图标)
   1)选中自己要的png文件,在线制作ico小图标,比特虫
   2)登录对应的网站（http://www.bitbug.net/） 将图标上传上去即可得到ico图标
   3)使用代码  <link rel="shortcut icon" href=" /favicon.ico" />  （注意路径：建议将ico图标放到根目录下面）


5,SEO搜索引擎优化
   1)title
   是搜索引擎的入口,可以把最重要的写进去(长度:谷歌35个中文,百度28个中文),可增减
   2)description
   针对网站的描述,是标题的补充,不超过120个字,作用次之
   值:
   <meta name="description" content="内容内容"/>
   3)keywords
   搜索引擎的关注点之一,6-8个关键词之间
   <meta name="keywords" content="内容内容"/>


6,logo处,给搜索引擎识别,增加权重和语义
需要写上h1品优购,font-size:0;(以前用text-indent:-9999px;)


7-1购物车处,不建议使用宽高,而是用padding撑开.
7-2不建议使用right定位,影响后期数字变动的美观,建议使用left.



8.1,定位的时候,以padding的点开始定位,不会包含边框,但是会包含padding.(即,padding对定位无效)
定位后,点击购物车,下面的定位会出来,但是购物车下边框和定位的子元素重叠的部分没有边框,没有边框的盒子用背景颜色hover的时候盖住.
8.2定位的细节:
脱标定位的元素,内容有多大就撑多大,如果内容很多,宽度不会超过相对定位的父级,会折行显示.
强制不换行(属性):white-space:nowrap;











四、




















五、
