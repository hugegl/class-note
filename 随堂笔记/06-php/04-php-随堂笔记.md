-----------------------------------复习-----------------------------------
一,sql语法:
基础查询:
增加:  insert into表名(字段1,字段2...)values(值1,值2...)
        insert into表名values(值1,值2...);值和字段必须一一对应;
删除:delete from表名   删除表格中所有的数据;delete from 表名 where 条件;
修改:update 表名 set字段1=值1,字段2=值2....,修改表格中所有记录;update 表名 set字段1=值1,字段2=值2.... where 条件;
查询:select*from表名  查询所有;select 字段1,字段2...from 表名 where 条件
-----------------------------------今日内容-----------------------------------
二,高级查询
1,where 条件
    1)=等于  eg: select *from stu where id = 10;
    2)>大于
    3)<小于
    4)>=大于等于
    5)<=小于等于
    6)and 和,并且; 要满足多种条件的时候,用and连接
    7)or   或者;要满足某一个条件时,用or连接;
2,模糊查询  like
  语法结构:  where 条件 like '值%'; 
  eg: where name like '李%'  找出李开头的名字;
3,in 语法
  语法结构:  where 字段 in (值1,值2,值3);
  eg : delete where id in (1,3);删除id 是1和3的行;
4,count()  统计条目
  语法结构:   select count(*) as total from 表名 where 条件
  eg:select count(*) as total from stu;查询stu一共有多少条目,total是一个变量名字,方便输出,获取
5,排序   order by
  语法结构:   order by 字段1   默认是升序排列;order by 字段2  desc 降序排列
  eg:   select  * from stu order by age  按照年纪升序排列;
6,对结果集截取   limit
  语法结构:  limit 起始索引,截取长度
  应用场景:1) 找 top  10 ;  limit 0,10;
          2)分页  查学生表,每页显示10条  第一页: select * from stu limit 0,10;
                                      第二页:select * from stu limit 10,10;
                                      第三页:select * from stu limit 20,10;
                                      第n页:select * from stu limit 10*(n-1),10;
  eg: select * from stu order by age desc limit
7,联合查询
1)主键和外键
  主键:当前表中的唯一标识,不能为空,不能重复
  外键:是其他表中的主键,通过外键可以建立表与表之间的关系,可以进行多表联合查询;
2)select 表名1.字段1,表名2.字段2... from 表1 join 表2 on 表1.字段1 = 表2.字段1 where 表1.条件;
注意: (1)想显示什么就在select后面写什么; 
      (2)在写字段的时候,最好写表名.字段,不然如果两个表的字段是一样的,就不知道查询的是哪一个表中的字段;如果字段是唯一的,可以直接写;
      (3)表1 join 表2 on 表1.字段1 = 表2.字段;表示表1和表2 是通过什么字段关联起来的;
  eg : select teacher.*,class.classname,class.total from teacher join class on teacher.classid = where teacher.id =1;
  例子解析:
        select teacher.*,class.classname,class.total from teacher  查询的字段
        join class on teacher.classid = class.id  联合条件
        where teacher.id =1; 查询条件
三,通过php操作数据库
步骤: 1)连接数据库(主机地址,端口号,用户名,密码)
      2)准备sql语句
      3)执行sql语句
      4)分析sql执行的结果
      5)关闭连接
1,连接数据库 
  @ mysqli_connect('ip地址','用户名','密码','数据库名',端口号(默认3306))
  细节: @ 错误抑制符,可以抑制错误的输出;
  返回值:连接成功,返回一个连接对象;连接失败,返回false;
 eg: mysqli_connect('127.0.0.1','root','root','test01',3306)
2,准备sql语句
(增删改)非查询语句
 $ 变量 = delete from stu where条件;//准备sql语句
 引申:  1)连接对象:连接数据库成功后返回的连接对象;
        2) 执行非查询语句(增删改),返回值:true/false;
        3)die('内容'),结束当前程序的运行,并输出一句话;//如果写在php中,那本就结束php程序,不会执行php后面的代码;
        4)sql语句一般用"",会解析变量,方便动态修改条件;
        5)写sql语句,由于sal语句里面可能会有字符串,且双引号会对变量进行解析,所以编写sql规则是外双内单;
        6)如果是变量,变量中存的也是字符串,那么在拼接字符串的时候,在变量外面也要用''包裹
查询语句
查询语句的返回值:查询成功,返回结果集;查询失败,返回false;
查询成功,返回结果集,通过下面的方式取出数据;
mysqli_fetch_assor(结果集),返回的是关联数组,一次只返回一条;
有数据,返回的是关联数组;没有数据,返回null;
查询结果集中有多少条数据 mysqli_num_rows(结果集);
eg:  
//定义一个空数组,接收返回的数组
$arr = [];
    while ( $row = mysqli_fetch_assoc($res) ) {
      //如果mysqli_fetch_assoc($res)如果有数据就返回数据,每次只返回一条关联数组;那么while判断条件就是true,执行循环体;
      //如果没有数据就返回null,则不符合while循环条件,null就是false;
      $arr[] = $row;
    }

3,执行sql 
mysqli_querry(连接对象,sql语句)
4,分析结果,
返回值true/false;
    1)如果返回false,可以输出错误信息:
    mysqli_error(连接对象);返回错误信息;输出需要echo;
    2)查询成功时,从结果集中取数据,以关联数组的形式返回,一次只返回一条数据,所以要用空数组接收
    mysqli_fetch_assoc(执行查询结果后的返回对象);从结果集中取数据,一次返回一条;
5,关闭连接
mysqli_close(连接对象);
四,将方法封装成函数
define('常量名','常量值');定义ip地址,用户名,密码,数据库名称,端口号的常量;
1,非查询语句
        function 函数名(形参){
        变量名 = mysqli_connect(登录用的常量名);
        if(!变量名){
          echo '失败';
          return false;
        }
        变量名2 = mysqli_query(变量名,形参);
        if(变量名2){
          mysqli_close(变量名);
          return true;
        }else{
          echo mysqli_error(变量名);
          mysqli_close(变量名);
          return false;
        }
        }
2,查询语句 
function my_querry(){
  变量名 = mysqli_connect(登录用的常量名);
  if(!变量名){
    echo '失败';
    return false;
  }
  变量名2 = mysqli_query(变量名,形参);
  if(!变量名2){
    echo mysqli_error(变量名);
    mysqli_close(变量名);
    return false;
  }
  变量名3 =[];
  while(变量名4 = mysqli_fetch_assoc(变量名2)){
    变量名3[] = 变量名4;
  }
  mysqli_close(变量名3);
  return true;
}
五,学生管理系统2.0版;   主要是把数据保存在数据库,而不是txt文件内;







总结:
sql语句常用方法汇总:
1)mysqli_connect(IP地址,用户名,密码,数据库名称,端口号); 
      建立连接,成功返回连接对象;失败返回false;
2)mysqli_query(连接对象,sql语句);   
      执行sql语句,非查询语句(增删改)返回true/false;
                  查询语句,成功返回结果集;失败返回false;
3)mysqli_num_rows(结果集);  查询结果集多少条数据;
4)mysqli_fetch_assoc(结果集);  
    作用:从结果集中取数据,每次取一条,以关联数组的形式返回;
    返回值:如果取到了,返回关联数组;如果没取到,返回null;
5)mysqli_error(连接对象); 返回错误信息;
6)mysqli_close(连接对象);关闭连接;

双击ctrl+d向后选中相同的内容

