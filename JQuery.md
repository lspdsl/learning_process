# 1.选择器

+ 标签选择器

  ```js
  //	语法
  $('选择器')
  $('body').css('backgroundColor','red')
  ```

+ 类选择器

  ```js
  // 语法
  $('.类名')
  ```

+ id选择器

  ```js
  //	语法
  $('#id')
  ```

+ 后代选择器

  ```js
  //	语法
  $('body p')
  ```

# 2.JQuery对象

```js
//	jQuery中利用选择器获取到的是jQuery对象，而非DOM对象
//	选择器获取
$('选择器')
//	dom对象转换jQuery对象
$(dom对象)

//	jQuery对象转换DOM对象
jQuery对象[dom对象在jquery中的索引]	//0
$('选择器').get(索引)
```

# 3.事件绑定

```js
//	语法
$('选择器').事件名(function(){})
//	事件名开头不需要写on
//	回调函数中的this，就是触发事件的dom元素

$('li').click(function(){})
```

# 4.链式编程

```js
//	通过.把多个操作连续写下去
//	语法
$('选择器').事件名(回调函数).事件名(回调函数).(事件名(回调函数))
$('.text').focus(function(){console.log(11)}).blur(function(){console.log(22))
```

# 5.内容操纵

```js
//	jQuery中封装了设置网页元素文本内容的方法

//设置	html方法解析标签，text方法不解析标签
$('选择器').html('内容')
$('选择器').text('内容')
//	读取	html方法获取标签，text方法只获取文本
$('选择器').html()
$('选择器').text()

//	设置支持链式编程
$('div').html('<a href="#">111</a>').click(function(){console.log('sssss')})
```

# 6.样式操纵

```js
//	jQuery中对样式的操作进行封装，可以设置或者获取样式
//	1.键值对设置  数值类的样式省略单位，默认是px
.css('样式名','值')
.css('color','red')

//	2.对象方式设置
.css(对象)
.css({
    width:'200px'
    height:200
})

//	3.样式获取
.css('样式名')
```

# 7.属性操纵

```js
//	jQuery中对属性的操作进行封装，可以设置、获取和删除属性
//	1.赋值
.attr('属性名','值')
//	2.取值
.attr('属性名')
//	3.删除属性
.removeAttr('属性名')
```

# 8.操纵value

```js
//	jQuery中封装了操纵表单元素value的方法，可以取值赋值
//	1.赋值
.val('参数')
//	取值
.val()
```

# 9.查找方法

```js
//	jQuery中封装了查找元素的方法，可以基于元素的结构关系查找元素
//	1.父元素
.parent()
//	2.子元素
.children('选择器')
//	3.兄弟元素	不传参时查找所有兄弟元素，不包含自己
.siblings('选择器')
//	4.后代元素
.find('选择器')
```

# 10.操纵类名

```js
//	jQuery中，封装了为网页元素添加、移除、检测、切换类名的方法
//	1.添加类名
.addClass('类名')
//	2.移除类名
.removeClass('类名')
//	3.判断类名，返回布尔值
.hasClass('类名')
//	4.切换类名	类名存在移除，不存在添加
.toggleClass('类名')
```

# 11.事件进阶

```js
//	jQuery中封装了更为灵活的on/off、one方法处理DOM事件
//	1.注册事件
.on('事件名',function(){})
//	2.移除指定事件
.off('事件名')
//	3.移除所有事件
.off()
//	4.注册一次性事件
.one('事件名'，function(){})

//	on、one方法回调函数中的this是触发事件的DOM元素
```

# 12.触发事件

```js
//	1.直接触发
.事件名()

//	2.trigger触发
.trigger('事件名')

//	3.触发自定义事件
.trigger('自定义事件')

// 4. 注册自定义事件
.on('自定义事件',function(){})
```

# 13.绑定windows事件

```js
//	window不是标签，$(window)选中window
//	滚动
$(window).scroll(function(){})
//	点击
$(window).click(function(){})
```

# 14.获取位置

```js
//	取值
$('选择器').offset()
$('选择器').position()
//	返回值
{top:xx,left:xx}

//	offset：位置参照html标签，会把外边距margin计算进去
//	position:位置参照距离最近有定位的祖先元素，以外边距margin为边界，不计算margin
```

# 15.滚动距离

```js
//	取值
$('选择器').scrollLeft()
$('选择器').scrollTop()
//赋值
$('选择器').scrollLeft(值)
$('选择器').scrollTop(值)
```

# 16.显示&隐藏动画

```js
//	通过jQuery以动画的方式显示&隐藏
//	显示	持续时间单位毫秒
$('选择器').show(持续时间)
//	隐藏
$('选择器').hide(持续时间)
//	显示&隐藏
$('选择器').toggle(持续时间)
```

#17.淡入&淡出动画

