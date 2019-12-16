1.entry

作为构建其内部依赖图的开始

2.output

输出结果

3.loader

对于loader，它就是一个转换器，将A文件进行编译形成B文件，这里操作的是文件，比如将A.scss或A.less转变为B.css，单纯的文件转换过程

- css-loader和style-loader模块是为了打包css的

-  babel-loader和babel-core模块时为了把ES6的代码转成ES5

-  url-loader和file-loader是把图片进行打包的。

 loader运行在打包文件之前
 
4.plugin

对于plugin，它就是一个扩展器，它丰富了wepack本身，针对是loader结束后，webpack打包的整个过程，它并不直接操作文件，而是基于事件机制工作，会监听webpack打包过程中的某些节点

plugins在整个编译周期都起作用

5.模式

通过选择 development 或 production 之中的一个，来设置 mode 参数，你可以启用相应模式下的 webpack 内置的优化
```
module.exports = {
  mode: 'production'
};
```
6.module

webpack中一切皆模块，一个模块对应一个文件，webpack会从配置的entry开始递归找出所有依赖的模块。

7.chunk

代码块，一个chunk由多个模块组合而成，用于代码合并与分割
