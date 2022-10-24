# 1. 安装

Build目录下Cesiumz复制到public目录下，导入

```
<script src="./Cesium/Cesium.js"></script>
<link rel="stylesheet" href="./Cesium/Widgets/widgets.css">
```

# 2.隐藏控件

```html
<!DOCTYPE html>
<html lang = "en">
<head>
    <meta charset = "UTF-8">
    <title>Title</title>
    <script src="./Cesium/Cesium.js"></script>
    <link rel="stylesheet" href="./Cesium/Widgets/widgets.css">
    <style>
        body,div{
            padding: 0;
            margin: 0;
        }
        /*隐藏下方版权信息*/ 
        .cesium-widget-credits{
            display:none !important;
        }
    </style>
</head>
<body>
    <div id="cesiumcontainer"></div>
    <script>
        let viewer=new Cesium.Viewer('cesiumcontainer',{
          geocoder:false, // 搜索框  false隐藏
          homeButton:false,// home按钮   false隐藏
          animation:false,// 动画控件
          fullscreenButton:false,//全屏按钮,底部
          sceneModePicker:false,//场景模式选择器 ,平面，球体
          timeline:false,//时间轴
          navigationHelpButton:false,// 导航提示,右上?
          baseLayerPicker:false,// 地图显示器
        })
    </script>
</body>
</html>

```

# 3.添加高德地图

1.iis发布api网页，IIS设置教程https://www.pageadmin.net/help/14.cshtml

2.添加高德地图的两种形式

3.投影方式webmercator

4.四叉树剖分

//卫片 " http://webst01.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}",  

//路网" https://wprd01.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=8&ltype=11"  

//地名" https://wprd01.is.autonavi.com/appmaptile?x={x}&y={y}&z={z}&lang=zh_cn&size=1&scl=1&style=8&ltype=4" 

//地名+路网 " http://webst01.is.autonavi.com/appmaptile?style=8&x={x}&y={y}&z={z}", 

//矢量切片风格 " http://webrd01.is.autonavi.com/appmaptile?&scale=1&lang=zh_cn&style=8&x={x}&y={y}&z={z}",

```js
imageryProvider:new Cesium.UrlTemplateImageryProvider({
            url:'http://webst01.is.autonavi.com/appmaptile?style=6&x={x}&y={y}&z={z}',
            minimumLevel:1,
            maximumLevel:18,
          })
        })
        //可同时添加两种风格地图,先添加的地图在底层，后添加的在上层
        let imageLayer=new Cesium.ImageryLayer(new Cesium.UrlTemplateImageryProvider({
          url:'http://webst01.is.autonavi.com/appmaptile?style=8&x={x}&y={y}&z={z}',
          minimumLevel:1,
          maximumLevel:18,
        }))
        viewer.imageryLayers.add(imageLayer)
```

# 4.地图定位

```js
// 地图定位
        viewer.camera.setView({
          destination: Cesium.Cartesian3.fromDegrees(117.28,31.86,10000), // 相机位置，不是地图位置,  经度、纬度、高度
          // 相机姿态
          orientation: {
            heading:Cesium.Math.toRadians(0.0),// 朝向
            pitch:Cesium.Math.toRadians(-90),//俯仰
            roll:0.0,// 滚转
        }
        })
        viewer.camera.flyTo({   // flyTo 地图慢慢移动到指定位置
          destination: Cesium.Cartesian3.fromDegrees(109,34,10000), // 相机位置，不是地图位置,  经度、纬度、高度
          // 相机姿态
          orientation: {
            heading:Cesium.Math.toRadians(0.0),// 朝向
            pitch:Cesium.Math.toRadians(-90),//俯仰
            roll:0.0,// 滚转
          },
          duration:10,// 单位 秒，移动到指定位置花费的时间
        })
```

# 5.坐标系统

