# 复习
1. vue单文件方式 XXX.vue
2. 准备好配置文件 package.json(包描述文件 && 封装命令`npm run dev`)+webpack.config.js文件(打包的配置文件)
3. 创建index.html(单页应用的页)
4. 创建main.js(入口文件)
5. 引入vue 和相关的文件 xxx.vue
6. 
```js
 new Vue({
  data(){
    methods
    components(组件内声明组件)
    props
  }
})
```
7. 实例:
  + 在组件内(xxx.vue)中的this
  + new Vue()
  + 实例事件
    - this.$on('事件名',回调函数(参数))
    - this.$emit('事件名',数据)
    - this.$once('事件名',回调函数(参数));只触发一次
    - this.$off('事件名');取消事件
8. 全局
  + Vue.component('组件名',组件对象);在哪里都可以使用
9. 组件传值
  + 父传子:属性作为参数
    - 常量 title="XXX" 子组件申明接收参数 props:['XXX']
    - 变量 :title="XXX" 子组件申明接收参数 props:['XXX']
  + 子传父:vuebus(只能同一个对象)
    - 先停车到父组件,on一下
    - 再开车到子组件,如果需要的话,emit一下,触发上述事件的回调函数

# 今日内容
## 过滤器
+ content | 过滤器,vue中没有提供相关的内置过滤器,但是可以自定义过滤器
+ 组件内的过滤器+全局过滤器
  - 组件内的过滤器就是options中的一个filters的属性(一个对象)
    + 多个key就是不用过滤器名,多个value就是与key对应的过滤方式函数体
  - Vue.filter(函数名,函数)
1. 输入的内容帮我做一个反转
2. 例子:父已托我帮你办点事;反转这个字符串
+ 总结 
  - 全局过滤器:范围大,如果出现同名时,权利小
  - 组件内过滤器:范围小,如果出现同名时,权利大
组件内过滤器
```html
<template>
  <div>
    请输入内容
    <input type="text" name="" v-model="text">
    显示:{{text|myfilter}}
  </div>
</template>
<script>
  exprot default{
    filters:{
      myfilter:function(value){//value 就是 text
      //输入的内容棒我做一个反转
      //转换成数组,反转数组,转换成字符转
          return value.split('').reverse().join('');
      }
    },
    data(){
      return{
        text:''
      }
    }
  }
</script>
<style>
</style>
```
+ 全局过滤器
1. 在main.js文件设置即可,在子组件中的template可以通过{{myfilter}}访问到
```js
//创建全局过滤器
Vue.filter('myFilter',function(value){;//myFilter是过滤器名字,随便起;value是形参;
  return '我是全局过滤器';//返回的信息
})
```

## 获取DOM元素
+ 前端框架就是为了减少dom操作,如果需要操作
  1. 在指定元素上,添加`ref="名称A"`;
  2. 在获取的地方加入`this.$refs.名称A`;
    + 如果ref放在了DOM元素上,获取的就是原生DOM对象
      - 可以直接操作
    + 如果ref放在了组件对象上,获取的就是组件对象
      - 1:获取到DOM对象,通过`this.$refs.组件名.$el`获取
    + 对应的事件(官网上叫钩子),也称生命周期时间(钩子)回调函数
      - created 完成了数据的初始化,此时还未生成DOM,无法操作DOM
      - mounted 将数据已经装载到了DOM之上,可以操作DOM
```html
<template>
  <div>
    <sub-vue ref="sub"></sub-vue>
    <div ref="myDiv">
    {{text}}
    </div>
  </div>
</template>
<script>
import SubVue from './sub.vue'
  exprot default{
    data(){
      return{
        text:'123'
      }
    },
    components:{
      subVue:SubVue
    },
    //组件创建后,数据已经完成初始化,但是DOM还未完成
    created(){//事件处理函数(created)
    // this.$refs.'属性名';这里的属性名要和上面设置的一样,只有数据初始化,在页面中并没有这个元素
    this.$refs.myDiv;//获取不到组件对象
    },
    //数据装载后,各种数据已经就位,将数据渲染到DOM上,DOM已经生成
    mounted(){
      // this.$refs.'属性名';这里的属性名要和上面设置的一样,只有数据初始化,在页面中有这个元素;这就是那个元素
      this.$refs.myDiv;//就是上面那个div
      //如果之前的有text内容在div盒子内,那么这里设置的内容ui覆盖前面的内容
      this.$refs.myDiv.innerHTML = '内容内容';//这里页面就会渲染那个DOM元素
      //这里也可以通过this.text来给内容重新赋值
      //获取得到组件对象
      this.$refs.sub;//就是上面的sub-vue组件
      this.$refs.sub.$el;//获取组件对象,并获取到其的DOM对象
      this.$refs.sub.$el.innerHTML;//获取组件对象,并获取到其的DOM对象,可以进行赋值
    }
  }
</script>
<style>
</style>
```

