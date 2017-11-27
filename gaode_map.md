# 高德地图开发文档整理 #

## 一、快速使用步骤 #

### 1.在页面中引入高德地图JavaScript API入口脚本 #
```
<script type="text/javascript" src="http://webapi.amap.com/maps?v=1.4.0&key=您申请的key值"></script> 
```

### 2.创建地图容器 #
在页面body里你想展示地图的地方创建一个div 容器，并指定id标识:
```
<div id="container"></div>  
```

### 3.给地图容器指定大小 #
可以使用CSS为地图容器设置合适的大小，比如:
```
<style>
  #container {width:300px; height: 180px; }  
</style>
```

### 4.创建地图 #
如上准备工作完成之后，就可以开始创建地图了。生成一副简单地图只需要一句代码，将我们刚刚创建的div的id传给Map的构造函数即可，
这个时候API将根据用户所在的城市自动进行地图中心点和级别的设定：
```
<script type="text/javascript">
  var map = new AMap.Map('container');
</script>
```

*此时打开html页面，就可以看到一张高德地图展现在你的html页面中*

## 二、进阶1 #
### 5.设定地图的中心点和级别 #

>zoom -> 级别  
>center -> 中心点  

我们一般需要给地图按需设定中心点和坐标等属性，这里可以通过两种方式，第一种，直接在地图初始化的时候传入相关属性，center属性
的值可以是经纬度的二元数组，也可以是AMap.LngLat对象，要求经度值在前，纬度值在后：

```
<script type="text/javascript">
    var map = new AMap.Map('container',{
        zoom: 10,
        center: [116.39,39.9]// center: new AMap.LngLat(116.39,39.9)
    });
</script>
```

也可以在地图初始化过后，任何需要的地方通过方法来改变地图的中心点和级别

```
<script type="text/javascript">
  var map = new AMap.Map('container');
  map.setZoom(10);
  map.setCenter([116.39,39.9]);
</script>
```

### 6.覆盖物 #

JavaScript API提供了丰富的覆盖物，比如Marker点标记、Polyline折线、Polygon多边形、Circle圆等。  
以Marker为例， 我们创建一个最简单的Marker，并将它添加到地图上：

```
var marker = new AMap.Marker({
  position: [116.480983, 39.989628],//marker所在的位置
  map:map//创建时直接赋予map属性
});
```

也可以在创建完成后通过setMap方法执行地图对象

```
var marker = new AMap.Marker({
  position: [116.480983, 39.989628],//marker所在的位置
});

marker.setMap(map);
```

