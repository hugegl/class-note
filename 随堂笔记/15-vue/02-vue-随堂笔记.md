# 复习
## v-model
1. 双向数据绑定原理:使用了 Object.defineProperty() 方法
2. Object.defineProperty()方法,可以用于给对象添加更新属性
```js
let obj = {};
// Object.defineP/roperty(参数1,'参数2',{参数3})
    //参数1:需要添加的属性的对象,obj
    //参数2:需要加的属性,
    //参数3:配置项,
    Object.defineProperty(obj,'name',{
        get(){
            //get函数中,一定要return当前这个新天剑进去的属性作为返回值
            console.log('你当前获取到的值是',name);//相当于obj.name
            return name;
        },
        //setter函数,这个函数中包含一个参数,这个参数表示当前设置的这个属性的新的值,相当于obj.name = '新的值'
        set(newName){
            name = newName;//newName相当于'新的值'
        }
    })
```
模拟双向数据绑定,只有核心,并不完全是这样的
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <body>
    <div id="app">
        <input type="text" id
        ="myinput">
        <h1 id="myh"></h1>
    </div>
  </body>
    <script >
        let obj ={};
        Object.defineProperty(obj,'name',{
            get(){
                return name;
            },
            set(newName){
                name = newName;
                //将设置的新的值,展示到页面h标签
                document.getElemtById('myh').innerText = newName;
                //当手动修改obj里面的name属性时,要把改变后的值赋值给input框;
                document.getElemtById('myinput').value = newName;
            }
        })
        document.getElemtById('myinput').addEventListener('input',function(e){
            console.log(e.target.value);//e.target.value即当前input的值,注册input事件,有改变就获取;将及时获取的值,赋值给obj.name;就会触发defineProperty()方法
            obj.name = e.target.value;
        })
    </script>
  </body>
</html>
```



# 今日内容
## 操作DOM之ref与自定义指令
1. 在vue中 不推荐操作dom,但是提供了一个ref属性,可以用来获取页面中dom元素的引用
+ 方法1: ref 属性可以用来获取dom元素,ref的值可以随便定义
    - 定义的时候,不要和页面中其他的ref相同,如果一样,会被覆盖
    - 使用,写在标签的属性位置`ref="ref名"`
    - 获取`this.$refs.ref名`
+ 方法2:自定义指令
    - 增强html标签的功能
    - 全局方法`Vue.directive('自定义指令名称',{配置项})`
        + 自定义指令名称:去掉`v-`的名字;建议全部小写;如果用了驼峰命名法,那么在元素中使用的时候,需要用'-'将驼峰命名法的地方分开
        + 配置项:主要包含一些和自定义指令执行相关的函数
            - bind(el,binding){},自定义指令一绑定到dom上就自动执行,只执行一次
            - inserted(el,binding){},dom插入到页面中的时候就执行,只执行一次
            - update(el,binding){},自定义指令后面的值更新的时候自动执行
            - 上面这些函数的参数:
                1. el,使用这个指令的dom元素
                2. binding,记录自定义指令信息的对象;
                    + 这个对象里面有一个binding.value;它的值是`v-指令名称="变量"`中变量的值;可以传任意数据,如果是函数,那么可以执行这个函数`binding.value()`
                    + 这个对象里面有一个binding.arg;它的值是`v-指令名称:绑定的属性名="变量"`中被绑定的属性名
                    + 这个对象里面有一个binding.modifiers对象;它存储了`v-指令名称:绑定的属性名.修饰符="变量"`中修饰符;如果添加了修饰符,那么binding.modifiers对象中该修饰符的值就是true;
    - 使用的时候`v-指令名="data中的变量名"`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <body>
    <div id="app">
        <!-- 方法1 -->
        <!-- 1.1 ref 属性可以用来获取dom元素,ref的值可以随便定义-->
        <input type="text" v-model="newId"  ref="inputRef">
        <!-- 方法2 -->
        <input type="text" v-model="newId"  v-myfocus ="newId">
    </div>
  </body>
  <script src="./vue2.js"></script>
    <script >
        // 方法2   
        Vue.directive('myfocus',{
            inserted(el,binding){
                el.focus();
            }
        })
        let vm = new Vue({
            el:'#app',
            data:{
                newId:'';
            },
            mounted(){
                // 方法1
            //页面一加载就会执行这个函数
            //1.2 获取定义的ref,可以通过this.$refs.ref的名字   $refs是一个对象
            this.$refs.inputRef.focus();//获取元素,设定元素一加载页面后获取焦点
            }
        })
    </script>
  </body>
</html>
```
## 钩子函数
1. mounted 函数,页面一加载就执行


