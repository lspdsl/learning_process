#1.选择器

+ 标签选择器

  标签名 {属性： 属性值}

+ 属性选择器

  标签名[属性]{}

+ 类选择器

  class="" 定义类名

  .类名 {属性： 属性值}

  class中可写多个类名，类名与类名之间用空格隔开

  < div class="color font"> 定义了color与font两个类

+ id选择器

  id="id名"

  -#id名{属性： 属性值}  id唯一，不允许存在同id标签，id选择器只能选择一个标签

+ 通配符选择器

  *{属性： 属性值} 选取页面中所有的标签

#2.字体属性

+ 字体系列

  font-family定义字体系列

  font-family: ‘Microsoft Yahei’,Arial  多字体从前往后判断是否存在， 不同字体用 , 隔开、字体名有空格用引号

+ 字体大小

  font-size

  body 可定义整个页面字体大小

+ 字体粗细

  font-weight   默认400 =normal  700=bold(粗体)

+ 文字样式

  font-style    italic 斜体

+ 符合属性

  body {font: font-style font-weight font-size/line-height font-family}顺序固定不可改变,各属性间用空格隔开

  ```
  body{
    font-style: italic;
    font-weight: 700;
    font-size: 16px;
    font-family: "Microsoft YaHei";
  }
  body {
  font:italic 700 16px 'Microsoft YaHei';
  }
  body {
  font:16px/20px 'Microsoft YaHei';     /*20px表示行高，如果是1.5表示当前元素文字大小的1.5倍*/
  }
  ```

​       不需要的属性使用默认值可不写，但必须保留font-size和font-family属性，否则font不起作用

#3.文本属性

+ 文本颜色

  color   颜色预定值red/十六进制/RGB代码rgb(255,0,0)或rgb(100%,0%,0%)

+ 对齐文本

  text-align  只能设置水平对齐方式

+ 装饰文本

  text-daecoration: none 默认，无装饰线/underline 下划线/overline 上划线/line-through 删除线

+ 文本缩进

  text-indent: 2em 

  em表示相对单位，就是当前文字一个文字的大小，如果当前元素没有设置大小，em按照父元素一个文字大小

+ 文本行间距---行高

  line-height

+ 单行文字垂直居中

  让文字的行高等于盒子的高度，就可以让文字在当前的盒子内垂直居中

#4.CSS引入方式

+ 行内样式表--行内式

  <-p style="color: red;font-size: 12px">

+ 内部样式表--嵌入式

  css放在<style>标签中，<style>标签一般放在<head>中

+ 外部样式表--链接式

  引用css文件<link rel="stysheet" href="css文件路径">link写在head中

#5.Emmet语法

+ 生成标签    输入标签名按tab键
+ 生成多个相同标签  div*3再按tab键
+ 生成具有父子关系的标签  ul>li tab键
+ 生成具有兄弟关系的标签  div+p tab键
+ 生成带有类名或id的div标签   .demo或#demo1 tab键
+ 生成递增类名div 可用自增符号$    .demo$*3 tab键
+ 生成标签中有默认字符   p{默认字符} tab键

#6.CSS的复合选择器

+ 后代选择器

  可以选择父元素里面的子元素，外层标签写在前面，内层标签写在后面，用空格分开,最终改子元素的样式

  元素1 元素2{样式声明}   ul li{}  后代选择器可选多层后代 ul li a{}

+ 子选择器

  选择最近一级的子元素，再下级同名元素不选择

  ul>a  选择ul下的 a标签

+ 并集选择器

  div,p{}  不同标签用逗号隔开

+ 伪类选择器

  用于向某些选择器添加特殊的效果，不同选择器之间用冒号隔开

  + 链接伪类选择器

    a:link			选择所有未被访问的链接

    a:visited       选择所有已被访问的链接

    a:hover        选择鼠标指针在上面的链接

    a:active       选择活动链接，鼠标按下未弹起的链接

    为确保链接伪类生效，声明顺序按照 link visited hover active声明

  + :focus伪类选择器

    用于选取获得焦点的表单元素

    input:focus{

    background-color:red;}

#7.CSS的元素显示模式

