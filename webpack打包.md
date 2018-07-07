## webpack4.x开发环境配置

配置教程参考：https://blog.csdn.net/u012443286/article/details/79504289

## 【webpack打包成功,但是在dist文件js里没有出现相对应的文件 】问题解决

1.打包成功但是在dist文件js里没有出现相对应的压缩文件，百分百是在某个文件中引用的路径名错了或者路径缺失
（可能因为你添加了文件夹或者更改了文件名）

2.例如：我的项目中，新建了 js 和 css 文件夹,把 .js 文件归纳到 JS 文件夹中，把 .css 文件归纳到 css 文件中了，
那么就要查看更改各个文件中的引用路径是否正确（一般都是需要更改的）。比如我下面的实例： entry: './src/index.js', 
就要把它更改为：entry: './src/js/index.js',才能打包成功并显示打包后的压缩文件：bundle.js

根据报错提示找到路径错误的文件是:

> ERROR in Entry module not found: Error: Can't resolve './src/index.js' in 'F:\homework\webpack-exercise'

修改路径
```js
var path = require('path');
module.exports = {
    entry: './src/js/index.js',
    output: { 
        filename: 'bundle.js', 
        path: path.resolve(__dirname,'./dist')
    },
    module: {
             rules: [
              {
                test: /\.css$/,
                use: [
                 'style-loader',
                 'css-loader'
                ]
             }
        ]
    }
}

```
3.执行webpack --mode development   就完美了


## 当打包出现未选择模式时

1.报错警告是：
```js
warning  The 'mode' option has not been set, webpack will fallback to
                'production' for this value. Set 'mode' option to 'development' or
                'production' to enable defaults for each environment.

```

2.这是因为 webpack 4+以上的版本引入了模式（mode），它有 development、production、none 三个值，我们不指定值时，
默认使用 production。在执行时，需要我们可以把命令调整下，例如：

（开发模式添加了：--mode development）

（生产模式添加了：--mode production）

比如: 就不能单纯的只执行入口文件和输出目录或者文件的命令，必须后面添加： --mode development

正确命令： $ webpack ./index.js -o build.min.js --mode development

比如：最后打包也不能只执行webpack ，这样是打包不成功的，会报错。

正确命令： $ webpack --mode development

3.也可以在package.json中添加配置项：
```js
"scripts": {
　　"dev": "webpack --mode development",
　　"build": "webpack --mode production"
}
```
然后npm run dev  这个时候dist里面的文件的不是压缩过的

但是npm run build 这个时候dist的main.js就是压缩了的。哈哈  很高兴吧


## webpack4.0版本中的js压缩问题
#### 报错提示：
> webpack.optimize.UglifyJsPlugin has been removed, please use config.optimization.minimize instead.

#### 解决方案:
尽量去官网查找(需要google翻墙):https://webpack.js.org/configuration/optimization/#optimization-minimize
```
是webpack版本的问题，在webpack4.0版本中已经废弃了之前 UglifyJsPlugin的用法，用的是config.minimize，然后怎样用optimization呢，
网上资料很多，但是对于一个不熟悉nodejs的人来说，还是比较困难的，我开始以为直接把new HtmlwebpackPlugin改成optimization就行，
自然而然的错了。那怎样做呢？

我们需要以下几步：

用npm安装uglifyjs-webpack-plugin插件;
将其引入：var uglifyjsPlugin=require('uglifyjs-webpack-plugin');
删除以前的写法，将optimization的JS压缩与plugins并排写在一起，注意，是并排，而不是像以前一样写在plugins里面。
```
#### 最后结果如下：
```js
var path = require('path');
var webpack=require('webpack');
var UglifyJsPlugin=require('uglifyjs-webpack-plugin');
//这个插件是用来生成html的
var HtmlwebpackPlugin=require('html-webpack-plugin');

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
        //提取模板，并保存入口html文件
        //这是来生成html文件的，它通过template选项来读取指定的模板index.ejs,然后输出到filename指定的文件
        new HtmlwebpackPlugin({
            // 模板文件
          template: 'src/html/index.html',
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
## webpack使用extract-text-webpack-plugin打包时
> 提示错误Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead


#### 问题描述
使用extract-text-webpack-plugin在打包是提示错误
```js
(node:12712) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
    E:\***\myproject\webpack-vue-elementUi\node_modules\webpack\lib\Chunk.js:460
                    throw new Error(
                    ^

    Error: Chunk.entrypoints: Use Chunks.groupsIterable and filter by instanceof Entrypoint instead
        at Chunk.get (E:\***\myproject\webpack-vue-elementUi\node_modules\webpack\lib\Chunk.js:460:9)
        at E:\***\myproject\webpack-vue-elementUi\node_modules\extract-text-webpack-plugin\dist\index.js:176:48
        at Array.forEach (<anonymous>)
        at E:\***\myproject\webpack-vue-elementUi\node_modules\extract-text-webpack-plugin\dist\index.js:171:18
```
#### 问题分析
```js
看官网也有这个问题，extract-text-webpack-plugin还不能支持webpack4.0.0以上的版本。有个这样的描述 
既然出现这个问题了，那基本上你用的webpack版本一定是4.0.0以上的了。 
查看下package.json里

"devDependencies": {
    ...
    "extract-text-webpack-plugin": "^3.0.2",
    "html-webpack-plugin": "^3.2.0",
    "postcss-loader": "^2.1.4",
    "style-loader": "^0.21.0",
    "webpack": "^4.6.0",
    ...
  },
```
#### 解决办法

>  1、命令行执行:npm install --save-dev extract-text-webpack-plugin@next 会下载到+ extract-text-webpack-plugin@4.0.0-beta.0 

>  2、然后查看package.json里  "extract-text-webpack-plugin版本是否更新

>  3、再打包就正常了
```js
"devDependencies": {
    ...
    "extract-text-webpack-plugin": "^4.0.0-beta.0",
    "html-webpack-plugin": "^3.2.0",
    "postcss-loader": "^2.1.4",
    "style-loader": "^0.21.0",
    "webpack": "^4.6.0",
     ...
  }

```