## 过滤器
1. 作用将源数据过滤成新的数据
2. Vue.filter('过滤器名字',函数);
  + 参数1:'过滤器名字' 
  + 参数2:函数,一个出来函数,这个函数默认有一个默认形参,这个形参就是需要过滤的数据,默认在形参1的位置;如果有需要传递的其他参数,就在调用的时候传递,在形参的第二个位置开始写;
  + 处理完成之后,必须要return一个数据
3. 使用过滤器,通过管道符连接`需要过滤的数据 | 过滤器名字(实参)`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <body>
    <div id="app">
      <p>{{oldname | myfilter('数据')}}</p>
    </div>
  </body>
  <script src="./vue2.js"></script>
    <script >
      // 1.创建全局过滤器
      Vue.filter('myfilter',function(source,userdata){
        //source默认的位置,默认传进来的是被过滤的数据,如果有其他参数,排在后面写;
        //userdata是用户传递来的数据   '数据'
        //对source数据进行处理,变成新的数据
        let str = source.split()
        return str;
      })
        let vm = new Vue({
            el:'#app',
            data:{
                newId:'';
            },
        })
    </script>
  </body>
</html>
```

## computed 计算属性
1. 插值表达式的计算属性不易太多,所以使用computed
2. 书写位置和data同级, computed是一个对象,里面放函数
3. 函数的名字自定义即可,这个函数的名字可以当做属性名来使用(即data中的属性名字)
4. 一定要有return返回值,返回的值会作为这个函数名字的值渲染到页面上
5. 不能将return写在异步函数内;

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <body>
    <div id="app">
      <!-- 示例 -->
      <input type="text" v-model="firstname">
      <input type="text" v-model="lastname">
      <h1>全名:{{fullname}}</h1>
      <!-- 模拟开发示例 -->
      <span>{{price}}</span>
      <span>{{count}}</span>
      <button @click="count = count+1">增加</button>
      <button  @click="count = count-1">减少</button>
      <p>总价:{{totalprice}}</p>
    </div>
  </body>
  <script src="./vue2.js"></script>
    <script >
      let vm = new Vue({
        el:'#app',
        data:{
          price:100,
          count:2
        },
        computed:{
          totalprice(){
            return this.price*this.count
          }
        }
      })
        // 示例
        // let vm = new Vue({
        //     el:'#app',
        //     data:{
        //         firstname:'';
        //         lastname:'';
        //     },
        //     computed:{
        //       //在computed里面写一个函数,这个函数的函数名将来可以作为一个属性来使用;必须要有返回值
        //       //计算属性是依赖于缓存的,当页面中调用同一个静态属性多次的时候,后面的计算属性的值,会直接从第一次得到的结果中去取,不会在执行一遍函数;
        //       //计算属性更高
        //       fullname(){
        //         return this.firstname +this.lastname
        //       }
        //     }
        // })
    </script>
  </body>
</html>
```


## watch 监听器
1. watch 监听器,会监听data中数据的变化,只要一变化,就能够执行相应的函数
2. 书写位置和data同级, watch,里面放函数
3. 函数的名字需要和data中监视的变量名字一样,监视哪个属性名,就用它的名字作为函数,在这个函数中,可以给data中定义一个新变量接收,将拼好的值赋值给这个变量,渲染到页面上;
4. 这个函数默认有两个形参,对应的是监听的数据的属性的值,第一个形参的位置是新值,第二个形参的位置是旧值;
5. 异步操作后要改变的属性的值,建议使用watch;
6. 监听data中的复杂数据类型,如对象,需要开启深度监听` 监听的属性名:{hander(newVal){函数体},deep:true,immediate:true}`
  + 监听的属性名是data中的属性;
  + hander是固定写法
  + newVal是形参,是一个对象,里面存放了当监听的对象中的属性值发生改变的值,只能接收新的值;无法接收旧的值
  + deep:true;深度监听,开启;
  + immediate:true;默认是数据变化之后触发,如果想页面一加载就执行,添加`immediate:true`即可;