+ 块元素 <h1>~<h6> 、<p>、<div>、<ul>、<ol>、<li>等   文字类标签内不能放块元素<p>、<h>

  + 独占一行
  + 高度、宽度、外边距、内边距都可以控制
  + 宽度默认是容器(父类的宽度)的100%
  + 是一个容器盒子，里面可以放行内或块级元素

+ 行内元素

  <a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等

  + 相邻行内元素在一行上，一行可以显示多个行内元素

  + 高度宽度直接设置是无效的

  + 默认宽度就是本身的宽度

  + 行内元素只能容纳文本或其他行内元素

    特殊情况：<a>里面可以放块级元素，但是给<a>转换一下块级模式更安全

+ 行内块元素

  行内元素中有几个特殊的标签---<img/><input/><td>他们同时具有块元素和行内元素的特点

  + <p style="color:red;">和相邻行内元素在一行上，但是他们之间会有空白缝隙，一行可以显示多个</p>

  + 默认宽度就是它本身内容的宽度

  + 高度、行高、外边距以及内边距都可以控制

+ 元素显示模式转换

  特殊情况下，一个模式的元素需要另外一种模式的特性

  + 转换为块元素				display: block;
  + 转换为行内元素            display: inline;
  + 转换为行内块元素         display: inline-block;

#8.CSS的背景

+ 背景颜色

  background: 颜色值;         一般情况下元素背景颜色默认是transparent--透明

+ 背景图片

  background-image： none|url(url);     背景图片与背景颜色同时存在时，背景图片在背景颜色上层

+ 背景平铺

  background-repeat: repeat|no-repeat| repeat-x|repeat_y-----平铺|不平铺|x轴平铺|y轴平铺

+ 背景图片位置

  background-position: x  y;   x  y可用方位名词或者精确单位

  + 方位名词

    + 方位顺序无关  top center=center top
    + 只指定一个方位名词，另一个省略，则第二个值默认居中对齐

  + 精确单位

    + 指定两个数值必定按照下x,y坐标顺序，第一个数据为x左边,第二个为y坐标
    + 只指定一个数值那么该数值为x坐标，另一个默认垂直居中

  + 混合单位坐标

    如果指定的两个值是精确单位和方位名词的混合使用，则第一个值是x坐标，第二个值是y坐标

+ 背景图片的固定

  background-attachment: scroll  /fixed;

+ 背景复合写法 

  background：color image repeat scroll position;

  background: red url(img/img.jpg) repeat-x fixed top;

+ 背景色半透明效果

  background: rbga(0,0,0,0.3)        参数a表示透明度，取值在0-1之间

#9.CSS的三大特性

+ 层叠性

  解决相同选择器设置相同样式冲突的问题

  + 样式冲突时遵循就近原则，执行最后定义的样式，只覆盖同种样式，别的样式不覆盖
  + 样式不冲突不会冲突

+ 继承性

  子标签据称父标签的某些样式，如文本颜色和字号

  text-    font-    line-  这些元素开头的都可以继承

  + 行高的继承

    继承行高时，父标签行高用倍数表示时，子标签行高用自身文字大小乘以父标签行高的倍数

    body{

    ​	font: 12px/1.5 'Microsoft Yahei'

    }

    p{

    font-size: 16px;}

    p继承body的行高,用自身文字大小乘以1.5，为自身的行高

+ 优先级

  当同一个元素指定多个选择器，就会有优先级的产生

  + 选择器相同，则执行层叠行

  + 选择器不同，则根据选择器的权重执行

    ！important>行内样式>ID选择器>类、伪类选择器>元素选择器>继承或者 *

    ​        无穷大    1000         0100             0010                   0001              0000

    权重比较时从高位向低位逐位比较 

    + 权重叠加

      如果是复合选择器，则会有权重叠加，需要计算权重

      计算按照权重直接相加，不会产生进位

      ul li{}  权重为0001+0001=0001

      .nav li{}权重为   0010+0001=0011

#10盒子模型

