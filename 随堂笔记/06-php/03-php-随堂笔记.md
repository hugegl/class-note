--------------------------------------今日内容----------------------------
一,学生管理系统案例
功能需求:添加,渲染,删除
功能思考:
    1)关闭页面,重新打开,添加的数据还在,说明了数据持久化(file_put/get-contents)
    2)每个学生收集到信息后,都应该是个关联数组
    3)存在本地的应该是二维数组,是多个学生(复杂数据类型)
    4)数组存到本地需要转成json字符串(json_encode/decode)
功能实现:
1,添加功能:
    1)前端输入接班表单信息和文件进行提交
    2)后台接收处理前端提交的信息(基本表单($_POST),文件表单($_FILES))文件信息;文件信息,需要转存文件,收集的是文件的信息??????
    3)先从本地读取学生信息数据,json字符串
    4)将json字符串转成数组,得到二维学生数组,已有的学生
    5)向数组中进行追加学生数据
    6)将学生数据转成??????
2,功能思考????????
二,http协议
定义:http协议即超文本传输协议,是一个浏览器端和服务器端请求和响应的标准
1,请求(request)报文:
    get:
        1)请求行
          请求方式+请求地址+参数+协议
          参数的固定格式:01-form-get.php?username=pp&password=123
          参数在?后面拼接;
          键值对通过=拼接;
          多个键值对之间用&分隔;
        2)请求头
          主机地址+允许通过https进行请求+浏览器对应的版本号,系统信息
          +接收的类型+发出请求的地址+可以接收的文件类型+可以接收的语言格式+建立连接
        3)请求主体;如不设置,默认进行get请求
          请求主体是用来传输数据的,get请求的数据已经在地址栏了,所以,get请求没有请求主体
    post: 
        1)请求行
          请求方式+请求地址+协议
        2)请求头
          主机地址+请求体内容的长度+禁用缓存+响应的域名地址+允许使用https协议
          +请求体内容的格式+浏览器对应的版本号,系统信息+可以接收的类型+发送请求的地址
          +可以接收的类型+可以接收的语言格式+建立连接
        3)请求主体
          post的请求参数在请求体中
    get与post的区别:
        1)get请求没有请求体,参数在地址栏进行传输
        2)post请求有请求体,请求参数在请求体中,在post请求中需要设置请求体的内容格式
2,响应(reponse)报文:
post和get一样:
    1)状态行(响应行)
      协议+协议版本号+状态码+状态文本
      状态码:状态文本,表示当前响应是否成功
            200响应成功
            302重定向;重新指定跳转的地址
            404丢失页面
            500服务器错误;5系列开头的都表示服务器错误
    2)响应头
      响应的时间,默认按零时区+服务器相关的版本信息+使用的php版本+响应体的内容长度
      +连接超时时间+返回的内容类型+建立连接
    3)响应主体
引申:
    1)可以用抓包软件抓包,查看请求报文与响应报文
    2)使用chrome,打开控制台,network,点击headers
    General:请求信息概览
    response headers:响应信息
三, mysql数据库
概念:专门用于存储管理数据的仓库,英文:database,DB;
关系型数据库:
    基于表,以表格的方式存储数据的;表与表之间存在关系,将来可以根据表的关系进行多表查询;代表mysql,SQL,Server,Oracle;
非关系数据库:
    基于键值对的存储方式,执行效率较高,数据之间没有耦合性,不适用于特别复杂的存储操作;代表mongodlb;
四,数据库的框架结构
一个数据库可以有多个表
      数据表:用来存储数据的表
      记录-行:表中的一行,就是一条记录
      字段-列:字段是比记录更小的单位(类似单元格),多个字段集合组成记录,即数据项
      注意:一个数据库可以有多个数据表,1个表可以有多条记录,一条记录可以有多个字段
五,SQL语言
    相当于是客户端发送的命令(与服务器进行交互),我们用SQL语句操作数据库
    文件后缀   .sql 
六,数据库与数据库的关系
    navicat:数据库可视化操作工具,只是用来方便我们操作数据库的可视化工具
    字段类型:
        1)整型:int整数类型,用于存储年龄,学号,数量,产品编号等
        2)小数:
        float: 普通小数,可能会丢失精度,产品重量....
        decimal:精确存储,一般用于存储金钱
        3)字符串:
        varchar(M):  M表示分配的空间，单位字节,最大存储M个字节;一般用于存储不定长度的字符串,如姓名
        char(M):一般用于存储固定长度的字符串,如11位手机号;效率更高一点
        text:不用指定长度一般用于存储文章段落
        4)日期:
        date,time(),用来存年月日时分秒
    字段约束:
        对于字段要求的规则
        1)not null 不能为空
        2)defalut 可以给字段设定默认值
        3)primary key 主键,唯一标识,不能重复,不能为空
        4)auto_increment 自动增长,当添加一条数据的时候,它会自动增长,必须是整型(int),一般配合主键使用
        5)unique key 不能重复 
注意:指定默认值时,如果是字符串,需要'',放入内容
七:sql语句 增删改查
大小写都支持
``反引号的意义:防止跟关键字冲突,一般用来把表头``栝起来
注释:  -- 表示注释(--空格)
结尾:要加封号;
查: select * from 表格名称
     查询表中的所有信息,*是通配,所有的意思
    select 字段列表 from 表格名称 
    eg : select age,id from stu   查出stu列表中字段为的age和id的列表
    select * from where 条件
增:insert into 表格名称(字段1,字段2,字段3...) values(字段值,值1,值2...)
    字段列表:字段1,字段2,字段3...;
    值列表:值1,值2,值3...
删: delete from 表格名称  会将表中的所有信息全部删除(慎用)
    delete from 表格名称 where 条件;
    条件:
        1)id = 需要删除的行id值;
        2)字段的要求   eg:  age > 80 删除年纪大于80的列表
改:update 表格名称 set 字段1 = 值1,字段2 = 值2 where 条件;
      如果不写where条件,会对所有的内容执行修改的操作;
      条件与删除的条件写法相同








知识点:
1,array_push(数组名,追加的项);
2,数组名[] = 追加的项;     类似于js中的push
3,页面跳转语法
header('location:路径地址');
4,删除数组中的项
array_splice(数组名,开始下标,删除的数量,替换的内容/数组)
特点:
    1)会改变原数组,返回值是删除的项;
    2)如果省略删除的数量;则删除后面的所有内容;
       如果删除的数量是负值,则一直删到负的这个数量位置
    3)开始下标,如果是负的值,则是倒数第几个开始删




