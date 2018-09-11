# Vue
## 概述
### 定义:渐进式JS框架;数据驱动编程
### 准备
  + 浏览器插件 Vue.js-devtools;在浏览器中;设置中;更多工具=>扩展程序=>开启开发者模式,把老师发过来的插件拖进去,安装,即可;在浏览器中F12,控制台会多出一个Vue的工具,如果网站是Vue编程的,Vue小图标会高亮
  + VS code插件
    - 自动补全标签
      + Auto Close Tag
      + Auto Complete Tag
      + Auto Rename Tag
    - 开启一个服务器浏览HTML网页，第一次使用需要Ctrl + Shift + p输入 live server选择open
      + Live Server
    - 路径自动补全
      + Path Intellisense
    - vue语法高亮和自动补全代码
      + Vetur
      + VueHelper
  + VS Code 首选项设置    文件--->首选项--->设置，然后添加如下代码：
  ```js
  {
    "editor.fontSize": 16,
    "editor.fontFamily": "Fira Code, Verdana, Consolas", //Fira Code
    "editor.fontLigatures": true,
    "editor.tabSize": 2,
    "editor.formatOnType": true,
    "editor.renderWhitespace": "boundary",
    "editor.wordSeparators": "`~!@#$%^&*()=+[{]}\\|;:'\",.<>/?",
    "extensions.autoUpdate": true,
    "emmet.syntaxProfiles": {
        "vue-html": "html",
        "vue": "html",
        // "javascript": "jsx",
        "javascript": "html"
    },
    "emmet.includeLanguages": {
        "vue-html": "html",
        "vue": "html",
        "javascript": "javascriptreact",
        "wxml": "html"
    },
    "emmet.triggerExpansionOnTab": true,
    "terminal.external.windowsExec": "C:\\#Alan\\Software\\cmder\\Cmder.exe",
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        "vue-html",
        {
            "language": "vue",
            "autoFix": true
        },
        "html",
        "vue"
    ],
    // 需要 npm install -g eslint-plugin-vue
    "eslint.options": {
        "extensions": [
            ".js",
            ".vue"
        ]
    },
    "files.associations": {
        "*.vue": "vue",
        "*.js": "javascript",
        "*.cjson": "jsonc",
        "*.wxss": "css",
        "*.wxs": "javascript",
        // "*.wpy": "vue"
    },
    "editor.cursorBlinking": "smooth",
    "sync.gist": "0098ebc82c9c1ac3237c27c11ba0cca9",
    "sync.lastUpload": "2018-08-21T00:41:00.355Z",
    "sync.autoDownload": false,
    "sync.autoUpload": false,
    "sync.lastDownload": "2017-09-23T11:59:03.285Z",
    "sync.forceDownload": false,
    "sync.host": "",
    "sync.pathPrefix": "",
    "sync.quietSync": false,
    "editor.renderIndentGuides": false,
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
        "**/dist": true
    },
    "vetur.format.styleInitialIndent": true,
    "vetur.format.scriptInitialIndent": true,
    "eslint.autoFixOnSave": true,
    "window.zoomLevel": 0,
    "sync.askGistName": false,
    "fileheader.Author": "Alan-Yih",
    "workbench.startupEditor": "newUntitledFile",
    "liveServer.settings.donotShowInfoMsg": true,
    "git.confirmSync": false,
    "explorer.confirmDragAndDrop": false,
    "explorer.confirmDelete": false,
    "workbench.colorCustomizations": {},
    // "materialTheme.cache.workbench.settings": {
    //     "accentPrevious": "Purple",
    //     "themeColours": "Default"
    // },
    "python.disablePromptForFeatures": [
        "pylint"
    ],
    "python.linting.flake8Enabled": true,
    "workbench.iconTheme": "material-icon-theme",
    "material-icon-theme.folders.color": "#fdd835",
    "material-icon-theme.activeIconPack": "react",
    "sync.removeExtensions": true,
    "sync.syncExtensions": true,
    "editor.quickSuggestions": {
        "strings": true
    },
    "element-helper.version": "2.3",
    "editor.wordWrap": "on",
    "gitlens.advanced.messages": {
        "suppressShowKeyBindingsNotice": true
    },
    "gitlens.historyExplorer.enabled": true,
    "minapp-vscode.disableAutoConfig": true,
    "breadcrumbs.enabled": true,
    "px-to-rem.px-per-rem": 37.5,
    "workbench.colorTheme": "Dracula Soft",
    "files.autoSave": "off",
    "javascript.updateImportsOnFileMove.enabled": "always",
    "editor.smoothScrolling": true
    // wxb88afe2feec4e6e0
}
```

### 常用框架
1. 尤雨溪->Vue
2. Google->AngularJS  英文版2.0版本以上需要先学TS
3. Facebook->ReactJS   英文版16.5

### MVVM型框架
1. 定义
    + module(数据模型)     数据对象
    + view(视图模型,负责将数据模型转化成UI展示出来,就是那些DOM结构)     DOM元素
    + ViewModel(一个同步View和Model的对象)   监听,起桥梁作用,vue实例对象

### 使用步骤即常用命令等
1. 初步使用
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
        <!-- 5. 将data中定义的展示到页面  {{属性名}} -->
        <h1>
        {{msg}}
        </h1>
    </div>
    <!-- 下面这串代码不在mvvm的管辖范围,所以没有任何效果 -->
    <div>{{msg}} </div>
  </body>
<!-- 1. 引入vue文件 -->
    <script src="./vue2.js"></script>

    <script >
        // 2. 创建一个vue实例,这个实例可以用来管理html代码
        let vm = new Vue({
            //3.通过构造函数参数el属性来指定vue实例需要管理的范围,el属性的值是一个id
            el:'#app',
            //4. 通过data属性保存页面需要用到的数据
            data:{
                msg:'hello world'
            }
        })
    </script>
  </body>
</html>
```
2. 插值表达式
+ 作用 渲染data中的数据,写在innerhtml的位置
+ 合法用法,在innerHTML的位置使用
    - 直接写变量
    - 字符串拼接
    - 数值运算
    - 三元表达式
    - 函数