+ 盒子模型组成

  边框、外边距、内边距、内容

  + 边框----border

    边框由边框粗细、边框样式、边框颜色三部分组成

    border: border-width  || border-style  || border-color       无顺序要求

    border: 1px solid red;

    border-top:1px solid red;      只设定上边框，其余边框同理

    边框会影响盒子的实际大小，盒子实际大小为盒子内容大小+边框大小

  + 内边距----padding

    盒子边框与内容之间的距离

    padding-left 

    padding-right

    padding-top

    padding-bottom

    padding:5px;   四个内边距都默认5px                                                                      一个参数

    padding: 5px 10px; 上下内边距5px，左右内边距10px                                         两个参数

    padding: 5px 10px 20px;上内边距5px，左右内边距10px,下内边距20px           三个参数

    padding:5px 10px 20px 30px; 上5px,右10px,下20px,左30px                             四个参数

    内边距会影响盒子的大小，盒子有了宽度和高度，再指定内边距会撑大盒子-----若要保证盒子跟效果图大小保持一致让width/height减去多出来的内边距大小即可

    如果盒子本身没有指定宽度/高度，此时padding不会改变盒子宽度/高度

  + 外边距----margin

    margin-left

    margin-right

    margin-top

    margin-bottom

    margin简写参数意义与padding一样   

    <p style='font-weight:700;color:red'>
        外边距可以让块级盒子水平居中，但必须满足两个条件：
    </p>


    1. 盒子必须指定了宽度
    2. 盒子左右的外边距都设置为auto
    
    <p style='font-weight:700;color:red'>
       行内元素或者行内块元素水平居中给其父元素添加text-align:center即可
    </p>


    + 嵌套块元素垂直外边距的塌陷
    
      对于两个嵌套关系的块元素，父元素有上外边距的同时子元素也有上外边距，此时父元素会塌陷较大的外边距值
    
      解决方案：
    
      1. 为父元素定义上边框
    
      2. 为父元素定义上内边距
    
      3. <p style='font-weight:700;color:red'>
              为父元素添加overflow:hidden
          </p>

  + 清除内外边距

    *{

    padding: 0;

    margin:0;

    }

    **行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距。但是转换为块级和行内块元素就可以了**

#11.圆角边框

border-radius 属性用于设置元素的外边框圆角

border-radius: 50px/50%;

设置圆形 -----先做一个正方形，border-radius参数设置正方形变长的一半

圆角矩形 -----矩形，参数设置为高度的一半

一个参数    四个角

两个参数  左上右下，右上左下

三个参数   左上，右上左下，右下

四个参数     左上角，右上角，右下角，左下角

#12.盒子阴影

box-shadow: h-shadow v-shadow blur sread color inset;

h-shadow------------必需，水平阴影的位置，允许负值

v-shadow-----------必需，垂直阴影的位置，允许负值

blur-------------------可选，模糊距离

spread---------------可选，阴影的尺寸

color------------------可选，阴影的颜色

inset-------------------可选，将外部阴影(outset)改为内部阴影

**默认的是外阴影，但是不可以写这个单词，否则会导致阴影无效**

**盒子阴影不占用空间，不会影响其他盒子排列**

div:hover{box-shadow: h-shadow v-shadow blur sread color inset;}   鼠标经过时添加阴影

#13.文字阴影

text-shadow: h-shadow v-shadow blur color; 

#14.CSS浮动  

<p style='font-weight:700;color:red'>
    网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动。
</p>


float属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含快或龙一个浮动框的边缘

选择器 {float：属性值; }

+ 浮动特性

  1. 浮动元素会脱离标准流

     + 脱离标准普通流的控制移动到指定位置
     + 浮动的盒子不再保留原先的位置

  2. 浮动的元素会一行内显示并且元素顶部对齐

     <p style='font-weight:700;color:red'>
         浮动的元素是相互贴在一起的，中间没有缝隙，如果父级宽度装不下这些盒子，多出的盒子会另起一行
     </p>

  3. 浮动的元素不论是行元素还是块元素都会具有行内块元素的特性

+ 浮动元素经常和标准流父盒子搭配使用

  <p style='font-weight:700;color:red'>
      先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置
  </p>

+ 一个元素浮动了，理论上其余的兄弟元素也要浮动

  一个盒子里面有多个盒子，如果其中一个盒子浮动了，那么其余的兄弟盒子也应该浮动，以免出现问题

  <p style="color:red; font-weight:700">
      浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流
  </p>

#15.清除浮动

由于父级盒子很多情况下不方便给高度，但是子盒子浮动不占有位置，父盒子高度就变成了0，会影响父盒子下面的标准流盒子

