﻿#gulp:新一代前端构建利器#
--------

V0.0.2
@gitgump
2015/12/01



##什么是gulp##
gulp.js 是一种基于流，代码优于配置的新一代构建工具。
gulp 和 Grunt 类似。但相比于 Grunt 的频繁的 IO 操作，gulp 的流操作，能更快地完成构建。



##gulp特性##
1. 使用方便
通过代码优于配置的策略，gulp可以让简单的任务简单，复杂的任务更可管理。

2. 构建快速
通过流式操作，减少频繁的 IO 操作，更快地构建项目。

3. 插件高质
gulp 有严格的插件指导策略，确保插件能简单高质的工作。

4. 易于学习
少量的API，掌握gulp可以毫不费力。构建就像流管道一样，轻松加愉快。



##gulp安装##
gulp是基于 Node.js的，故要首先安装 Node.js
```
npm install -g gulp
npm install —-save-dev gulp
```



##gulp使用##
gulp的任务都是以插件的形式存在，本次示例以 gulp-jshint 为例，展示gulp的常规用法。

###安装 gulp-jshint###
```
npm install gulp-jshint --save-dev
```

###创建 gulpfile.js###
gulp项目页 有一个 Sample gulpfile。如果不会写的话，直接参考一下就OK了。
```
var gulp = require('gulp');
var jshint = require('gulp-jshint');

var paths = {
  scripts: 'js/**/*.js',
};

gulp.task('lint', function() {
  return gulp.src(paths.scripts)
    .pipe(jshint())
    .pipe(jshint.reporter('default'));
});
```
然后执行命令行
```
gulp lint
```
即可。



##与grunt对比##
1. 流：gulp是一个基于流的构建系统，使用代码优于配置的策略。

2. 插件：gulp的插件更纯粹，单一的功能，并坚持一个插件只做一件事。

3. 代码优于配置：维护gulp更像是写代码，而且gulp遵循CommonJS规范，因此跟写Node程序没有差别。

4. 没有产生中间文件。



##gulp总结##
gulp 相比于 Grunt 有很多优点，比较直观的：就是学习曲线比较平滑。比Grunt速度更快、配置更少。
当然，gulp还有很多高级的特性，详见官方文档http://gulpjs.com/



##参考资料：##
1. http://blog.csdn.net/ys_073/article/details/20805345
2. http://segmentfault.com/a/1190000002932998

