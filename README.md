# vue1+webpack1+vue-router1环境搭建(新手向,老司机勿喷)

## 目录
* [前言](#前言)
* [特别鸣谢](#特别鸣谢)
* 准备工作
  - [安装node](#安装node)
* 正式开始
  - [初始化](#初始化)
  - [安装基础包](#安装基础包)


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

## 正式开始
### 初始化
>利用npm初始化package.json，来管理安装的包<br />
`npm init`
<br />可以对项目进行定义

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

## 特别鸣谢
&nbsp;&nbsp;&nbsp;&nbsp;[简单的vue1环境自我搭建](http://www.qinshenxue.com/article/20160806114423.html)
#### [return top](#目录)
