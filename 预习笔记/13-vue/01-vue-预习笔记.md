## 复习
### 配置 vue 入口 index.js
+ 自定义的index.js,在vue上挂载自己的show方法
```js
import ToastComponet from './vue-tosat.vue'
let Toast = { }
Toast.install = function(Vue,option){
Vue.prototype.$toast = function(message,option){//把自定义的toast的函数绑定到Vue的原型上
  const ToastController = Vue.extend(ToastComponet);//构造函数ToastController 通过 extend 继承 Vue 的 构造函数
   var instance = new ToastController().$mount(document.creatElement('div'))//先新建一个实例 ToastController 挂载到 新建的div上,并返回到intance上
   instance.message = message;
   instance.visible = true;

}

}
exprot default Toast;
```
### webpack 模块打包器
+ 常用插件
  1. html-webpack-plugin
  2. extract-text-webpack-plugin
  3. UglifyJsPlugin/new webpack.optimize.UglifyJsPlugin()
  4. CommonsChunkPlugin/new webpack.optimize.CommonsChunkPlugin()
  5. clean-webpack-plugin
  6. copy-webpack-plugin
+ 常用loader
  1. 解析js文件,并输出
  2. 解析css文件 css-loader
  3. 解析sass,less,scss,stylus文件 sass-loader/less-loader/node-sass
  4. 解析图片(png,jpg,svg,gif) file-loader/url-loader 
  5. 给css添加前缀 postcss-loader,autoprefixer
+ scss语法
```html
<style lang='scss'>
  /* css样式 */
</style>
```
### webpack属性配置-复习即案例vue的配置
```js
const htmlWebpackPlugin =require('html-webpack-plugin')
const path = require('path')
module.exprots = {
  entry:{//main是默认入口,也可以是多入口
    main:'./路径'
  },
  //出口
  output:{
    filename:'./路径',//指定js文件
    path:path.join(__dirname,'路径')//最好是绝对路径
  },
  module:{
    //一样的功能rules: webpack2.X之后新加的
    loaders:[  
      {test:/\.css$/,//以'.css'结尾,这里是正则表达式
      loader:'style-loader!css-loader',//顺序是反过来的  2!1
      }
      {test:/\.(jpg|svg|png|gif)$/,//以'.jpg'或者'.svg'结尾
      loader:'url-loader?limit=4096$name=[name].[ext]',//[name].[ext]是内置提供的,因为本身是先读这个文件
      //或者以下面的options的方式配置
      // options:{
      //   limit:4096,
      //   name:'[name].[ext]'
      // }
      },{
        //处理Es6的js
        text:/\.js$/,
        loader:'babel-loader',
        //排除node_modules下的所有
        exclude:/node_modules/,
        options:{
          presets:['es2015'],//关键字
          plugins:['transform-runtime'],//关键字
        }
      },{//解析vue
        text:/\.vue&/,
        loader:'vue-loader',//cue-template-compiler是代码上的依赖
      }
    ]
  }
  //插件的执行顺序,是依次执行的
  pligins:[
    new htmlWebpackPlugin({
      template:'./src/index.html',
    })
    //将src下的template属性描述的文件根据当前配置的output.path,将文件移动到该目录
  ]
}
```


## ES6的模块
### 案例小练习
+ Vue本身默认支持es6的模块导入道导出
+ 安装所需的第三方包;保存在-D开发时依赖项中
  1. babel-loabel (内部依赖babel-core)
    + 关键字(preset es2015)
    + 函数(babel-plugin-transform-runtime )
  2. babel-core
  3. babel-preset-es2015
  4. babel-plugin-transform-runtime 
+ 此为小案例,主要练习ES6中模块导入导出,即Vue配置webpack项
```js
//文件1
//ES5引入 cal对象
var cal = require('./cal.js')
//ES6 引入  cal对象
import cal from './cal.js'
//获取按钮
document.getElementById('btn').onclick = function(){
  var n1 = document.getElementById('n1').value - 0;
  var n2 = document.getElementById('n2').value - 0;
  //自己创建一个函数模块计算 n1+n2 = n3
}
//文件2 
//ES5 导出 cal对象
module.exprots = cal;
//ES6 导出 cal对象
export default cal;
```

