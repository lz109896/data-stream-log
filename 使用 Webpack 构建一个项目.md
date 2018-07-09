# 使用 Webpack 构建一个项目
在本章中，我们学习了一些网络的知识，知道了一些前端的性能指标，也初步认识了 Node.js 和 npm，分析了前端的模块化，最后学习了
Webpack 构建工具的使用。有了这些知识，我们在构建项目的时候就知其然，也知其所以然了，明白我们构建的每个任务背后都是出于某个
目的的。当然，本章最重要的目的还是让大家学会使用构建去优化我们项目目录和开发体验，下面我们就来实践下如何去构建一个完整的项
目吧。

## 项目说明
- 概述： 我们提供的项目src 目录下的代码虽然本身能正常运行，但是代码存在大量全局变量，js文件也很多，并且没有经过优化，在本
项目我们希望大家使用 Webpack 将项目的代码模块化，并且对代码进行打包，压缩等操作，自己动手构建出一个前端工程化的项目。
- 目标：将原始项目改造成使用 Webpack 构建的前端工程化的项目。

## 第一步：Webpack 里的 CommonJS
Webpack 打包本身支持 CommonJS, AMD 甚至 ES6 Modules，而且不需要引用额外的库，只需要直接修改 js 文件，声明依赖和暴露接口
就可以了，打包后的模块也会有自己单独的作用域，模块中声明的变量如 var a = 1 不会影响全局环境，除非通过 window.a = 1 声明，
这样才会挂到全局变量。

##### 所以我们修改源代码的 js 文件只需要根据注释在 头部声明依赖 以及 最后声明本模块暴露的接口或对象 即可。
需要把整个 js 文件夹中的 js 文件进行 头部声明依赖 以及 最后声明本模块暴露的接口或对象
如 src/dust.js, 修改成下面代码即可：
```js
// 灰尘类

// 依赖 global
var global = require('./global');  // 头部声明依赖

// 中间代码不用修改
var Dust = function(){
}
Dust.prototype.init = function(){
}
Dust.prototype.drawDust = function(){
}

module.exports = Dust;   // 最后暴露 Dust 类
```
## 第二步：编写配置文件：webpack.config.js
UglifyJsPlugin 已经更新，不适用新版本，需要做变动

```js
var path = require('path');
var webpack=require('webpack');
var UglifyJsPlugin=require('uglifyjs-webpack-plugin');
//这个插件是用来生成html的
var HtmlwebpackPlugin=require('html-webpack-plugin');
var CopyWebpackPlugin = require('copy-webpack-plugin');
var ExtractTextPlugin = require('extract-text-webpack-plugin');
var CleanWebpackPlugin = require('clean-webpack-plugin');

//用于合并两个webpack的配置文件
module.exports= {
    entry: './src/js/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, './dist')
    },
    module: {
     rules: [{
      test: /\.css$/,
      use: ['style-loader', 'css-loader']
     }]
    },
    plugins:[
        //定义当前生产环境为node环境
        new webpack.DefinePlugin({
            'process.env':{
                NODE_ENV:'"production"'
            }
        }),
        new CleanWebpackPlugin(['dist']),
        new CopyWebpackPlugin([{
            from: path.resolve(__dirname,'./src/images'), 
            to: path.resolve(__dirname,'./dist/images') 
        }]),
        new ExtractTextPlugin('style.css'),

        //提取模板，并保存入口html文件
        //这是来生成html文件的，它通过template选项来读取指定的模板index.ejs,然后输出到filename指定的文件
        new HtmlwebpackPlugin({
            // 模板文件
          template: 'src/index.html',
          // 打包后文件名称，会自动放到 output 指定的 dist 目录
          filename: 'index.html'
        })
    ],
     //压缩js
    optimization: {
        minimizer: [
            new UglifyJsPlugin({
                uglifyOptions: {
                    compress: false
                }
            })
        ]
    },
}


```

## 第三步：安装插件

> 安装 clean-webpack-plugin 命令：  npm i clean-webpack-plugin --save-dev

> 安装 copy-webpack-plugin r命令：      npm i copy-webpack-plugin --save-dev

> 安装 css-loader命令：                      npm i css-loader --save-dev

> 安装 extract-text-webpack-plugi 命令：      npm i extract-text-webpack-plugi --save-dev

> 安装 html-webpack-plugin 命令：          npm i html-webpack-plugin --save-dev

> 安装 style-loader 命令：                npm i style-loader --save-dev

> 安装 webpack 命令：                  npm i webpack --save-dev

> 安装 webpack-dev-server 命令：      npm i webpack-dev-server --save-dev


## 第四步：报错问题官网
尽量去官网查找（需要google翻墙）：https：//webpack.js.org/configuration/optimization/#optimization-minimize
或者翻看：https://github.com/lz109896/data-stream-log/blob/master/webpack%E6%89%93%E5%8C%85.md


## 第五步：打包
> webpack --mode production


## 第六步：自动更新
> npm install webpack-cli -D

> 全局安装命令： npm i webpack-dev-server -g

> 查看安装版本：webpack-dev-server -v

> webpack-dev-server --open