```html
<!DOCTYPE html>
<html lang="en">
<head>
<title></title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<script src="./vue2.js"></script>
</head>
<body>
<div id="app">
  <!-- 示例 -->
  <input type="text" v-model="firstname">
  <input type="text" v-model="lastname">
  <h1>全名:{{fullname}}</h1>
</div>
</body>
<script src="./vue2.js"></script>
<script >
  let vm = new Vue({
    el:'#app',
    data:{
      firstname:'',
      lastname:'',
      fullname:'',
      user:{
        name:'pp',
        age:15,
      }
    },
    watch:{
      //监听的数据名放到这里作为函数名,一有
      //这里的函数有两个形参,一个是新值,一个是旧值
      firstname(newVal,oldVal){
        this.fullname = newVal+this.lastname;
      },
      lastname(newVal,oldVal){
        this.fullname =this.firstname + newVal;
      }
      //监听复杂数据类型的时候,不能像监听普通数据那样写;深度监听;
      // 获取不到旧的值;
      //函数的名字只能是hander
      user:{
        //只能获取到改变后的对象,无法获取原来的对象;
        hander(newVal,oldVal){//所以oldVal值和newVal值一样
          console.log(newVal);
          // console.log(oldVal)
        },
        deep:true;
      }
    }
  })
</script>
</body>
</html>
```

## vue-resource 和 axios 用来发送请求
### axios 的简单使用
  1. 引入axios文件`<script src="路径/axios.js"></script>`
  2. 不支持jsonp跨域请求,可以使用代理(后期讲,配合webpack),或者CORS;
```html
<!DOCTYPE html>
<html lang="en">
<head>
<title></title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<script src="./vue2.js"></script>
</head>
<body>
<div id="app">
</div>
</body>
<script src="./vue2.js"></script>
<script src="./axios.js"></script>
<script >
  let vm = new Vue({
    el:'#app',
    data:{
    },
    methods(){
      //axios支持promise之get请求1
      axios.get('http:请求路径?参数')
      .then(res=>{
        //res是一个对象,里面存储了响应回来的相关的内容
        console.log(res.data);
      })
      .cath(err=>{
        //捕获错误对象的
        console.log(err)
      })
      //axios支持promise之get请求2
      axios.get('/user', {
        params: {
          ID: 12345,
        }
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
      //axios支持promise之post请求
       axios.post('/user', {
          firstName: 'Fred',
          lastName: 'Flintstone'
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    }
  })
</script>
</body>
</html>
```

### vue-resource
1. 依赖于vue,需vue引入之后
2. 引入 vue-resource 文件`<script src="路径/vue-resource.js"></script>`
3. 成功引入之后,会在vue的原型上面绑定一个`$http对象`,这个对象中包含了vue-resource 所有的方法
2. 支持jsonp跨域请求
```html
<!DOCTYPE html>
<html lang="en">
<head>
<title></title>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<script src="./vue2.js"></script>
</head>
<body>
<div id="app">
</div>
</body>
<script src="./vue2.js"></script>
<script src="./vue-resource.js"></script>
<script >
  let vm = new Vue({
    el:'#app',
    data:{
    },
    mounted(){
      //get请求
      this.$http.get('请求路径')
      .then(res=>{
        //res响应的结果,数据包裹在body中
        res.body;//包含返回的数据
      },err=>{
        //err失败的对象
      })
      //jsonp请求
      this.$http.jsonp('请求路径')
      .then(res=>{
        //res响应的结果,数据包裹在body中
        res.body;//包含返回的数据
      },err=>{
        //err失败的对象
      })
    }
  })
</script>
</body>
</html>
```






# 引申
1. 给对象添加属性
+ 不能使用 `this.对象名.属性名='值'`这种方式,需要使用
+ Vue.set(参数1,参数2,参数3)方法
            - 参数1:{object | Array} target;表示需要设置的数组/对象
            - 参数2:{string | number} key;表示数组索引
            - 参数3:{any} value  ;该索引项的新的值
            - 这是一个全局方法,可以在任何位置使用
        + 使用数组的splice(下标,删除几项,替换的内容)
+ Vue.set(对象名,'属性名','属性值');//这是全局调用
+ this.$set(对象名,'属性名','属性值');//这样写也可以,是通过实例调用的