### ES6的模块导入和导出
1. 导入
  + 默认导入 `import 变量名 from '路径'`;会获取到整个对象的default
  + 声明式导入 `import {变量名1,变量名2,变量名3...} from '路径'`;按需加载;变量名与导出项的名字要一致
  + 全体导入 `import * as 变量名 from '路径'`;获取的就是一整个对象
2. 导出
  + 默认导出  export default  导出对象;
  + 声明式导出
    - export var 变量名 = 导出项;
    - 或者是先 var 变量名 = 导出项;再 export {变量名};
3. 注意,import 和 export 不能包含在函数中,必须在顶层

### ES6的代码变化
1. 对象属性的声明
+ 当属性的key和变量的名相同,而要使用变量的值做value,就可以简写{name} -> {name:name}
+ es6中函数的声明就是干掉了function
```js
var name = 'pp';
var p = {name};//同 var p = {name:name};
var cal = {
  add:function(){},
  add(){},//效果同上
}
```
## Vue
### Vue介绍
1. 2014年诞生,2013年react,09年 angular js
2. 作者尤雨溪
3. 核心概念:组件化  双向数据流(基于ES5的 defineProperty 来实现的),IE9才支持 
4. angular核心:模块化  双向数据绑定(脏检测:一个数组($watch))
  + 开发一个登陆模块,登陆需要的头部,底部,中部称为组件
  + 组件:组合起来的一个部件(肉不,底部,中部)
  + 细分代码
    - 头部: 页面,样式,动态效果
    - 代码: template style script
5. 双向数据流
  + 1向: js内存属性发生改变,影响页面的变化
  + 1向:页面的改变影响js内存属性的改变
6. 框架对比[网址](https://cn.vuejs.org/v2/guide/comparison.html#React)
### Vue单文件方式
1. 单文件就是一`.vue`结尾的文件,最终通过webpack也会编译成`.js`在浏览器运行
2. 内容:  <template></template>+<script></script>+<style></style>
  + template中只能有一个根节点
  + script按照 exprot default {配置}  来写
  + style 中可以设置 scoped属性,让其只在template中生效

### 一单文件的方式启动
1. webpack招人来理解你的单文件代码
  + vue-loader,vue-template-compiler,代码中依赖vue
2. 启动命令
  + `../node_modules/bin/webpack-dev-server --inline --hot --open`
  + 或者新增一个(注意路径)package.json中;设置简化命令
    ```js
    "scripts":{
      "dev":"../node_modules/bin/webpack-dev-server --inline --hot --open --port 端口号" ,//如果使用的端口被绑定了,打开的是Apache的端口,打开浏览器后看到的是文件格式的,这里需要重新用'--port 端口号'设置一下端口号
      "build":"webpack"
    }
    ```

### Vue基本使用步骤
1. 在html文件中给个div,给个id名
```html
<!-- 有个id即可,app是随意的 -->
<div id="app"></div>
```
2. 安装vue及其需要的依赖项`npm i vue -S && npm i vue-loader vue-template-compiler -D`
3. 新建一个main.js
```js
//1.引入vue
import Vue from 'vue';
//将自己写好东西引进来;// template+script+style
import App from './app.vue';
//2. 创建vue实例
new Vue({
  el:'#app',//渲染的目的地;这里是选择器,名称与上面的id名一样'#app'
  render:function(creater){//creater只是形参;render是渲染内容
    return creater(App);//App包含template+script+style,最终生成DOM结构;返回值就是最终生成的DOM结构
  }
  //对象中key是固定的,值是自定义的;
})
```
4. 编写app.vue
```html
<template>
  <!-- 2.X版本以后只能包含一个根节点,即一个template中只能有一个div;如果有两个就报错 -->
  <div>
    第一个程序
    <!-- 在这边能获取到 text的数字-->
    <!-- 直接输出 -->
    {{text}}
    <!-- 作为input的值输出,改变上面text的值,这边输入框的值也跟着变化,因为v-model是双向数据绑定 -->
    <input type="text" v-model="text">
    <ul>
      <!-- 列表输出 person是变量名,list是数据的名字-->
      <li v-for="person in list">
        {{person.list}}
        <!-- 这里会输出两次li,包含名字 -->
      </li>
    </ul>
  </div>
</template>
<script>
  exprot default{
    //配置
    //类似$.scope.XXX = '初始化'
    // data:fucntion(){},
    data(){
      return{
        //放数据的地方
        text:'随便什么字',
        list:[{name:'pp'},{name:'ppd'}]
       }
    }
  }
</script>
<style></style>
```

### Vue常用命令
+ 都是写在标签的属性内,如<div v-html="html"></div>;这里的html在script标签的data属性中定义了;
  1. v-text 是元素的inner Text只能在双标签中使用
  2. v-html 是元素的innerHTML,不能包含`{{XXX}}`
  3. v-if  元素是否移除或者插入(用true/false控制)
  4. v-show 元素是否显示或者隐藏
  5. v-model 双向数据绑定
  6. v-bind:属性名   单向数据绑定(内存js改变影响页面);属性名处写上要绑定的属性名即可
  7. v-bind:value   给input框赋值用;单向数据绑定(内存js改变影响页面)
  8. v-for 遍历

+ 如果没有定义的,不能直接在页面中使用{{未定义的}}

### class结合v-bind使用;methods和v-on的使用;v-model示例
+ class结合v-bind使用
  1. 需要根据可变的表达式的结果来给class赋值,就需要用到v-bind:class="XXX"
    + v-bind:属性名="表达式",最终表达式预算结束的结果赋值给该属性名 
      - 简化的写法是`:属性名="表达式"`
  2. class:结果的分类
    + 一个样式:返回字符串(三元表达式和key和样式的清单对象)
    + 多个样式:返回对象(样式做key,true或false做值)
    + class="{'A':'red,'B':'green'}[stu
        .score]";具体参数信息查看示例
