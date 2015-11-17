# 使用CSS3
==========

使用Modernizr

使用特定于浏览器的样式 --- 开发商前缀
-moz-
-webkit-
-ms-
-o-

## web字体

流程:
@font-face
1) 将字体上传到网站
2) 将每个需要使用的字体注册到 @font-face
3) 在样式表中使用注册过的字体
4) 浏览器遇到使用 web字体 的样式表时, 把字体下载到和图片的缓存中

格式:
因为浏览器支持的字体文件格式不一样
TTF / OTF
EOT
SVG
WOFF

## 媒体查询

根据媒体的信息(大小 / 分辨率 等)采取不同的样式

### 识别浏览器窗口页面大小  max-width
在样式修改量不大的情况下, 使用@media块: 
```
@media (not max-width: 600px) and (max-width: 700px) {
	/* 窗口页面宽度在 (600, 700]px 之间时, 覆盖相应样式 */
}
@media (min-width: 599.99px) and (max-width: 700px) {
	/* 窗口页面宽度在 (600, 700]px 之间时, 覆盖相应样式 */
}
```

在样式区别大的情况下, 单独创建样式表:
```
<link rel="stylesheet" media="(min-width: 480.01px)" href="standard_style.css">
<link rel="stylesheet" media="(max-width: 480px)" href="small_style.css">
```
考虑到老版本的IE不支持媒体查询, 会忽略掉样式, 加上一句支持老IE:
```
<!--[if lt IE 9]>
    <link rel="stylesheet" href="standard_style.css">
<![endif]-->
```

### 识别移动设备 max-device-width
```
<link rel="stylesheet" media="(max-device-width: 480px)" href="mobile_style.css">
```
但是, 已iPhone4为例, 其屏幕分辨率是960px * 640px

## 多变的盒子

### 透明盒子
rgba():
```
.box {
	background: rgb(170, 240, 0);
	background: rgba(170, 240, 0, 0.5);
}
```
第一行代码写上 rgb() , 是为了在不支持rgba()的浏览器中不会有糟糕的体验.
更好的做法是: 在 rgb() 函数中, 选择与rgba()效果相似的颜色, 而非原色.

```
opacity:
.box {
	background: rgb(170, 240, 0);
	opacity: 0.5;
}
```

区别: 
opacity 属性不仅会让背景透明, 还会包括文本、边框等多个元素的颜色
rgba() 只会对其设置的属性值透明

### 圆角盒子
```
border-radius: 10px;
border-radius: 10px 5px;
border-top-left-radius: 150px 30px;
border-top-right-radius: 150px 30px;
```

### 背景盒子
```
.box {
	background-image: url("top-left.png"), url("bottom-right.png");
	background-position: left top, right bottom;
	background-repeat: no-repeat, no-repeat;
}
```
顺序依次对应

### 阴影盒子
```
/* 水平偏量  垂直偏量  模糊距离  阴影颜色 */
box-shadow: 5px 5px 10px gray;

/* 水平偏量  垂直偏量  模糊距离  阴影延伸范围  阴影颜色 */
box-shadow: 5px 5px 10px 5px gray;

/* 水平偏量  垂直偏量  模糊距离  阴影颜色  内部阴影 */
box-shadow: 0px 0px 10px gray inset;
```

### 渐变盒子
-moz- / -webkit- / -o- / IE10
线性渐变
background: linear-gradient(top, white, blue);
background: linear-gradient(top left, white, blue);
background: linear-gradient(top, white, blue, red);
background: linear-gradient(top, white 0%, blue 20%, red 80%, violet 100%);

放射性渐变
background: radial-gradient(cicle, white, blue);

## 过渡效果
transition: background linear 0.5s;

对 padding / margin / font-size 应用过渡就不值得考虑, 
因为这些操作会导致浏览器重新计算布局大小和文本, 可能使响应迟钝和卡顿.

## 变换效果
