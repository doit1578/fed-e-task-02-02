# fed-e-task-02-02

一、简答题
1、Webpack 的构建流程主要有哪些环节？如果可以请尽可能详尽的描述 Webpack 打包的整个过程。

- 流程
  - 初始化项目
  - 配置文件webpack.config.js
  - 配置项目入口、输出路径、开发模式等
  - 配置不同资源处理的loader
  - 配置plugin
  - 执行打包命令

- 通过webpack.config.js配置文件的entry入口配置开始查找项目依赖资源
- 根据配置的loader解析不同的资源，输出打包后的资源。
- 在webpack打包过程中不同阶段根据配置的plugin做一些额外的工作

2、Loader 和 Plugin 有哪些不同？请描述一下开发 Loader 和 Plugin 的思路。

- loader主要是对不同资源做处理，将一些浏览器不支持或者有兼容问题的代码处理为浏览器可以支持的资源，如将ES6+转为ES5、Sass转为css等
  - 开发思路
    - 通过module.exports导出一个函数
    - 该函数默认参数一个参数source(即要处理的资源文件)
    - 在函数体中处理资源(loader里配置响应的loader后)
    - 通过return返回最终打包后的结果(这里返回的结果需为字符串形式)
- plugin主要是在webpack构建的不同阶段执行一些额外的工作，比如拷贝静态资源、清空打包后的文件夹等
  - 开发思路
    - 通过钩子机制实现
    - 插件必须是一个函数或包含apply方法的对象
    - 在方法体内通过webpack提供的API获取资源做响应处理
    - 将处理完的资源通过webpack提供的方法返回该资源