+ methods和v-on的使用
  1. 绑定事件的方法
    + `v-on:事件名="表达式||函数名()"`
    + 简写`@事件名="表达式||函数名()"`
    + 简写,如果函数名没有参数`@事件名="表达式||函数名"`
    + 声明组件内函数
      - 在export default 这个对象的根属性(和data同级),加上methods属性,其是一个对象,在对象内增加函数即可
        + 这个对象中,key是函数名,值是函数体
    + 在 export default这个对象的根属性加上data属性,其是一个函数,返回一个对象
      - 对象的属性是我们初始化的变量的名称
  2. 凡是在 template中使用变量或者是函数,不需要加this,在script中使用就需要加上this

```html
<template>
  <div>
      <div v-bind:class="isRed?'red':'green'">单个class</div>
      <div :class="{'red':true,'big':false}">多个class</div>
      <!-- 通过遍历,根据当前对象的成绩,匹配成绩和样式的清单对象,用成绩做key,取对象的值做vaule ,最终返回字符串做样式名-->
      <ul>
        <li v-for="stu in stus":class="{'A':'red,'B':'green'}[stu
        .score]">
        {{stu.name}}
        </li>
      </ul>
      <!-- 点击会切换isRed的值 true/false -->
      <button v-on:click="isRed = !isRed">可点击</button>
      <!-- 点击会调用change()函数 -->
      <button v-on:click="change()">可点击</button>
      <!-- 简写   点击会调用change()函数 -->
      <button @click="change">可点击</button>
      增加的名字:<input type="text" name="" v-model="name"><br/>
      增加的成绩:<input type="text" name="" v-model="score">
      <button @click="double">可点击增加自定义的名字和分数</button>
  </div>
</template>
<script>
  //class 取一个 返回一个字符串
  //取多个 返回一个对象
  exprot default{
    data(){
      return{
        name:'',
        score:'',
        isRed:false,
        stus:[{name:'pp',score:'A'},{name:'ppd',score:'B'}]
      }
    },
    //声明函数,属于组件对象的
    methods:{
        //包含多个函数名做key,函数体做value
        change(){//点击按钮,会调用这个函数
          //在script中使用的对象,基本template中也能使用,但是在script中加this,template中不需要this
          // this.XXX
          this.isRed = !this.isRed;//点击按钮,会切换isRed的颜色,会在stus数组的后面增加一个元素,并且具有样式等;
          this.stus.push({
            {name:'mivk',score:'A'}
          });//这个是用来单向数据绑定的
        },
        double(){
          //这个函数是用来双向数据绑定的
          this.stus.push({
            name:this.name,
            score:this.score,
          });
          //添加完成后,把输入框中的内容清空
          this.name = '';
          this.score = '';
        }
    }
  }
</script>
<style>
  .red{
    background-color:red;
  }
  .green{
    background-color:green;
  }
</style>
```

