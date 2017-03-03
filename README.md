# vue1+webpack1+vue-router1环境搭建(新手向,老司机勿喷)

## 目录
* [前言](#前言)
* 准备工作
  - [安装node](#安装node)
* 正式开始
  - [初始化](#初始化)
  - [安装基础包](#安装基础包)
  - [初步配置webpack](#初步配置webpack)
  - [搭建vue页面](#搭建vue页面)
  - [配置路由](#配置路由)
  - [配置入口文件](#配置入口文件)
  - [配置App.vue和index.html](配置appvue和indexhtml)
* [特别鸣谢](#特别鸣谢)

## 前言

>&nbsp;&nbsp;&nbsp;&nbsp;很多新手在刚接触的时候会感觉到vue-cli会非常好用，的确非常好用，我也是新手，同样感觉非常的好用,但是这是一个先甜后苦的过程。日后当我们需要对现有项目进行维护配置的时候,却会发现官方给的cli我们随意乱改也许会出错，并且各种各样的语句我们也并不能看懂。当我们想自己配置一个vue+webpack的环境时往往苦于版本或者各种各样的问题难以实现，所以我想通过这个教程来让想自食其力的新手们有一个方向。

#### [return top](#目录)

## 准备工作
### 安装node
首先安装nodejs以获取npm包管理器

>下载地址 https://nodejs.org/en/
>安装方法使用next安装法，在这里我就不赘述了。<br />
当你安装好node，那么恭喜你，你也同时安装了npm包管理器。<br />
如果你觉得npm在国内来说不太友好，那么我推荐你使用以下方法:<br />
>安装cnpm淘宝镜像 传送门（http://npm.taobao.org/）<br />
> 安装yarn 传送门(https://yarnpkg.com/zh-Hans/docs/install#windows-tab)

#### [return top](#目录)

## 正式开始
### 初始化
>利用npm初始化package.json，来管理安装的包<br />
`npm init`
<br />可以对项目进行定义

#### [return top](#目录)
### 安装基础包
#### 安装vue1
`npm install vue@1 --save-dev`
#### 安装vue-loader
`npm install vue-loader@8.7.0 --save-dev`
>安装结束后可能会提示缺少某些包，没关系，按照提示全部安装一遍或者暂时忽略稍后安装也是可行的。<br />
> 值得注意的是 __vue-loader__ 大于10.0.0的版本和小于 10.0.0的版本在后续安装依赖插件是有区别的，如果安装错误版本可能会出现 **cannot read property 'indexOf' of undefined**

#### 安装vue-router
`npm install vue-router@0.7.13 --save-dev`
>__vue-router2与1有着极大的差别，请各位注意__

#### 安装webpack1
`npm install webpack@1 --save-dev`
#### 安装webpack-dev-server
`npm install webpack-dev-server --save-dev`
>安装webpack热加载模块( __轻量级的express服务器便于调试__ )，修改文件实时刷新网页，免除修改一次代码就要重新打包刷新网页的麻烦

#### [return top](#目录)

### 构建目录结构
> | --- package.json&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//包管理文件<br />
  | --- index.html&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// 启动页<br />
  | --- webpack.config.js&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// webpack配置文件<br />
  | --- src<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| --- App.vue&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//项目的入口页面<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| --- main.js&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//项目的入口js<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| --- router.js&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//项目的router配置文件<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| --- components&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//各个组件文件夹<br />
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| --- views&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//各个vue存放的文件夹<br />

#### [return top](#目录)

### 初步配置webpack
####配置入口
    module.exports = {
        entry:  './src/main.js'
    }
####配置热加载
>在package.json中进行配置

    "scripts": {
        "dev": "webpack-dev-server --inline --hot --open"
     }
>在以上配置保存后可以打开命令行（win+r）或者你的git工具到项目跟目录下运行 `npm run dev` <br />
>访问 **localhost:8080**（提前在index.html中写入内容确认是否成功）

#### [return top](#目录)

### 搭建vue页面
#### 在搭建vue页面之前我们来学习一下vue文件的结构(老司机请自动忽略)
    <template></template> //请务必记住template内一般只允许存在一个节点
    <script>
     export default {
          name: '',
          data () {  //当存在data时，必须有return
               return {}
          }
     }
    </script>
    <style>可以在这里写css,前提是已经安装css-loader</style>
####我们需要在views下搭建两个vue页面，为接下来router的配置做准备
    <template>
         <div>
              <h1>This is {{pageName}} page</h1>
        </div>
    </template>
    <script>
         export default {
              name: 'home',
              data () {
                   return {
                        pageName: 'home'
                   }
              }
         }
    </script>
    <style></style>
>相似的我们再创建一个test页面

#### [return top](#目录)

### 配置路由
>在vue-router1中我们需要调用router.map({})配置路由（在2.x版本中已经有更简单的方法了），为了方便后期维护我们将map单独的抽取到router.js中，在外部我们需要使用的时候就调用require('./router')(router)。需要文档的小伙伴可以戳这里(  [vue-router@1.x官方文档](https://github.com/vuejs/vue-router/tree/1.0/docs/zh-cn) )

    module.exports = function (router) {
         router.map({
              '/': {
                   name: 'home',
                   component: require('./views/home.vue')
              }
         })
    }
#### [return top](#目录)

### 配置入口文件
>在main.js中我们需要这么配置

    import Vue from 'vue';
    import VueRouter from 'vue-router';
    var App = require('./App.vue');
    Vue.use(VueRouter);
    var router = new VueRouter();
    require('./router')(router);
    router.start(App, '#app');

#### [return top](#目录)

### 配置App.vue和index.html
### App.vue
    <template>
        <div>
            <!-- 请注意，下列写法在vue2中已经被舍弃 -->
            <a v-link="{path: '/home'}">Home</a>
            <a v-link="{path: '/test'}">Test</a>
            //视图加载的挂载点
            <router-view></router-view>
        </div>
    </template>
    <script></script>
    <style></style>
#### index.html
    <body>
         <div id='app'></div>
         <script src='dist/build.js'></script>
    </body >
#### [return top](#目录)

### 配置loader
>在配置之前我们需要安装一些缺少的package

    npm install babel-core --save-dev

    npm install babel-loader --save-dev

    npm install babel-plugin-transform-runtime --save-dev

    npm install babel-preset-es2015 --save-dev

    npm install vue-hot-reload-api@1.3.3 --save-dev

    npm install vue-html-loader@1.2.4 --save-dev

    npm install vue-style-loader --save-dev

    npm install css-loader --save-dev
>这些包安装好以后我们就可以开始配置webpack.config.js文件了

#### webpack.config.js
    var path = require('path');
    module.exports = {
        entry: './src/main.js',
        output: {
            path: path.resolve(__dirname, './dist'),
            publicPath: '/dist/',
            filename: 'build.js'
        },
        module: {
            loaders: [
                {
                    test: /\.vue$/,         //解析vue文件
                    loader: 'vue'
                },{
                    test: /\.css$/,         //配置以保证外部css文件的加载
                    loader: 'vue-style!css'
                },
                {
                    test: /\.js$/,            //使得webpack能够将es6的语法转换成es5
                    loader: "babel-loader?presets[]=es2015&plugins[]=transform-runtime&comments=false",
                    exclude: /node_modules/
                }
            ]
        }
    }
>现在我们可以放心的`npm run dev`了
#### [return top](#目录)

## 结束语
>这个教程是根据我自己亲身配置得出的，其中踩了不少坑，希望能因为这个教程让新手们少踩点坑，愉快的自食其力。<br />
> 当然我的教程还没有完全配置完成，例如sass等预编译语言的配置，还有图片加载的url-loader的配置，但是这些配置总的来说大同小异，所以我就不一一赘述了，希望能够帮到你。<br />
> Thanks
#### [return top](#目录)

## 特别鸣谢
&nbsp;&nbsp;&nbsp;&nbsp;[简单的vue1环境自我搭建](http://www.qinshenxue.com/article/20160806114423.html)
#### [return top](#目录)
