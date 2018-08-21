# 1、Node.js回调函数
#### 什么是回调？
```
函数调用方式分为三类:同步调用、回调和异步调用。
回调是一种双向调用模式。
可以通过回调函数来实现回调
```
#### 阻塞与非阻塞
```
阻塞和非阻塞关注的是程序在等待调用结果(消息,返回值)时的状态.
阻塞就是做不完不准回来
非阻塞就是你先做,我先看看有其他事没有,完了告诉我一声
```
```js
//阻塞代码
var fs = require('fs');
var data = fs.readFilesync('data.txt');
console.log (data.tostring());
```
```js
//非阻塞代码
var fs = require('fs');

fs.readFile('data.txt', function(err, data){ 
    if(err){ 
        return console.error(err);
    } 
    console.log(data. tostring());
}） 
console.log('程序执行完毕!');
```
```js
事件处理代码流程
1.引入events对象,创建eventEmitter对象.
2.绑定事件处理程序.
3.触发事件.

//引入Event模块并创建eventsEmitter对象
var events = require('events');
var eventEmitter = new events.EventEmmitter();

//绑定事件处理函数
var connctHandler = function connected(){ 
        console.log('connected被调用!");
}
eventEmitter.on('connection',connctHandler());//完成事件绑定

//触发事件
eventEmitter.emit('connection');
console. log('程序执行完毕');
```
#### 模块化的概念与意义
```
1.为了让Node.js的文件可以相互调用, Node.js提供了一个简单的模块系统。
2.模块是Node.js应用程序的基本组成部分。
3.文件和模块是一一对应的。一个Node.js文件就是一个模块。
4.这个文件可能是JavaScript代码、JSON或者编译过的C/C++扩展。
5.Node.js中存在4类模块(原生模块和3种文件模块)。
```

#### Node.js 的模块加载流程
```
1.开始require==>是否在文件模块缓存区中==》是==》返回exports
2.开始require==>是否在文件模块缓存区中==》否==>是否原生模块==》否==》查找文件模块==》根据扩展名载入文件模块==》缓存文件模块==》返回exports
3.开始require==>是否在文件模块缓存区中==》否==>是否原生模块==》是==》是否在原生模块缓存区中==》否==》加载原生模块==》缓存原生模块==》返回exports
```
#### Nodejs的模块加载方式
```
1.从文件模块缓存中加载
2.从原生模块加载
3.从文件加载
```
#### require方法加载模块
```
require方法接受以下几种参数的传递:
1、http、 fs、 path等,原生模块。
2、/mod或../mod,相对路径的文件模块。
3、/pathtomodule/mod,绝对路径的文件模块。
4、mod,非原生模块的文件模块。
```
```js
//模块的主要逻辑
function Hello() { 
    var name;
    this.setName = function( argName ){ 
        name = argName;
    }
    
    this.sayHello = function() { 
        console.log('Hello' + name);
    };
};
//对模块进行导出
module.exports= Hello; 
```
```js
//调用Hello模块
var Hello =require('./hello');

hello = new Hello();
hello.setName('Yideng');
hello.sayHello();
```
#### 匿名函数
```
1.我们可以把一个函数作为变量传递。
2.不一定”先定义,再传递",可以直接在另一个函数的括号中定义和传递这个函数。




8.Node.js路由
```



























