# 1.项目说明
## 1.1.项目目录结构
```
├─ /resume/ ··················· 项目所在目录
└─┬─ /css/ ······················· 我们自己的CSS文件
  ├─ /img/ ······················· 使用到的图片文件
  ├─ /js/ ························ 自己写的JS脚步
  ├─ /lib/ ······················· 从第三方下载回来的库【只用不改】
  ├─ /resource/ ······················· 网页中用到的其他资源，例如视频、pdf等
  ├─ /favicon.ico ················ 站点图标
  └─ /index.html ················· 入口文件
```
## 项目说明
该简历是本人利用自己所学知识，倾注了十天左右的时间完成。最大程度的用了自己所学的知识，利用使用了html的video标签。
* 简历的一切文字信息均属实
* 简历中出现的一些问题，欢迎指正
* 对于简历的使用，我的态度是欢迎。您的使用恰恰证明我的优秀

# 2.页面滚动
整体项目采用基于Velocity.js的超酷滚动页面特效
> [Velocity.js地址](https://github.com/julianshapiro/velocity)  

## 使用方法
* 要使用某种内置的页面滚动效果，可以在<body>标签上使用data-animation和data-hijacking属性来指定。
* data-animation属性的可选值有：none/scaleDown/rotate/gallery/catch/opacity/fixed/parallax。
* data-hijacking属性的可选值有：on/off。
* 页面滚动特效的HTML结构就是一组<section>元素加上一个上下导航按钮。
* 每一个<section>都简单的设置为100vh，占满整个视口。背景颜色和图片使用:nth-of-type()选择器来选择相应的元素来制作。
* 当data-hijacking = off的时候，每一个section的都根据它相对于视口的位置来动画。
* 当data-hijacking = on的时候，插件中使用Velocity UI Pack registration feature来定义每一个动画的效果

##### 整体结构如下：
```html
<!doctype html>
<html lang="zh" class="no-js">
<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> 
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>刘鸿飞—Web前端工程师</title>	
	<link rel="stylesheet" href="lib/Velocity.js/css/reset.css"> 
	<script src="lib/Velocity.js/js/modernizr.js"></script> 
	<!--[if IE]>
		<script src="http://libs.useso.com/js/html5shiv/3.7/html5shiv.min.js"></script>
	<![endif]-->
</head>
<body data-hijacking="on" data-animation="gallery">
	<!--首页-->
	<section class="cd-section visible">
		<div>
			<h2>Section 1</h2>
		</div>
	</section>
	<!--个人简介-->
	<section class="cd-section">
		<div>
			<h2>Section 2</h2>
		</div>
	</section>
	<!--技能掌握-->
	<section class="cd-section">
		<div>
			<h2>Section 3</h2>
		</div>
	</section>
	<!--工作经历-->
	<section class="cd-section">
		<div>
			<h2>Section 4</h2>
		</div>
	</section>
	<!--作品展示-->
	<section class="cd-section">
		<div>
			<h2>Section 5</h2>
		</div>
	</section>
	<!--个人能力与自我评价-->
	<section class="cd-section">
		<div>
			<h2>Section 6</h2>
		</div>
	</section>
	<!--联系我-->
	<section class="cd-section">
		<div>
			<h2>Section 7</h2>
		</div>
	</section>
	<nav>
		<ul class="cd-vertical-nav">
			<li><a href="javascript:;" class="cd-prev inactive">Next</a></li>
			<li><a href="javascript:;" class="cd-next">Prev</a></li>
		</ul>
	</nav> 
	
	<script src="lib/Velocity.js/js/jquery-2.1.4.js"></script>
	<script src="lib/Velocity.js/js/velocity.min.js"></script>
	<script src="lib/Velocity.js/js/velocity.ui.min.js"></script>
	<script src="lib/Velocity.js/js/main.js"></script> <!-- Resource jQuery -->
</body>
</html>

```

# 3.首页与个人简介
## 3.1.首页
首页作为一个过渡，可以让用户有一个循序渐进的过渡。
* 指明自己对前端的决心
* 用两张图表示

## 3.2.个人介绍
这一部分指出自己的个人基本情况以及所获得的奖项（作为学生，在学校里四年的奖项基本可以代表自己四年的经历）
* “部分奖项”部分，通过添加左右两个伪元素可以实现边框突出的效果。

# 4.技能掌握
这个模块分为左右两块，左边是通过konva框架实现，右边是一个具体的技能能量条
## 4.1.通过konva框架封装圆环
> [konva官方地址](http://konvajs.github.io/) 
* konva是基于canvas封装的框架，将动画图形等封装成对象
* Konva的整体理念
  * 整个视图看做是一个舞台 stage
  * 舞台中可以绘制很多个层 layer
  * layer下面可以有很多的group
  * group下面可以有 矩形、图片、其他形状等
### 将一个个圆环封装封装CircleText对象
* 使用了面向对象的思想
* 代码在CircleText.js文件中
* 封装成对象后只需要直接创建对象就可使用

```javascript
// 封装一个CircleText对象
function CircleText( option ) {
	this._init( option );//构造函数默认执行初始化工作
}

CircleText.prototype = {
	_init: function( option ) {
		this.x = option.x || 0;		//圆形组的中心点坐标
		this.y = option.y || 0;
		this.innerRadius = option.innerRadius || 0;		//内圆半径
		this.outerRadius = option.outerRadius || 0;
		this.text = option.text || 'canvas';			//圆内的文字
		this.innerStyle = option.innerStyle || 'red';	//内圆的填充样式
		this.outerStyle = option.outerStyle || 'blue';	//外圆的填充样式

		//创建文字和圆形的一个组
		this.group = new Konva.Group({	
			x: this.x,  //设置组的x，y坐标后，所有的内部元素按照组内的新坐标系定位。
			y: this.y,
		});
		//初始化一个内部圆
		var innerCircle = new Konva.Circle({	//创建一个圆
			x: 0,	
			y: 0,
			radius: this.innerRadius,  //圆的半径
			fill: this.innerStyle,		//圆的填充颜色
			opacity: .8
		});
		//把内部圆，添加到组内
		this.group.add( innerCircle );

		//初始化一个圆环
		var outerRing = new Konva.Ring({	//初始化一个圆环
			x: 0,
			y: 0,
			innerRadius: this.innerRadius,	//内圆的半径
			outerRadius: this.outerRadius,  //外圆的半径
			fill: this.outerStyle,			//圆环的填充的样式
			opacity: .3						//透明度
		});
		//把外环，添加到组内
		this.group.add( outerRing );

		//初始化一个文字
		var text = new Konva.Text({
			x: 0 - this.outerRadius,
			y: -7,
			width: this.outerRadius * 2,//文字的宽度
			fill: '#fff',			    //文字的颜色
			fontSize: 17,				//文字的大小
			text: this.text,			//文字的内容
			align: 'center',			//居中显示
			fontStyle: 'bold'			//字体加粗
		});

		//把文字添加到组内
		this.group.add( text );

	},
	//把 组添加到层或者其他组中。
	addToGroupOrLayer: function( arg ) {
		arg.add( this.group );
	}
}
```
## 4.2.技能列表
* 将技能分为3类：前端、后台、设计。分为予以三个颜色显示
* 长短代表能力强弱
* 鼠标放在技能条上显示具体技能

# 5.时间经历
以时间为主线，具体为何时在什么地方干了什么事

# 6.个人作品
写了3个项目，通过css3添加了一些效果

# 7.自我概述
分为优势分析与看法、个人能力图
优劣分析和主观看法写了自身的一些情况

## 基于echart的个人能力图
这部分使用echart的饼状图来完成的，当鼠标悬停在相应色块，显示相应能力值
> [echart官网](http://echarts.baidu.com/)
* echart是百度开发的图表工具集

# 8.与我联系
* 这个模块为了凸显html5的新特性，我添加了一个视频
* 视频通过js可以点击视频区域来控制播放与暂停
* 账号部分是通过css3内置动画实现，比较简单
```css
.contactMe .lxfs .chatLogo img:hover {
  cursor: pointer;
  transform: rotate(360deg);
  -ms-transform: rotate(360deg);/* IE 9 */
  -moz-transform: rotate(360deg);/* Firefox */
  -webkit-transform: rotate(360deg);/* Safari 和 Chrome */
  -o-transform: rotate(360deg);
  -webkit-transition: -webkit-transform 0.6s ease-out;
  -moz-transition: -moz-transform 0.6s ease-out;
  transition: transform 0.6s ease-out;
}
```
* 下载简历部分：通过在啊标签添加download属性
