# webpack-vue

#### 0.项目初始化
>
cd 'to/your/path' npm init
>
#### 1.安装 webpack 
>
分为全局安装和项目内安装
```
    npm install webpack -g
    npm install webpack --save-dev
``` 
>
#### 2.配置webpack.config.js文件
```
     const path = require('path');

     module.exports = {
         entry: './Script/main.js', //项目入口文件
         output:{                    //输出编译后文件地址及文件名
             path: path.resolve(__dirname, 'dist'),
             filename: 'js/bundle.js'
         }
     };
```          
命令行里面执行 webpack 命令即可看到编译后的文件

#### 3安装webpack-html-plugin
npm install html-webpack-plugin --save-dev
```
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    ...
    plugins:[
        ...
        new HtmlWebpackPlugin({
            title:'react 学习',
            inject:'body',
            filename:'index.html',
            template:path.resolve(__dirname, "index.html")
        }),
        ...
    ]
```          
>
再次执行webpack命令可看到多了一个index.html文件
这个文件是根据模板生成的并自动引入打包生成的js文件
运行打包后的index.html即可看到效果。
>
#### 4.安装Vue
>
```
   npm install vue -save
```
修改main.js：
```
    import Vue from  'vue';

    var MainCtrl = new Vue({
        el:'#main',
        data:{
            message:'Hello world'
        }
    })
```
修改index.html:
```
   <div id="main">
      <h3>{{message}}</h3>
   </div>   
```
执行webpack打包运行index.html(打包的文件)报错，经查在webpack.config.js里面配置：
```
    ...
    resolve: { alias: { 'vue': 'vue/dist/vue.js' } }
```
再次运行即可看到效果
![效果图](https://github.com/liubin915249126/webpack-vue/blob/master/image/index1.png)
>
#### 5.安装webpack-dev-server热更新
>
```
    npm install webpack-dev-server -g
    npm install webpack-dev-server --save-dev
    npm install vue-hot-reload-api --save-dev
```
 配置webpack.config.js
```
    ...
    devServer: {
        historyApiFallback: true,
    },
    ...
```  
配置package.json里面命令
```
    "start":"webpack-dev-server --hot --inline --progress --open"
```
执行 npm start 浏览器自动打开页面，更改文件后即可看到页面实时更新

> 
#### 6.安装babel
>
在使用.vue文件之前先要安装babel(将es6语法转化为es5)
```
    npm install babel-core babel-loader babel-plugin-transform-runtime --save-dev 
    npm install babel-preset-stage-0 babel-runtime babel-preset-es2015 --save-dev 
```
项目根目录新建.babelrc文件、配置：
```
    {
    "presets": ["es2015", "stage-0"],
    "plugins": ["transform-runtime"]
    }
```
>
#### 7.安装vue-loader处理.vue的文件 
>
安装loader 处理.css,.vue文件
```
npm install css-loader style-loader vue-loader vue-html-loader --save-dev
```
配置webpack.config.js
```
   ...
   module:{
       loaders: [
           {test: /\.js$/,loader: 'babel-loader',exclude: /node_modules/},
           {test: /\.vue$/,loader: 'vue-loader'}]
        },
    //vue: {loaders: {js: 'babel'}}
   ...
```
配置完运行报错：Cannot find module 'vue-template-compiler'
安装vue-template-compiler
```
cnpm install vue-template-compiler --save-dev
```
>


[参考文献](http://www.jianshu.com/p/a5361bff1cd8)