+ 不支持的用法
    - if else 语句
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
      <!-- 插值表达式,作用使展示data中的数据 -->
    <div id="app">
        <h1>{{'姓名'+name}}</h1>
        <p>{{age+1}}</p>
        <p>{{age >= 18?'已成年':'未成年'}}</p>
        <p>
            <!-- {{if(age>18){return'已成年'}}}不能使用if else -->
        </p>
        <!-- 将name倒叙排列 -->
        <p>{{name.split('').reverse().join('')}}</p>
        <p>{{getname()}}</p>
    </div>
  </body>
    <script src="./vue2.js"></script>

    <script >
        let vm = new Vue({
            el:'#app',
            methods:{
                getname(){
                    console.log('只在控制台打印,不会在页面中展示')
                }
            },
            data:{
                name:'mick',
                age:15,
            }
        })
    </script>
  </body>
</html>
```
3. v-text  与插值表达式使用一样  是一个指令
+ `v-XXX` 凡是以v-打头的,都是指令,指令是用来增强html功能的
+ 写在标签的属性位置,将data中的属性名作为v-text的值即可
+ 合法用法
    - 直接写变量
    - 字符串拼接
    - 数值运算
    - 三元表达式
    - 函数

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
        <!-- v-text作用和插值表达式一样,用来展示数据的,在标签的的属性位置使用 -->
        <p v-text="name"></p>
        <p v-text="'姓名'+name"></p>
        <p v-text="age+1"></p>
        <p v-text="age >= 18?'已成年':'未成年'"></p>
        <p v-text="name.split('').reverse().join('')"></p>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                name:'mick',
                age:15,
                avatarUrl:'./avatar.jpg',//在页面中显示的图片地址
            }
        })
    </script>
  </body>
</html>
```
4. v-bind
+ 用于动态绑定属性,可以绑定原生属性即自定义属性
    - 使用方式`v-bind:属性名="data中的属性名"`,写在标签的属性位置,绑定属性的值会随着data中对应属性名的属性值的变化而变化;
    - 简写`:属性名="data中的属性名"`(推荐方式)
+ 用法
    - 支持字符串拼接(不推荐)
    - 使用模板字符串`:属性名='其他字符串${data中的属性名}'`
    -  绑定class样式`:class="{data中的属性名:条件}"`;如果条件为true则class具有属性名,反之则没有

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
      redfont{
          color:red;
      }
  </style>
  <body>
    <div id="app">
       <img v-bind:src="avatarUrl">

       <!-- 字符串拼接 -->
       <a :href="'del.php?id='+id"></a>

       <!-- 模板字符串 (推荐)-->
       <a :href="del.php?id=${id}"></a>

       <!-- v-bind可以动态绑定任何属性 -->
       <p :username="name">测试绑定属性</p>

       <!-- 绑定样式class样式,使用对象语法  :class="{key:条件}" 如果条件为true,则具有该类名;false则没有-->
        <p :class="{redfont:name==='pp'}">测试动态添加样式</p>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                name:'pp',
                age:18,
                avatarUrl:'./avatar.jpg',//在页面中显示的图片地址
                id:11,
            }
        })
    </script>
  </body>