### v-for的使用
1. 可以使用操作数组(item,index)
2. 可以使用操作对象(value,key,index)
3. key 是类似于 trank by的一个属性,为的是告诉vue,js中的元素,与页面之间的关联,当视图删除元素的时候,是单个元素的删除,而不是整版替换,所以需要关联其关系,设置(必须,性能)  2.X版本之后必须设置
```html
<template>
  <div>
    <ul>
      <!-- 使用数组的方式 -->
      <!-- stu表示元素,index表示索引  stus 是数组  v-bind:key="index"是绑定key属性值是index,注意,这里如果使用index,前面 (value,key,index) in person 必须把index传进来-->
      <li v-for="(stu,index) in stus" v-bind:key="index">
        {{index}}
        {{stu}}
        <button @click="del(index)">删除</button>
      </li>
      <!-- 使用对象的方式 -->
      <!-- value表示属性值,key表示属性名,index表示索引  person 是对象;此处绑定key用的是bind简写-->
      <li v-for="(value,key,index) in person" :key="index">
        {{value}}
        {{key}}
        {{index}}
      </li>
    </ul>

  </div>
</template>
<script>
  //class 取一个 返回一个字符串
  //取多个 返回一个对象
  exprot default{
    data(){
      return{
        stus:[{name:'pp',score:'A'},{name:'ppd',score:'B'}]
        person:{name:'mick',aliser:"麦克"}
      }
    },
    //声明函数,属于组件对象的
    methods:{
      del(index){
        this.stus.splice(index,1)
      }
    }
  }
</script>
<style>
  .red{
    background-color:red;
  }
  .green{
    background-color:green;
  }
</style>
```

### 组件的使用
1. vueBus的通信使用,实现子组件通信父组件(vuebus)(扩展)
  + 通过new Vue()这样的一个对象,来$on('事件名',fn(prop1,prop2))
  + 另一个组件,引入同一个 vuebus,来$emit('事件名',prop1,prop2);注意,事件名必须和上面的一致,要同一个对象;
```js
//main.js文件
//引入子组件对象
import subVue from './sub.vue';
//声明全局组件
Vue.component('bodyVue',subVue);
```
```js
//conector.js文件
import Vue from 'Vue';
var conector = new Vue();
export default conector;
```
```html
<!-- 父组件 -->
<template>
  <div>
    <subVue></subVue>
    <button @click="listen">听电话</button>
  </div>
</template>
<script>
  //引入连接器
  import conector from './conector.js';
  exprot default{
      data(){
        return{
        }
      },
      methods:{
        listen(){
          //接电话
          conector.$on('phone',function(msg){
            console.log(msg)
          })
        }
      }
    }
  }
</script>
<style>
</style>


<!-- 子组件 -->
<template>
  <div>
    <button @click="call">打电话</button>
  </div>
</template>
<script>
   import conector from '../conector.js';
  exprot default{
      data(){
        return{
        }
      },
      methods:{
        call(){
          //发射信号
          conector.$emit('phone','发送出去的消息')
        }
      }
    }
  }
</script>
<style>
</style>




```
#### 父子组件的使用(父传子)
1. 创建三个头,中,底部的`.vue`子组件供父组件使用
2. 在父组件中使用即可
3. 父和子,使用的是父,被用的是子
  + 父需要声明子组件,引入子组件对象,声明方式
  ```js
  import 子组件对象 from './XXX.vue'
  {
    components:{
      组件名:子组件对象;
    }
  }
  ``` 