+ 语法

  选择器 { clear：属性值} 

  clear: left;----------------清除左侧浮动的影响

  clear: right;--------------清除右侧浮动的影响

  clear: both---------------清除左右两侧浮动的影响

+ 清除浮动的方法

  1. 额外标签法----隔墙法

     在浮动元素末尾添加一个空的标签(**块级元素标签**) 例：< div style="clear:both">< /div>

  2. 父级添加overflow属性

     overflow：属性值；     hidden  ||  auto  ||  scroll

  3. 父级添加after伪元素

     ```
      .clearfix:after {              clearfix  父级类名
                 content: "";
                 display: block;
                 height: 0;
                 clear: both;
                 visibility: hidden;
             }
     
             .clearfix {
                 /* IE6、7 专有 */
                 *zoom: 1;
             }
     ```

  4. 父级添加双伪元素

     ```
      .clearfix:before,
             .clearfix:after {
                 content: "";
                 display: table;
             }
     
             .clearfix:after {
                 clear: both;
             }
     
             .clearfix {
                 *zoom: 1;
             }
     ```

#16.CSS定位

定位：将盒子固定在某一个位置，可叠在其他盒子上层。

定位=定位模式+边偏移

定位模式：指定一个元素在文档中的定位方式  通过position设置    属性：static、relative、absolute、fixed

边偏移：决定该元素的最终位置   属性值：top  bottom left right    定义距离父元素边界的距离

+ 静态定位------static

  语法：选择器{position：static}

  静态定位按照标准流特性摆放位置，他没有边偏移

  静态定位在布局中很少用到

+ 相对定位------relative

  语法：选择器{position: relative}

  相对定位参照位置是参照自身原来的位置移动的

  <p style="color:red;font-weight:700;">相对定位的盒子移动到了别的位置，原来的位置仍保留，其他盒子不能占用移动前存在的位置</p>

  top:100px;相对原来的上边界，向下移动100px

  left:100px;相对原来的左边界，向右移动100px

+ 绝对定位-----absolute

  绝对定位是相对于它祖先元素移动的

  语法：选择器{position：absolute;}

  <p style="color:red;font-weight:700">
      如果没有祖先元素或祖先元素没有定位，则以浏览器边缘为定位标准<br>
      如果祖先元素有定位，则以最近一级的有定位的祖先元素为参考点移动位置<br>
  绝对定位不再占有原先的位置
  </p>

+ 固定定位-------fixed

  元素固定在浏览器可视区的位置

  语法：选择器{ position：fixed;}  

  与父元素没有关系

  不随滚动条滚动

  固定位不占有原先的位置

  <p style="color:red;font-weight:700">
      固定定位定位在版心右侧位置---随屏幕缩放位置变化，但始终固定在排版内容右侧：<br>
      1.让固定定位的盒子left:50%;走到浏览器可视区一半的位置<br>
      2.让固定定位的盒子margin-left:版心宽度一半的距离<br>
      经过两步，第一次到屏幕中间位置，第二步走到排版内容右边的位置
  </p>

+ 粘性定位-------sticky

  语法：选择器{position：sticky; top: 10px}

  特点：以浏览器可视窗口位参照移动元素，粘性定位占有原先的位置，必须添加top、left、right、bottom其中一个才有效

+ 定位的叠放次序----z-index

  语法：选择器{z-index: 1;}     数值可以是正整数、负整数或0，默认是auto，数值越大盒子越靠上

  <p style="color:red">数值相同时，按照书写顺序，后写的显示在上层
  </p>

+ <p style="color:red;font-weight:700">定位的拓展
  </p>


  1. 绝对定位的盒子水平居中

     <p style="color:red">1.left:50%<br>
         2.margin-left:自己盒子宽度的一半&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-100px<br>
         垂直居中类似，先top:50%;再margin-top:自身高度的一半---负值
     </p>

  2. 定位的特殊特性

     + 行内元素添加绝对或者固定定位，可以直接设置高度和宽度
     + 块级元素添加绝对或者固定定位，如果不给高度和宽度，默认是内容的大小

  3. 脱标的盒子不会触发外边距塌陷

     浮动元素、绝对性定位元素都不会触发外边距合并的问题

  4. 绝对定位(固定定位)会完全压住盒子

     浮动元素不同，只会压住它下面的标准流的盒子，但是不会压住下面标准流里面的内容---文字，图片等

     原因在于浮动产生的最初目的是做文字环绕效果的，文字会围绕浮动元素。