</html>
```
5. v-for
+ 遍历数组
    - 使用方法1 ` v-for="item in arr"`  item是一个参数,表示数组中的每一项;arr是需要遍历的数组的名字 
    - 使用方法2 ` v-for="(item,index)in arr"`  item是一个参数,表示数组中的每一项;arr是需要遍历的数组的名字;index是下标;位置是固定的;
        - `index`可以作为属性`key`的值,例`key="index"`
    - 在遍历的DOM范围内,可以直接使用 `item,index`即获取到了对应的内容和下标
+ 操作数组
    - 注意,以下情况更新数组中的数据后,动态渲染的页面不会刷新(不会触发视图更新)
        + 使用数组的length属性去更改数组的时候不行
        + 使用索引的方式更改数组也不行
    - 解决方式
        + Vue.set(参数1,参数2,参数3)方法
            - 参数1:{object | Array} target;表示需要设置的数组/对象
            - 参数2:{string | number} key;表示数组索引
            - 参数3:{any} value  ;该索引项的新的值
            - 这是一个全局方法,可以在任何位置使用
        + 使用数组的splice(下标,删除几项,替换的内容)
+ key属性
    - 使用v-for循环的时候,一定记得将key属性加上,并且要保证key的值是唯一,不重复的
    - 是用来标识数据的每一项,提高渲染性能的
    - 需要绑定key属性,以便后期操作`:key="index"`
    - 是给vue使用的,所以检查页面是看不到的
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <ul>
            <!-- v-for指令可以用来遍历对象/数组,常用来遍历数组, -->
            <!-- 1.遍历数组 -->
            <!-- 使用方法1.1    v-for="item in arr"   item是一个参数,表示数组中的每一项;arr是需要遍历的数组的名字 -->
            <li v-for="item in list">{{item.name}}</li>
            <!-- 使用方法1.1    v-for="(item,index) in arr"   item是一个参数,表示数组中的每一项;arr是需要遍历的数组的名字 index表示下标-->
            <li v-for="(item,index) in list" key="index">名字{{item.name}},下标是{{index}}</li>
        </ul>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                list:[
                    {id:01,name:'pp1'},
                    {id:02,name:'pp2'},
                    {id:03,name:'pp3'},
                ]
            }
        })
    </script>
  </body>
</html>
```
+ 遍历对象
    - 使用方法1 ` v-for="item in obj"`  item是一个参数,表示对象中的每一项;obj是需要遍历的对象的名字 
    - 使用方法2 ` v-for="(item,key,index)in obj"`  item是一个参数,表示对象中的每一项;obj是需要遍历的对象的名字;index是当前变量的这个属性的下标,;位置是固定的;
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <ul>
            <!-- 2.遍历对象 -->
            <!-- 2.1使用方式   v-for="value in obj"value是对象属性的值,obj是data中这个对象的属性名   -->
            <li v-for="value in boss">{{value}}</li>
            <!-- 2.2使用方式   v-for="(value,key,index) in obj"value是遍历的对象的键(属性值),key表示属性的键(属性名),index是键的索引,obj是data中这个对象的属性名   -->
            <li v-for="(value,key,index) in boss">属性的值:{{value}}属性的名:{{key}}属性的下标:{{index}}</li>
        </ul>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                boss: {name:'pp',age:12},
            }
        })
    </script>
  </body>
</html>
```

6. v-html
+ 渲染带有html标签的字符串
+ 使用不安全,一般不用
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <div v-html="htmlStr"></div>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                htmlStr:'<h1>内容内容</h1>'
            }
        })
    </script>
  </body>
</html>
```
7. v-model指令
+ 双向数据绑定就是数据模型中的数据与视图中的数据同步变化
+ 用来实现双向数据绑定;
    - 只能给input/select/textarea/组件  这些标签使用
+ 使用场景,获取用户输入的数据
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <!-- 双向数据绑定 -->
        <input type="text" v-model="name">
        <!-- 单向数据绑定(读取) -->
        <input type="text" :value="name">
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                name:'pp'
            }
        })
    </script>
  </body>
