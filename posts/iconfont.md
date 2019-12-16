CSS3 @font-face 规则

 css通常用font-family
 
我们都知道，在网页制作中，会经常用到不同的字体，常用的有 微软雅黑、宋体、Aria 等等。在我们写css的样式的时候，通过 font-family 可以指定元素的字体名称。

CSS3 @font-face自定义字体

如果是 特殊字体 ，因为我们的电脑没有安装那个字体，所以在网页中显示不出来，所以我们通过 @font-face 来引入特殊字体。


```
@font-face {
    font-family: <YourWebFontName>;
    src: <source> [<format>][,<source> [<format>]]*;
    [font-weight: <weight>];
    [font-style: <style>];
}
```
取值说明：

YourWebFontName：字体名称，他将被引用到元素中的 font-family 上

source：字体的存放路径，跟css引用图片一样；

format：字体的格式，主要用来帮助浏览器识别，其值主要有以下几种类型：truetype , opentype , truetype-aat , embedded-opentype , svg 等；

weight和style：这两个值大家一定很熟悉，weight定义字体是否为粗体，style主要定义字体样式，如斜体。

注：字体文件格式

**TrueType(.ttf)** 格式：
.ttf 字体是 Windows 和 Mac 的最常见的字体，是一种 RAW 格式，因此他不为网站优化,支持这种字体的浏览器有 【IE9+ , Firefox3.5+ , Chrome4+ , Safari3+ , Opera10+ , iOS Mobile Safari4.2+】

**OpenType(.otf)** 格式：
.otf 字体被认为是一种原始的字体格式，其内置在 TureType 的基础上，所以也提供了更多的功能,支持这种字体的浏览器有【Firefox3.5+ , Chrome4.0+ , Safari3.1+ , Opera10.0+ , iOS Mobile Safari4.2+】

**Web Open Font Format(.woff)** 格式：
.woff 字体是Web字体中最佳格式，他是一个开放的 TrueType/OpenType 的压缩版本，同时也支持元数据包的分离,支持这种字体的浏览器有【IE9+ , Firefox3.5+ , Chrome6+ , Safari3.6+ , Opera11.1+】

**Embedded Open Type(.eot)** 格式：
.eot 字体是IE专用字体，可以从TrueType 创建此格式字体,支持这种字体的浏览器有 【IE4+】

⚠️
字体文件的体积可能非常的大，而且需要额外的HTTP连接，这些都会降低网站页面的加载速度。所以，在使用网络字体@font-face前，你需要清楚它的利与弊，判断网络字体是否真的有必要用在你的网站页面上。

http://font-spider.org/
中文字体压缩器