## mint-ui 组件
1. element-ui 在PC端使用的(饿了么出的)
2. 移动端的版本 mint-ui
3. [网址](https://mint-ui.github.io/#!/zh-cn)
4. 使用步骤-移动端案例
+ 先`npm i mint-ui -S`
+ 在main.js文件中引入`import MintUi from 'mint-ui'`
+ 在main.js文件中引入样式`mint-ui/lib/style.css`
+ 在main.js文件中安装插件`Vue.use(MintUi)`
+ 需要在index.html中增加移动端的视口,快捷键`meta:vp`
+ 注意:
  - 如果是全部安装的方式
    + 在template中可以直接使用组件标签
    + 在script中必须要声明,引入组件对象(按需加载)
```html
<template>
  <div>
        <!-- 固定头部 -->
        <mt-header title="多个按钮">
        <mt-button icon="back">返回</mt-button>
        <mt-button>关闭</mt-button>
        <mt-button icon="more" slot="right"></mt-button>
        </mt-header>

        <button @click="handleClose">显示弹出框</button>
        <!-- switch -->
        <mt-switch v-model="value"></mt-switch>
        <!-- 轮播图 -->
        <mt-swipe :auto="4000">
        <mt-swipe-item>1</mt-swipe-item>
        <mt-swipe-item>2</mt-swipe-item>
        <mt-swipe-item>3</mt-swipe-item>
        </mt-swipe>
  </div>
</template>
<script>
  //在js部分所有变量都是模块作用域
  //如果需要使用就必须引入
  //Toast是模块对象,不是全局的,所以需要先引入
  import { Toast } from 'mint-ui';
  exprot default{
    data(){
      return{
        text:'123',
        value:false,
      }
    },
    methods:{
      handleClose(){
        Toast('提示信息');
      }
    }
  }
</script>
<style>
</style>
```

## vue-router
+ `window.addEventListener('hashchange',fn)`监听锚点值的改变
+ 根据你放`<router-view></router-view>`作为DOM上的标识
+ 最终锚点值改变触发 hashchange 的回调函数,我们讲指定的模板数据插入到DOM标识上
1. 前端路由 核心就是锚点值的改变,根据不同的值,渲染指定DOM位置的不同数据
2. ui-router:锚点值改变,如何获取模板
3. vue中,模板助教不是通过ajax请求来,而是调用函数获取到模板内容
4. 核心:锚点值的改变
5. 以后看到`vue-`开头,就知道必须使用`vue.use`
6. vue的核心插件
  + vue-router 路由
  + vuex 管理全局共享数据
7. 使用方式
  + 1:下载`npm i vue-router -S`
  + 2:在main.js中引入`import VueRouter from 'vue-router'`
  + 3:安装插件`vue.use(插件)`
  + 4:通过创建路由对象,并配置路由规则
        - `let router = new VueRouter({ routers:[{path:'/home',components:Home}]})`
  + 5:将其路由对象传递给Vue的实例,options中
        - 在options中加入`router:router`
  + 6:在app.vue中留坑`<router-view></router-view>`
  + 具体步骤
index.html文件内
```html
<html>
  <head>
    <meta charset="UTF-8">
    <tittle>Document</tittle>
    <meta name="viewport" content="witdh=device-width,user-scalable=no,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0">
  </head>
  <body>
    <div id="app"> </div>
  </body>
</html>
```
main.js文件内
```js
//引入一堆
import Vue from 'vue';
import VueRouter from 'vue-router';
//主体
import App from './components/app.vue';
import Home from './components/home.vue';

//安装插件
Vue.use(VueRouter);//挂载属性
//创建路由对象并配置路由规则
let router = new VueRouter({
  //routers是固定的
  routers:[
    //一个个对象
    {path:'/home',component:Home}
  ]
});
//new Vue 启动
new Vue({
  el:'#app',
  //让vue知道我们的路由规则
  router:router;
  //简写
  // router;
  render:c=>c(App),
})
```
在app.vue文件中
```html
<template>
  <div>
        <div class="h">头部
                <!-- 传统方法,需要跟上路径  (了解)-->
                <a href="#/music">进入音乐</a>
                <a href="#/movie">进入电影</a>
                <!-- 1. 去哪里  命名的方式(推荐)-->
                <router-link  :to="{name:'music'}">进入音乐</router-link>
                <!-- 也可以根路径使用 (了解)-->
                <router-link  to="/movie">进入音乐</router-link>
        </div>
        <!-- 留坑 -->
        <router-view class="b"></router-view>
        <div class="f">底部</div>
</div>
</template>
<script>
  exprot default{
    data(){
      return{
      }
    },
  }
</script>
<style scoped>
        .h{
                height:100px;
                background-color:yellow;
        }
        .b{
                height:100px;
                background-color:skyblue;
        }
        .f{
                height:100px;
                background-color:hotpink;
        }
</style>
```
在home.vue文件中
```html
<template>
  <div>
          我是主页
</div>
</template>
<script>
  exprot default{
    data(){
      return{
      }
    },
  }
</script>

<style>
</style>
```

## 命名路由
+ 需求,通过a标签点击,做页面数据的跳转
+ 使用router-link标签
        - 1.去哪里`<router-link to="/beijing">去哪里</router-link>`
        - 2.去哪里`<router-link :to="{name:'bj'}">去哪里</router-link>`
                + 更利于维护,如果修改了path,只修改路由配置中的path,该a标签会根据修改后的值生成href属性
在main.js文件中
```js
//方法一
let router = new VueRouter({
  //routers是固定的
  routers:[
    //一个个对象
    {path:'/home',component:Home}
    {path:'/movie',component:Movie}
//     便捷的方式(推荐,方便后期维护)
    {name:'music',path:'/music',component:Music}
    //以下规则匹配  /detail?xxx=xxx&xxx=xxxx   查询字符串方式,不用修改下面的
    {name:'detail',path:'/detail',component:Detail}
    // path的方式;需要在路径中申明一个变量id    :id   到时候传参的时候,会把id的值赋值给这个变量
    {name:'detail',path:'/detail/:id',component:Detail}
  ]
});
//方法二
let router = new VueRouter();
router.addRoutes([
  //重定向
  {path:'/home',component:Home}
  //最终无法匹配 -> 404
])
```
```html
<template>
  <div>
    <!-- 列表页 -->
    <!-- 查询字符串的方式 -->
    <ul>
        <li v-for="(v,i) in heros" :key="i">
            {{v.name}}
            <!-- 1. 去哪里   以这样的形式传参 ?id=12-->
            <router-link :to="{name:'detail',query:{id:i}}"></router-link>
        </li>
    </ul>
    <!-- path的方式 -->
    <ul>
        <li v-for="(v,i) in heros" :key="i">
            {{v.name}}
            <!-- 1. 去哪里   以这样的形式传参 ?idetail=12-->
            <router-link :to="{name:'detail',params:{id:i}}"></router-link>
        </li>
    </ul>
</div>
</template>
<script>
  exprot default{
    data(){
      return{
        heros:[
            {name:'pp'},
            {name:'pp2'},
        ]
      }
    },
  }
</script>
<style>
</style>
```
在详情页
```html
<template>
  <div>
          <!-- 详情页 -->
</div>
</template>
<script>
  exprot default{
    data(){
      return{
      }
    },
    //DOM还未生成
    created(){
        //获取路由参数
        //vue-router中挂载了两个对象的属性
        //$route(信息数据)   $router(功能函数)
        // this.$route.params 这里区分了,前面在列表页中用query传的参数,就用query接收,如果是path路径传递的方式就用 params接收,接收的是一个对象,如果要获取对应的参数,要在后面.参数名  如   this.$route.params.id
         this.$route.params ;
        this.$route.query
    },
    //已经将数据装载到页面上去了,DOM已经生成
    mounted(){

    }
  }
</script>
<style>
</style>
```


## 参数router-link
1. 在vue-router中,有两大对象被挂载到了实例this
2. $route(只读,具备信息的对象),$router(具备功能函数)
3. 查询字符串
    + 1.去哪里`<router-link :to="{name:'detail,query:{id:index}'}">XXX</router-lin>`;index是for遍历的下标;唯一
    + 2.导航(查询字符串path不用改) ` {name:'detail',path:'/detail',组件}`
    + 3.去了干嘛,获取路由参数(要注意是query还是params和对应的id名)
        - `this.$route.query.id`
4. path方式
    + 1.去哪里`<router-link :to="{name:'detail,params:{name2:index}'}">XXX</router-lin>`;index是for遍历的下标;唯一
    + 2.导航(path方式需要在main.js路由规则上加上/:XXX)` {name:'detail',path:'/detail/:name2',组件}`
    + 3.去了干嘛,获取路由参数(要注意是query还是params和对应的name2名)
        - `this.$route.params.name2`

## 编程导航
1. 不能保证用户一定会点击某些按钮
2. 并且当前操作,除了路由跳转以外,还有一些别的附加操作
3. this.$router.go(num) 根据浏览器记录 前进 后退;num为-1时,是上一次的记录;num为1,是前进1次
4. this.$router.push(path)
  + 参数path:字符串 `'/XXX'`
  + 对象:`{name:'XXX'}`;这边name的值'XXX'是在main.js中设置的路由规则的属性名和属性值;name是示例
  + 对象:`{name:'XXX',query:{id:1,name:2},params:{id:1,name:2}}`;是传参的书写方式;这边如果是`params`这样写的,前面在main.js路由规则上,也需要写`/:id`和`/:name`

## 重定向和 404
+ 进入后,默认就是/
+ 重定向`{path:'/',redirect:'/home'}`
+ 重定向`{path:'/',redirect:{name:'home'}}`,这种方法维护成本小;
+ 404:在路由规则的最后一个规则
  - 写一个最强大的匹配
  - `{path:'*',component:notFoundVue}`;notFoundVue这个组件需要自己创建出来
  在main.js中配置好路由,并把包引入,做好对应的404和重定向页面
```js
let router = new VueRouter();
router.addRoutes([//路由规则,从上往下执行
  {path:'/',redirect:{name:'home'}};//配置重定向的跳转路径;
  {name:'home',path:'/home',component:Home};//配置跳转路径后的具体走向,是之前引入的Home文件返回的导出项;component(组件),即引用的组件
  {path:'*',component:notFoundVue};
])
```

## Vue.use()
1. 实际操作
  + 组件库,在内部注册了各种全局组件
  + 插件,挂载属性,为了方便this,可以使用其功能

## 多视图
+ 在同一个路径的路由处引入多个组件共同组成一个页面
  - 以前可以放一个坑对应一个路由和显示一个组件
    + 一次行为 = 一个坑 + 一个路由 +一个组件
    + 一次行为 = 多个坑 + 一个路由 +多个组件
+ components 多视图,是一个对象 对象内多个key和value,key对应视图的name属性,value对应要显示的组件对象
+ 多个视图的`<router-view name="header"></router-view>` name就是header
+ 多个视图的`<router-view ></router-view>` name就是 default

main.js文件;增加路由规则
```js
let router = new VueRouter({
  routes:[
    {
      path:'/',
      components:{
        header:headerVue,//这里的name和下面坑名字的name对应上
        default:bodyVue,//如果下面坑没有name属性,默认是default
        footer:footerVue
      }
      }
  ]
})
```

app.vue文件
```html
<template>
  <div>
       <header-vue></header-vue>
       <!-- 留坑,坑的名字 -->
       <router-view class="b" name="header"></router-view>
       <router-view class="b"></router-view>
       <router-view class="b" name="footer"></router-view>


       <footer-vue></footer-vue>
</div>
</template>
<script>
  exprot default{
    data(){
      return{
      }
    },
    //DOM还未生成
    created(){
        //获取路由参数
        //vue-router中挂载了两个对象的属性
        //$route(信息数据)   $router(功能函数)
        // this.$route.params 这里区分了,前面在列表页中用query传的参数,就用query接收,如果是path路径传递的方式就用 params接收,接收的是一个对象,如果要获取对应的参数,要在后面.参数名  如   this.$route.params.id
         this.$route.params ;
        this.$route.query
    },
    //已经将数据装载到页面上去了,DOM已经生成
    mounted(){

    }
  }
</script>
<style>
</style>
```

## 路由包含路由


main.js
```js
//配置路由规则
let router = new VueRouter({
  routes:[
    {path:'/',redirect:{name:'music'}},
    {name:'music',path:'/music',children:[
      //-> /oumei
      {name:'oumei',path:'/',component:Oumei}
    ]}
  ]
})
```

# 引申
1. 在`.vue`的文件中,script中的components对象中的属性名如果是`subVue`,那么在template中可以通过 `sub-vue`拿到组件使用,不区分大小写和-;
2. wappalyzer工具   获取当前网站的使用技术;在浏览器->插件->扩展程序->搜索即可
3. hashchange 事件,监听锚点值的改变,触发该事件;
4. location.hash  地址的锚点值  `#/music`