</html>
```
8. v-on 指令
+ 监听DOM事件,使用v-on指令` v-on:事件类型="事件函数"`;事件类型可以自定义
+ 简写`@事件类型="事件函数"`
+ 传递参数`@事件类型="事件函数(实参)"`
+ 传递事件对象`@事件类型="事件函数($event)"`;如果函数有形参,又想获取事件对象,只需在实参处写上 $event 即可;
+ 事件修饰符  `.stop ` 阻止冒泡及 `.prevent`  阻止默认行为  使用示例`@事件类型.stop ="事件函数()"`
+ 按钮修饰符  一般配合 keyUp 和 keyDown使用
    + 大小写不明感,建议使用驼峰命名法(React中使用)
    + 写法`v-on:keyUp="函数名"`,简写`@keyUp="事件函数"`
    + 加上按键修饰符的写法`@keyUp.建码="事件函数"`
    + 按键修饰符的别名,`@keyUp.别名="事件函数"`
        * enter
        * tab
        * delete (捕获“删除”和“退格”键)
        * esc
        * space
        * up
        * down
        * left
        * right
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <p>{{name}}</p>
        <!-- 监听DOM事件,使用v-on指令   v-on:click="事件函数" -->
        <button v-on:click="changeName">点击改变</button>
        <!-- 简写 -->
        <button @click="changeName">点击改变</button>
        <!-- 传参 -->
        <button @click="changeNameByArg('小小')">点击传参</button>
        <!-- 获取事件对象,如果想传递事件对象,必须写$event,并且不能加引号 -->
        <button @click="getEvent($event)">获取事件对象</button>
        <!-- 事件修饰符,用来增强事件功能,常用的有 .stop  阻止冒泡及 .prevent  阻止默认行为-->
        <a href="http://baidu.com">跳转到百度</a>
        <a href="http://baidu.com" @click.prevent="print">打印一句话</a>
        <!-- 按钮修饰符 -->
        <input type="text" v-model="name" @keyDown.13="submit">
        <!-- 事件修饰符的别名 -->
        <input type="text" v-model="name" @keydown.enter="submit">
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                name:'pp'
            },
            //定义函数在methods属性中
            methods:{
                changeName(){
                    //改变name的值;this指向vue的实例
                    this.name = '大大';
                },
                changeNameByArg(newname){
                    this.name = newname;
                },
                getEvent(e){
                    //e就是事件对象
                    //前提,如果
                },
                print(){
                    console.log('阻止跳转')
                },
                keyDown(){
                    console.log('提交了')
                }
            }
        })
    </script>
  </body>
</html>
```

9. v-if 和 v-show
+ 控制元素的显示与隐藏
    - v-if  是通过操作DOM来显示与隐藏
    - v-show 是用过控制display:none 来显示和隐藏
+ 写法` v-if="条件"`和`v-show="条件"`;带有这个属性的DOM元素显示与隐藏取决于条件是true还是fasle;true显示,fasle则隐藏
+ 使用场景
    - 如果页面中涉及到异步渲染,用v-if
    - 如果页面中涉及到大量DOM元素的显示与隐藏,用v-show;减少DOM操作
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
        <!-- v-if  是通过操作DOM来显示与隐藏-->
    <p v-if="age>=18">已成年</p>
    <p v-if="age<=18">未成年</p>
    <!-- v-show 是用过控制display:none 来显示和隐藏 -->
    <p v-show="age>=18">已成年</p>
    <p v-show="age<=18">未成年</p>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                age:18,
            },
        })
    </script>
  </body>
</html>
```
10. v-else-if  和 v-else
+ 条件为true则显示,false则隐藏
+ 写法`v-else-if="条件"`
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
  </style>
  <body>
    <div id="app">
    <p v-if="age<18">未成年</p>
    <p v-else-if="age>=18 && age < 30">青年</p>
    <p v-else-if="age>30 $$ age<50">成年</p>
    <p v-else>老年</p>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                age:18,
            },
        })
    </script>
  </body>
</html>
```
11. v-cloak
+ 是用来解决表达式闪烁问题
+ 有些电脑刷新页面后 vue2还是没有加载完,所以会看到{{}}在页面上
+ 解决办法 在闪烁的元素的属性 加上 v-cloak;在style中设置样式 [v-cloak]{display:none}
+ 写法
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <script src="./vue2.js"></script>
  </head>
  <style>
      /* 2. 利用属性选择器,选中 v-cloak 设置display:none */
      [v-cloak]{
          display:none;
      }
  </style>
  <body>
    <div id="app">
        <!-- 1. 找到表达式闪烁的标签,加上 v-cloak属性 -->
        <!-- 3. 编译完成之后,会把这个元素上的 v-cloak 指令移除 -->
        <p v-cloak>{{name}}</p>
    </div>
  </body>
    <script src="./vue2.js"></script>
    <script >
        let vm = new Vue({
            el:'#app',
            data:{
                name:'pp',
            },
        })
    </script>
  </body>
</html>
```






# 引申
1. 案例




