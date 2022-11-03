---
title: CommonJS规范
date: 2016/11/23 19:22:15
categories: 前端
---
JS没有模块系统,为了让JS可以在任何地方运行,CommonJS定义的模块分为:{模块引用(`require`)} {模块定义(`exports`)} {模块标识(`module`)}
 
`require()` 用来引入外部模块；`exports`对象用于导出当前模块的方法或变量，唯一的导出口；`module`对象就代表模块本身。  
<!-- more -->
* 在CommonJs规范中，一个文件就是一个模块，拥有单独的作用域;
* 普通方式定义的变量、函数、对象都属于该模块内;
* 所有代码都运行在模块作用域，不会污染全局作用域；模块可以多次加载，但只会在第一次加载的时候运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果；模块的加载顺序，按照代码的出现顺序是同步加载的;
* `__dirname`代表当前模块文件所在的文件夹路径，`__filename`代表当前模块文件所在的文件夹路径+文件名;
* 通过`require`来加载模块，通过`exports`和`modul.exports`来暴露模块中的内容;
* `require`（同步加载）基本功能：读取并执行一个JS文件，然后返回该模块的`exports`对象，如果没有发现指定模块会报错;
* 模块内的`exports`：为了方便，node为每个模块提供一个`exports`变量，其指向`module.exports`，相当于在模块头部加了这句话：`var exports = module.exports`，在对外输出时，可以给`exports`对象添加方法，PS：不能直接赋值（因为这样就切断了`exports`和`module.exports`的联系）;
* `npm root -g`：查看npm全局包安装位置，`npm config set prefix ""`，将路径添加到环境变量中, `npm init -y`：初始化一个`package.json`文件，加上`-y`就会默认生成该文件，无需一步一步填写；`npm docs 包名`：查看包的文档；`npm install`：安装`package.json`中`dependencies`属性中所有依赖的包
* NPM的模块加载机制：
    * 1、如果`require`的是绝对路径文件(以`./`或`/`开头)，查找不会去遍历每个`node_modules`目录，其速度最快
    * 2、如果参数字符串不以`./`或`/`开头，则表示加载的是一个默认提供的核心模块（位于Node的系统安装目录中），或者一个位于各级`node_modules`目录的已安装模块（全局安装或局部安装）
    * 3、如果指定的模块文件没有发现，Node会尝试为文件名添加.js、.json、.node后，再去搜索。
    * 4、如果想得到`require`命令加载的确切文件名，使用`require.resolve()`方法。