#17.元素的显示与隐藏

本质：让一个元素在页面中隐藏或者显示出来          --广告

1. display显示隐藏

   display属性用于设置一个元素应如何显示

   + display: none; 隐藏对象

     <p style="color:red">隐藏后不再占有原来的位置</p>

   + dispay: block; 除了转换位块级元素之外，同时还有显示元素的意思

2. visibility显示隐藏

   + visibility：visible；  元素可视

   + visibility：hidden；元素隐藏

     <p style="color:red">隐藏后仍占有原来的位置</p>

3. overflow溢出显示隐藏

   overflow属性指定了如果内容溢出一个元素的框(超出其指定的高度和宽度)时，会发生什么    

   + overflow：visible；  溢出部分显示

   + overflow：hidden；  溢出部分隐藏

   + overflow：scroll；     溢出时溢出部分显示滚动条，不发生溢出时也显示滚动条

   + overflow：auto；     溢出时显示滚动条，不溢出时不显示滚动条

     <p style="color:red">有定位的盒子慎用overflow:hidden;它会隐藏多余的部分</p>

#18.精灵图

多个小图片集中到一张图片上，减少服务器请求次数，提高页面加载速度

+ 精灵图(sprites)的使用

  使用精灵图核心：

  1. 精灵技术主要针对于背景图片使用，就是将多个小背景图片整合到一张大图中。
  2. 这个大图叫做精灵图
  3. 移动背景图片位置，将需要的部分显示 在盒子中，此时可以使用background-position
  4. 移动的距离就是这个目标图片的X、Y坐标，
  5. 一般情况下都是往上往左移动，所以数值是负值
  6. 使用精灵图的时候需要精确测量，每个小背景图片的大小和位置

#19.字体图标--iconfont

主要用于显示网页中通用、常用的一些小图标

字体图标展示的是图标，本质属于字体

1. font文件夹放在html文件同目录下

2. 复制字体图标 

3. css引用

   ```
   @font-face {
     font-family: 'icomoon';
     src: url('fonts/icomoon.eot?5lma99');
     src: url('fonts/icomoon.eot?5lma99#iefix') format('embedded-opentype'),
     url('fonts/icomoon.ttf?5lma99') format('truetype'),
     url('fonts/icomoon.woff?5lma99') format('woff'),
     url('fonts/icomoon.svg?5lma99#icomoon') format('svg');
     font-weight: normal;
     font-style: normal;
     font-display: block;
   }
   ```

4. 容器声明字体

   font-family: 'icomoon';

+ 字体图标追加

#20.CSS三角

宽、高为0的div，一个边框实线，其余透明，即可生成三角

```html
 .box1 {
            width: 0;
            height: 0;
            /* border: 10px solid pink; */
            border-top: 10px solid pink;
            border-right: 10px solid red;
            border-bottom: 10px solid blue;
            border-left: 10px solid green;
        }
        .box2 {
            width: 0;
            height: 0;
            border: 50px solid transparent;
            border-left-color: pink;
            margin: 100px auto;
        }
```

#21.CSS用户界面样式

+ 鼠标样式

  li{course: 属性值}     设置或检索对象上移动的鼠标采用哪种系统预定义的光标形状

  ```
  default					默认
  pointer                 小手
  move					移动
  text					文本
  not-allowed				禁止
  ```

+ 轮廓线-----outline----表单文本框

  给表单添加outline:0;或者outline:none;样式后就可以去掉选中文本框默认的蓝色边框

+ 文本域禁止拖拽大小---resize

  textarea{resize: none;}

#22.vertical-align属性应用  

用于设置图片或者表单(行内块元素)和文字垂直对齐

vertical-align: baseline  |  top  |  middle  |  bottom

```
baseline       默认。元素放在父元素的基线上
top            把元素的顶端与行中最高元素的顶端对齐
middle		   把此元素放置在父元素的中部
bottom         把元素的顶端与行中最低的元素的顶端对齐
```

+ 解决图片底部默认空白的问题

  图片底侧会有一个空白间隙，原因是行内块元素默认与文字的基线对齐

  解决方法：

  + 给图片添加vertical-align:  middle  |  top  |  bottom  等
  + 把图片转换为块级元素  display：block;