```js
//	通过jQuery以淡入&淡出的方式切换元素的显示隐藏
//	淡入	单位毫秒
$('选择器').fadeIn(持续时间)
//	淡出
$('选择器').fadeOut(持续时间)
//	淡入&淡出
$('选择器').fadeToggle(持续时间)

//	淡入淡出效果通过修改元素的opactity样式实现的
//	淡入淡出过程中元素的大小不发生改变
```

# 18.展开&收起动画

```js
//	展开	单位毫秒
$('选择器').slideDown(持续时间)
//	收起
$('选择器').slideUp(持续时间)
//	展开&收起
$('选择器').slideToggle(持续时间)

//	垂直方向上调整的样式有高度、margin、padding
```

# 19.动画队列及停止方法

```js
//	通过jQuery为元素设置的多个动画会依次添加到动画队列中，并根据添加的顺序依次播放
//	停止当前动画 进入下一个动画
$('选择器').stop()
//	清空队列 在动画当前状态停止
$('选择器').stop(true)
//	清空队列 直接到当前动画的结束状态
$('选择器').stop(true,true)

//	动画方法和stop方法返回的是同一个jQuery对象
```

# 20.自定义动画

```js
//	jQuery提供了animae方法来实现更为复杂的动画效果
$('选择器').animate(动画属性，持续时间)		//	持续时间单位毫秒
//	数值类样式支持动画，支持多个
//	默认的单位是px
//	支持非样式的特殊属性  scrollTOP  scrollLeft
```

# 21.插入节点--DOM树变化

```js
//	jQuery中封装了在指定位置动态插入元素节点的方法，可以插入节点或者改变节点位置
//	四个方法参数一样位置不同
$('父元素选择器').append(参数)		//	父元素结尾
$('父元素选择器').prepend(参数)		//	父元素开头
$('兄弟元素选择器').before(参数)	   //	兄弟元素去前面	
$('兄弟元素选择器').after(参数)	   //	兄弟元素后面

//	插入节点：传入创建的DOM元素或html结构
//	改变位置：传入现有的dom元素或者jQuery对象
```

# 22.动画的回调函数

```js
//	所有的jQuery动画方法都支持传入回调函数
$('选择器').基础动画方法(回调函数)
$('选择器').基础动画方法(持续时间,回调函数)
$('选择器').animate(属性,回调函数)
$('选择器').animate(属性,持续时间,回调函数)

//	回调函数会在动画执行完毕时立即执行
//	回调函数中的this是执行动画的dom元素
```

# 23.动画的延迟方法

```js
$('选择器').delay(延迟时间).动画方法()
$('选择器').delay(延迟时间).动画方法().delay(延迟时间).动画方法()

//	延迟时间单位毫秒 
```

# 24.获取元素尺寸

```js
$('选择器').width				//	内容宽度
$('选择器').height				//	内容高度
$('选择器').innerWidth()		//	内容宽度+内边距
$('选择器').innerHeight()		//	内容高度+内边距
$('选择器').outerWidth()		//	内容宽度+内边距+边框
$('选择器').outerHeight()		//	内容高度+内边距+边框
$('选择器').outerWidth(true)	//	内容宽度+内边距+边框+外边距
$('选择器').outerHeight(true)	//	内容高度+内边距+边框+外边距
```

# 25.事件参数

```js
//	jQuery中绑定的事件中可以获取事件参数(事件对象)，用法和原生js完全一致
$('选择器').事件(function(event){
    eventstopPropagation
})
```

# 26.删除节点

```js
jQuery对象.remove()

//	remove方法删除的是调用方法的元素节点
```

# 27.事件委托

```js
//	直接绑定
$('选择器').on('事件名',function(){})
//	事件委托
$('祖先选择器').on('事件名','后代选择器',function(){})

//	减少事件注册
//	解决动态增加后代元素的事件绑定问题
//	原理是事件冒泡
//	回调函数中的this是触发事件的dom对象
```

# 28.入口函数

```js
//	原生写法
window.onload=function(){}          //	可以获取图片尺寸
//	jQuery写法
$(window).on('load',function(){})   //	页面资源加载完毕执行逻辑代码
// 完整写法
$(document).ready(function () {})
// 简化写法
$(function () {})					//	dom载入完毕就执行

//	slick			轮播图插件
//	lazyload		懒加载图片
//	fullpage		全屏滚动插件
```

# 29.提交事件

```js
//	阻止提交默认行为，return false=event.preventDefault()
$('form').submit(function (event) {
    console.log('submit')
    event.preventDefault()
    return false
  })
```

# 30.克隆节点

```js
//	克隆/复制节点
//	不带事件
$('选择器').clone()
//	带事件
$('选择器').clone(true)

//	方法返回jQuery对象
```

# 31.表单序列化

```js
//	jQuery中封装了快速获取表单数据的方法，叫做序列化
$('form').serialize()

//	表单元素要有name属性才能获取到value值
//	获取到的数据格式是name1=value1&name2=value2的字符串
```

# 32.插件机制

