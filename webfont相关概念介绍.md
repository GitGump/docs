#webfont相关概念介绍#
----------

V0.0.2
@gitgump
2015/12/01



##使用font-face##

###CSS写法###
```
@font-face {
      font-family: 'fontName';
      src: url('../font/fontName.eot');
      src: url('../font/fontName.eot') format('embedded-opentype'), 
      url('../font/fontName.woff') format('woff'), 
      url('../font/fontName.ttf') format('truetype'), 
      url('../font/fontName.svg#fontNameregular') format('svg');
      font-weight: normal;
      font-style: normal;
    }
    [class^="icon-"],
    [class*=" icon-"] {
      font-family: fontName;
      font-weight: normal;
      font-style: normal;
      text-decoration: inherit;
      display: inline;
      width: auto;
      height: auto;
      line-height: normal;
      vertical-align: baseline;
      background-image: none !important;
      background-position: 0% 0%;
      background-repeat: repeat;
    }
    [class^="icon-"]:before,
    [class*=" icon-"]:before {
      text-decoration: inherit;
      display: inline-block;
      speak: none;
    }
    .icon-call:before {
      content: "\e600 ";
    }
```


###HTML 写法###
``<i class="icon-call"></i>``


###语法规则解析###
```
@font-face {
        font-family: <YourWebFontName>;
        src: <source>[<format>][,<source>[<format>]]*;
        font-weight: <weight>;
        font-style: <style>;
    }
```
取值说明
1. `YourWebFontName`: 你自定义的字体名称，最好是使用你下载的默认字体，他将被引用到你的Web元素中的font-family。如“font-family:"YourWebFontName";”
2. `source`: 你自定义的字体的存放路径，可以是相对路径也可以是绝路径；
3. `format`：你自定义的字体的格式，主要用来帮助浏览器识别，其值主要有以下几种类型：truetype, opentype, truetype-aat, embedded-opentype, avg等；
4. `weight`和`style`: weight定义字体是否为粗体，style主要定义字体样式，如斜体。


```
.icon-call:before {
    	content: “\e600”;
    }
```
before（after）是伪元素，主流浏览器都已经支持伪元素了，这其中包括了IE8+。
伪元素实际上在html dom中不存在，但会被浏览器渲染成html的一个节点，`:before`，就是在这个标签里的开始处插入了一个子元素（节点），同理，`:after`是在该元素的最后插入子元素，它与以下html具有相同的效果：
```
<div class="icon-call">
    <span></span><!-- 或者一个div -->
     .....
</div>
```
伪元素与一个CSS属性息息相关，就是content，顾名思义，这是定义伪元素内容的，如上面提到的
```
.icon-call:before {
	content: “\e600”;
}
```
相当于：
```
<div class="icon-call">
     <span>”\e600”</span>
 </div>
```
而content里的内容``“\e600”``实际上是一个字符，e600是这个字符16进制unicode编码。
计算机里面每个字符都有一个unicode编码,比如「我」的unicode是6211（16进制），而字体文件的作用是规定某个字符应该用什么形状来显示。
unicode字符集里面，e000 至 f8ff属于用户造字区。原本是空的，用户可以在字体文件里面随便定义这些字符的形状。我们所见的webfont icon，一般就选在这一部分。


###兼容浏览器###
1. TureTpe(.ttf)格式：
.ttf字体是Windows和Mac的最常见的字体，是一种RAW格式，因此他不为网站优化,支持这种字体的浏览器有【IE9+,Firefox3.5+,Chrome4+,Safari3+,Opera10+,iOS Mobile Safari4.2+】；

2. OpenType(.otf)格式：
.otf字体被认为是一种原始的字体格式，其内置在TureType的基础上，所以也提供了更多的功能,支持这种字体的浏览器有【Firefox3.5+,Chrome4.0+,Safari3.1+,Opera10.0+,iOS Mobile Safari4.2+】；

3. Web Open Font Format(.woff)格式：
.woff字体是Web字体中最佳格式，他是一个开放的TrueType/OpenType的压缩版本，同时也支持元数据包的分离,支持这种字体的浏览器有
【IE9+,Firefox3.5+,Chrome6+,Safari3.6+,Opera11.1+】；

4. Embedded Open Type(.eot)格式：
.eot字体是IE专用字体，可以从TrueType创建此格式字体,支持这种字体的浏览器有【IE4+】；

5. SVG(.svg)格式：
.svg字体是基于SVG字体渲染的一种格式,支持这种字体的浏览器有
【Chrome4+,Safari3.1+,Opera10.0+,iOS Mobile Safari3.2+】。

这就意味着在@font-face中我们至少需要.woff,.eot两种格式字体，甚至还需要.svg等字体达到更多种浏览版本的支持。

为了使@font-face达到更多的浏览器支持，Paul Irish写了一个独特的@font-face语法叫Bulletproof
```
@font-face:
    @font-face {
    font-family: 'YourWebFontName'; 
    src: url('YourWebFontName.eot?') format('eot');/*IE*
    src: url('YourWebFontName.woff')format('woff'),url('YourWebFontName.ttf') 
    format('truetype');/*non-IE*/   
    }
```
但为了让各多的浏览器支持，也可以写成：
```
@font-face {
font-family: 'YourWebFontName';
src: url('YourWebFontName.eot'); /* IE9 Compat Modes */
src: url('YourWebFontName.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
url('YourWebFontName.woff') format('woff'), /* Modern Browsers */
url('YourWebFontName.ttf') format('truetype'), /* Safari, Android, iOS */
url('YourWebFontName.svg#YourWebFontName') format('svg'); /* Legacy iOS */   
}
```



##如何自定义字符##
1. 工具：PS或者Illustrator或者FontCreator字体编辑器
2. 在图片软件中调整好单独的图标
3. 打开FontCreator新建一个字体，重命名，然后删成需要的样子（也可以不删）
4. 右击字符图形，选“属性”，调下值然后插入（这个值用在写页面的时候），做完保存
5. 打开http://www.fontsquirrel.com/tools/webfont-generator（内网访问不了）上传刚才的字体在线生成下其他格式的文件，然后下载下来



##如何将图片转成webfont格式##
1. 工具：fontCreator
2. 新建一个字体，选中某一个空白元素
3. 右击，选择“import image”载入图片，点击generate软件会自动生成灰度图
4. 双击可编辑图标，右键选择glyph properties自定义name和content值（V9.0没找到哪里可以输入content），也就是该图标的`class`和`content`
5. 另存为ttf或者woff文件即可引用

**需要说明的是这种方式不支持定制颜色，还需要配合fontsquirrel使用，另外在实践中并没有找到定义`content`属性的地方，所以导出来的文件根本无法引用，导出的文本也不被icomoon支持，所以不推荐使用。**



##参考资料：##
1. http://segmentfault.com/a/1190000003003614
2. http://www.w3cfuns.com/thread-5597432-1-1.html
3. https://icomoon.io/
4. http://www.zhihu.com/question/22022905