#23.溢出的文字用省略号显示

+ 单行文本溢出显示省略号--必须满足三个条件

  1. 先强制一行内显示文本----不管能不能显示完，都要在一行内显示

     white-soace: nowrap；         默认normal自动换行

  2. 溢出的部分隐藏

     overflow：hidden;

  3. 文字溢出的时候用省略号代替

     text-overflow: ellipsis;

     ```
     white-soace: nowrap；
     overflow：hidden;
     text-overflow: ellipsis;
     ```

+ 多行文本溢出显示省略号

  多行文本溢出显示省略号，有较大兼容性问题，适合于webKit浏览器或移动端(移动端大部分是webKit内核)

  撒

  ```
  overflow：hidden;
  text-overflow: ellipsis;
  /* 弹性伸缩盒子模型显示 */
  display: -webkit-box;
  /* 限制在一个块元素显示的文本的行数 */
  -webkit-line-clamp: 3;
  /* 设置或检索伸缩盒对象的子元素的排列方式 */
  -webkit-box-orient: vertical;
  ```

#24.常见布局技巧

1. margin负值的运用

   避免盒子浮动时边框相邻使的边框变粗

   1. 让每个盒子margin往左侧移动一个边框的单位，正好压住相邻的边框
   2. 鼠标经过某一个盒子的时候，提高当前盒子的层级(给如果没有定位，则加相对定位--保留位置，如果有定位，则加z-index)

2. 文字围绕浮动元素

   利用浮动元素不会遮挡文字给一个盒子添加浮动，文字自动围绕盒子

3. 行内块的巧妙运用

4. CSS三角强化---可生成直角三角形

   ```
    .box1 {
               width: 0;
               height: 0;
               /* 把上边框宽度调大 */
               /* border-top: 100px solid transparent;
               border-right: 50px solid skyblue; */
               /* 左边和下边的边框宽度设置为0 */
               /* border-bottom: 0 solid blue;
               border-left: 0 solid green; */
              /* 1.只保留右边的边框有颜色 */
              border-color: transparent red transparent transparent;
               /* 2. 样式都是solid */
               border-style: solid;
               /* 3. 上边框宽度要大， 右边框 宽度稍小， 其余的边框该为 0 */
               border-width: 100px 50px 0 0 ;
   
           }
   ```

#25.网站favicon图标

1. 制作favicon图标-----比特虫：www.bitbug.net
2. favicon图标放在根目录下
3. HTML页面引入favicon图标  <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">

#26.网站TDK三大标签SEO优化

1. title网站标题

   网站名(产品名) - 网站的介绍（尽量不超过30个汉字）

2. description 网站说明

   简要说明网站主要做什么的

   <meta name="description" content="网站说明"/>

3. keywords关键字

   keywords是页面关键词，是搜索引擎的关注点之一

   keywords 最好限制在6-8个关键词，关键词之间用英文逗号分隔，

   <meta name="keywords" content="关键字"/>

#27.LOGO SEO优化

1. logo里面首先放一个<h1>标签，目的是为了提权，告知搜索引擎这个地方很重要
2. < h1>里面再放一个链接，可以返回首页的，把logo的背景图片给链接即可
3. 为了搜索引擎收录我们，链接里面要放文字(网站名称)，但是文字不要显示除来
   + 方法1：text-indent移动到盒子外面(text-indent:-9999px),然后overflow:hidden;-----淘宝的做法
   + 方法2：直接给font-size:0;就看不到文字了-------京东的做法
4. 最后给链接一个title属性，这样鼠标放到logo上就可以看到提示文字了

#28.注意点

+ <p style="color:red">实际使用中不直接使用链接a,而是使用li标签包含a  
      &lt;li&gt;&lt;a&gt;
  </p>

+ <p style="color:red;">导航栏&lt;li&gt;标签添加浮动，&lt;li&gt;标签是块级元素需要在同一行显示，导航栏里文字不一样多，最好给链接&lt;a&gt;左右padding程开盒子而不是指定宽度</p>

+ <p style="color:red;">浮动的盒子不会有外边距合并的问题

#29.CSS3的新特性

