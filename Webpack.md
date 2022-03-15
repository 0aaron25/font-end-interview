关于webpack面试题

#### 1.webpack 针对模块化做的处理

这一块建议去读 webpack4 文档中对于 library，libraryTarget 的描述。当我们开发一个 JS 库的时候，通常最终的 npm package 需要输出的是一些组件或 api，这个时候我们需要了解webpack4所提供的模块化的打包能力。通过对libraryTarget的设置，我们可以将我们的工程打包成amd，umd，或commonJS模块。

#### 2.Webpack中的loader与plugins作用分别是什么

loader是一个转换器
1、用于对模块源码文件的预编译和转换，，loader描述了webpack如何处理非javascript模块。
2、没有loader，构建的打包过程无法顺利完成
3、loader作用在打包前
4、将A文件转换为B文件，操作的是文件，比如将A.scss转换为A.css，是单纯的文件转换过程
Plugin是插件扩展器
1、plugin构建过程更完整的补充和优化，如使用new UglifyJsPlugin(),new CssMinimizerPlugin()压缩js和css
2、没有plugin，文件的打包过程可以完成
3、plugin作用于整个打包过程，
4、针对webpack的打包过程，他不直接操作文件，而是基于事件机制工作，会监听webpack打包过程的事件钩子，执行任务，通过事件钩子拦截webpack的执行。