4. 父子组件的使用具体示例
```html
<!-- 这是父组件 -->
<template>
  <div>
    <!-- 使用子组件 -->
    <!-- 这是父组件,在父组件中定义 textone常量 接收父组件参数的示例中会用到-->
    <header-vue textone="大"></header-vue>
    <!-- v-bind:textwo    v-bind会运算这个表达式,拿到值,赋值给texttwo属性这是变量-->
    <body-vue v-bind:textwo="text2"></body-vue>
    <footer-vue></footer-vue>
  </div>
</template>
<script>
  //引入子组件对象
import headerVue from './header.vue';
import bodyVue from './body.vue';
import footerVue from './footer.vue';


  exprot default{
    data(){
      return{
          text2:'哈哈'
      }
    },
    //声明函数,属于组件对象的
    methods:{},
    //必须声明
    components:{
      //组件名(在模板中使用):组件对象
      headerVue:headerVue,
      bodyVue,//简写
      footerVue,//简写
    }
    }
  }
</script>
<style>
  /* 需要去对应的子组件中分别设置div的样式 */
  div:{
    height:100px;
    background-color:pink;
  }
</style>
```
5. 子组件接收父组件值参数的设置(父组件传递参数给子组件)
  + 父组件通过子组件的属性将值进行传递
    - 方式
      + 常量  prop1="常量值" 
      + 变量 :prop2="变量值"(这里是通过v-bind:prop2简写的形式)
  + 子组件需要声明
    - 在根属性中增加属性(与函数data同级)`props:['prop1','prop2']`
    - 在template中直接使用`{{prop1}}`即可得到属性值并且渲染到页面上
    - 在js中使用`this.prop1`获取值
```html
<!-- 这是子组件 -->
<template>
  <div>
    <!-- 使用子组件 -->
    {{textone}}
    {{texttwo}}
  </div>
</template>
<script>
  exprot default{
    data(){
      return{
      }
    },
    //声明函数,属于组件对象的
    methods:{},
    //接收父组件值参数textone
    props:['textone','texttwo']
    //如果这边需要使用父组件传递过来的属性值,使用    this.属性名  即可;
    }
  }
</script>
<style>
  /* 设置子组件的不同的样式 */
  div:{
    height:100px;
    background-color:pink;
  }
</style>
```





#### 全局组件
1. 全局组件,使用更加方便,不需要声明,直接用
2. 在main.js引入一次,在main.js中使用`vue.component('组件名',组件对象)`
3. 所有的组件就可以直接通过组件名,使用
```js
//在main.js文件中写
  //引入子组件对象
import headerVue from './header.vue';
import bodyVue from './body.vue';
import footerVue from './footer.vue';

//声明全局组件
Vue.component('headerVue',headerVue);//注册一个组件,第一个参数是名称,在template中使用,第二个参数是实际的对象,显示成什么内容,具备什么功能
Vue.component('bodyVue',bodyVue);
Vue.component('footerVue',footerVue);
//在其他组件中直接使用即可,不需要别的什么操作
```









## 引申
1. 设置子元素垂直水平居中
```js
//给父元素设置
display:flex;
justify-content:center;
algin-items:center;
```
2. 启动目录的结构
  + project(项目名称)
    - src 存放有功能划分的代码
    - dist 真实上线代码减少请求
    - webpack.config.js打包生成dist下的代码
    - package.json文件 包信息描述
  + node包查找机制是逐级向上查找的
  3. 在项目目录级别的 命令行运行`webpack` 立刻读取webpack.config.js文件,生成到dist目录下
  4. 在项目目录级别的 命令行运行`webpack-dev-server` 运行src下的代码,虚拟出 build.js 测试
  5. `npm i`会下载开发时和生产时依赖项
  6. `npm i --production`会下载生产时依赖项
  7. vue中的文档分类
    + 全局API,全局配置:通过`Vue.`调用的API和配置
    + 实例方法事件:组件内的 `this.` 和`new Vue().`
      - vm.$once 只触发一次
      - vm.$off 取消事件
    + 选项和实例相关
      + 选项/数据 options/类别
      + 选项/DOM options
      + 选项/资源 options
  ```js
  new Vue({//接收的都是选项options
    el:
    render:
  })
  export default{//接收的都是选项options
    componenets
  },
  methods
  ```
  + 总结
    1. 全局的代表Vue.的
    2. 实例的代表this.或者 new Vue().
    3. 选项代表new Vue() 的参数,或者 export default{} 里面的属性名;