+ CSS3新增选择器

  1. 属性选择器

     利用属性选择器可以不用借助于类或ID选择器，根据元素特定的属性来选择元素

     input[value]                 选择具有value属性的所有input元素

     input[type="text"]           选择所有type属性值为text的input元素

     div[class^=icon]             选择所有class属性值以icon开头的的div元素

     section[class$=data]          选择所有class属性值以data结尾的section元素

     div[class*="con"]             选择所有class属性值包含con字符池的div元素

     <p style="color:red">类选择器、属性选择器、伪类选择器，权重为10</p>

  2. 结构伪类选择器

     结构伪类选择器主要根据文档结构来选择元素，长用于根据父级选择器里面打子元素

     ```python
     ul li:first-child{}              选择ul标签中第一个li子标签
     ul li:last-child{}				 选择ul标签中最后一个li子标签
     ul li:nth-child(n){}             选择ul标签中第n个li子标签
     ul li:first-of-type{}            选择ul标签中第一个li子标签        
     ul li:last-of-type{}             选择ul标签中最后一个li子标签
     ul li:nth-of-type(n){}           选择ul标签中第n个li子标签
     ```

     <p style="color:red;font-weight:700">nth-child&nbsp;&nbsp;执行时先把所有子元素排序，然后再根据序号查找，查找结果可能不是想要的<br>
     nth-of-child&nbsp;&nbsp;执行时先将指定查找的盒子进行排序，然后再进行匹配
     </p>


     **nth-child(n)选择某个父元素的一个或多个特定的子元素**
    
     <ul style="color:red;font-weight:700">
     	<li>n可以是数字，关键字和公式</li>	
         <li>n如果是数字，就是选择第n个子元素</li>
         <li>n可以是关键字：偶数--even、奇数--odd</li>
         <li>n可以是公式：常见的公式如下(如果是公式，则从0开始计算，但是第0个元素或者超出了元素的格式会被忽略)   参数n不能是其他字母<br>
             ol li:nth-child(n){}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;表示从第0个li标签开始，选择ol标签中的li标签,直到选择了ol标签中所有的li标签<br>
             2n&nbsp;&nbsp;----&nbsp;&nbsp;偶数<br>
             2n+1&nbsp;&nbsp;----&nbsp;&nbsp;奇数<br>
             5n&nbsp;&nbsp;----&nbsp;&nbsp;5、10、15···<br>
             n+5&nbsp;&nbsp;----&nbsp;&nbsp;从第五个开始(包括第五个)，直到最后<br>
             -n+5&nbsp;&nbsp;----&nbsp;&nbsp;前五个
     </ul>

  3. 伪元素选择器

     伪元素选择器可以帮助我们利用CSS创建新标签元素，而不需要HTML标签，从而简化HTML结构

     ::before  --------  在元素内部的前面插入内容

     ::after   ---------   在元素内部的后面插入内容

     + before和after创建一个元素，但是属于行内元素
     + 新创建的这个元素在文档树中是找不到的，所以我们称之为为伪元素
     + 语法：   element::before{}
     + before和after必须有content属性
     + before在父元素内容的前面创建元素，after在父元素内容的后面创建元素
     + 伪元素选择器和标签选择器一样，权重为1

+ CSS3盒子模型

  CSS3中可以通过box-sizing来指定盒子模型，有两个值：content-box、border-box

  1. box-sizing: content-box;   盒子大小为width+padding+border（以前默认的）
  2. box-sizing:border-box; 盒子大小为width

<p style="color:red;padding-left:30px;">如果盒子模型改为了box-size:border-box,那么padding和border就不会撑大盒子(嵌套padding和border不会超过width宽度)</p>

+ CSS3过渡

  过渡--transition可以不使用flash动画或者js的情况下，当元素从一种样式变换成为另一种样式时为元素添加效果

  过渡动画:是从一个状态渐渐的过渡到另外一个状态    常与hover连用

  语法：transition：要过渡的属性   花费时间  运动曲线  何时开始

  ​			多个属性利用逗号进行分隔

  属性：想要变化的CSS属性，宽度、高度、背景颜色、内外边距都可以，如果要所有的属性都变化过渡，写一个all就可以

  花费时间：单位是秒（必须写单位）  例：0.5s

  运动曲线：默认是ease(可以省略)

  何时开始：单位是秒（必须写单位）可以设置延迟出发时间 默认是0s(可以省略) 