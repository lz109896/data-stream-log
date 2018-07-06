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