```js
//	插件是jQuery提供的拓展机制，本质是往jQuery原型对象上添加方法
jQuery.fn.extend({
    插件名(参数){
        //	逻辑
    }
})

//	jQuery是$的别名
//	jQuery内部也是通过这种方式添加方法
//	导入jQuery后新增两个全局变量：jQuery、$
```

# 33.工具方法

```js
//	jQuery除了封装了大量的DOM操作外，还提供了一些工具方法，这些方法通过$或jQuery直接调用

// 遍历数组
$.each(数组, function (值, 下标) {})
// 遍历并返回新数组
$.map(数组,function(值,下标){
	// 返回新的值
  })
```

# 34.常用插件

```js
//	轮播图插件	slick   
//	网址：https://github.com/kenwheeler/slick
//	导入	先导入jQuery再导入slick
<link rel="stylesheet" href="./assets/slick/slick.css" />
<link rel="stylesheet" href="./assets/slick/slick-theme.css" />
<script src="./assets/jquery/jquery-3.5.1.js"></script>
<script src="./assets/slick/slick.js"></script>
autoplay:自动播放
arrows:翻页按钮/true/false
prevArrow:上一页/标签选择器
nextArrow:下一页/标签选择器
dots:指示器/true/false

//	懒加载插件	lazyload
//	网址：https://github.com/tuupola/lazyload/tree/1.x
//	懒加载图片	class='lazyload',data-original='待加载图片',src='占位图片'
//	导入
<script src="./assets/jquery/jquery-3.5.1.js"></script>
<script src="./assets/lazyload/jquery.lazyload.js"></script>

//	全屏滚动插件	fullpage
//	自定义容器包裹要滚动的容器，滚动容器class='section'
//	导入
<link rel="stylesheet" href="./assets/fullpage/jquery.fullpage.css" />
<!-- 导入 jQuery -->
<script src="./assets/jquery/jquery-3.5.1.js"></script>
<!-- 在jQuery之后导入 fullPage -->
<script src="./assets/fullpage/jquery.fullPage.js"></script>
navigation:显示导航/true/false
navigationPosition:导航位置/right/left
anchors:每个区域的锚链接名[]/锚定后当前区域显示在导航栏，刷新页面不复原初始位置
afterLoa():区域加载完毕回调函数,参数：锚链接，索引

//	日期选择器	datepicker
//	网址：https://github.com/fengyuanchen/datepicker
//	导入
<link rel="stylesheet" href="./datepicker/datepicker.css" />
<!-- 导入 jQuery -->
<script src="./assets/jquery/jquery-3.5.1.js"></script>
<!-- 在jQuery之后导入 日期选择器插件 -->
<script src=./datepicker/datepicker.js"></script>
<!--导入语言包-->
<script src=./datepicker/i18n/datepicker.zh-CN.js"></script>
autoPick:是否自动选择当前日期/true/false--默认false
autoHide:选择日期后是否自动关闭/true/false--默认false
languane:语言模式/结合语言包使用

//	表单验证插件	validate
//	网址:
//	导入
<!-- 导入 jQuery -->
<script src="./assets/jquery/jquery-3.5.1.js"></script>
<!-- 在jQuery之后导入 validate插件 -->
<script src=./jquery-validate/jquery-validate.js"></script>
onBlur:失去焦点时验证/true/false---默认false
onSubmit:提交时验证/true/false---默认false
sendForm:是否提交表单/true/fslse---默认true
valid:所有表单项验证通过执行的回执函数/this是jQuery对象
invalid:至少一个表单项验证不通过时执行的回调函数/this是jQuery对象
description:错误提示信息/Object
//	自定义属性--放在表单中
data-required:验证表单项不能为空
data-pattern:基于正则表达式验证
<input data-required data-pattern=".{6,}"
data-describedby:指定显示错误信息的标签/标签的id
data-description:指定错误信息的内容/和description中的属性对应
<input 
type="password"
name="password"
data-required
data-describedby="password-error"
data-description="password"
data-pattern=".{6,}"/>
<span class="error" id="password-error">error</span>
$('form').validate({
    description:{
        password:{  //	对应data-description
            required:'密码不能为空'
            pattern:'密码不能少于六位'   //	验证不通过输出在span中
        }
    }
})
```

# 35.JQuery中的Ajax

```js
//	jquery中发起Ajax请求常用三种方法

//	1.$.get()	--从服务器获取数据，发送get请求
$.get(url,[data],[callback])
url:   string    请求资源的地址
data:  object	 请求资源节期间要携带的参数    非必选
callback: function  请求成功时的回调函数      非必选

//	2.$.post()	--向服务器发送数据，发送post请求
$.post(url,[data],[callback])
url:   string    提交资源的地址
data:  object	 提交的数据    非必选
callback: function  提交成功时的回调函数      非必选

//	3.$.ajax()	--既能获取也能发送胡数据   type设置是get请求还是post请求
$.ajax({
   type: '', // 请求的方式，例如 GET 或 POST
   url: '',  // 请求的 URL 地址
   data: { },// 这次请求要携带的数据
   success: function(res) { } // 请求成功之后的回调函数
})
```



