# ECharts学习

## 01快速上手

### 1.引入文件

### 2.准备盒子模型

### 3.实例化对象

### 4.准备配置项

### 5.将配置项设置给echarts实例

## 通用配置

### 标题 title

- 文字样式：textStyle
- 标题边框：borderWidth:5，borderColor，orderRadius
- 标题位置：left，top

### 提示框 tooltip

- 触发类型 trigger

	- item，axis

- 触发时机 triggerOn

	- mouseover，click

- 格式化 formatter

	- 字符串模版，回调函数

### 工具栏 toolbox

- 导出图片：saveAsImage
- 数据试图：dataView
- 动态类型切换：magicType
- 数据区域缩放：dataZoom
- 重置：restore

### 图例 legend

- data是一个数组，筛选多个系列：【‘语文’，‘数学’】
- legend中的data值需要和series数组中数值name值一致

## 02柱状图

### 基本设置

- 基本代码结构
- x轴和y轴数据
- series中的type设置bar

### 常见效果

- 标记：

	- 最值：markPoint
	- 平均值：markLine

- 显示：

	- 数值显示：label
	- 柱宽度：barWidth
	- 横向柱图：换x轴和y轴类型

## 03折线图

### 常见效果

- 线条控制：

	- 平滑 smooth
	- 风格：lineStyle

- 标记：

	- 最值：markPoint
	- 平均值：markLine
	- 标注区间：markArea
	- 填充风格：areaStyle

- 紧挨边缘：类目轴-boundaryGap：false
- 缩放：脱离0值比例-数值轴-scale：true
- 堆叠图：stack

## 04散点图

### 实现步骤

- Echarts 基本结构
- 二维数组
- series的type：scatter
- xAxis和yAxis的type：value
- 调整：脱离0值比例使用scale

### 常见效果

- 气泡效果

	- 散点大小不同：symbolSize
	- 散点颜色不同：itemStyle.color

- 涟漪动画效果

  1.type:'effectScatter', //涟漪动画
  2.showEffectOn:'emphasis',//时机选择 render,emphasis
  
  
## 05直角坐标系

### 网格：grid

1.grid显示show
2.grid边框：borderWidth，borderColor
3.grid的位置和大小：left，top，right，bottom，width，height

### 坐标轴axis

- 坐标轴分为x和y
- 一个grid中最多两中位置的x轴和y轴
- 坐标轴类型

	- value：数值轴，自动从series目标数据中读取
	- category：类目轴，该类型必须通过data设置类目数据

### 显示位置position

- xAxis：top，bottom
- yAxis：left，right

### 区域缩放dataZoom

- x轴和y轴都可以设置
- 类型：inside slider

### 

## 06饼图

### 基本饼图

- 基本的代码结构
- 数据是由name和value的对象的数组
- series中的type设置为pie
- 无需配置xAxis和yAxis

### 常见效果

- 显示数值：label.formatter
- 圆环：radius:['50%','75%']//第0个元素代表内圆半径，第1个元素外圆半径
- 南丁格尔图
- 选择效果selectedMode：multiple/single

## 07地图

### 基本实现步骤

- 1.ECharts最基本的代码结构
- 2.准备中国地图的矢量数据
- 3.使用Ajax获取数据
- 4.在Ajax的回调函数中注册地图矢量数据，Echarts.registerMap（'chinaMap'，矢量地图数据）
- 5.配置geo的type为'map'，map为 'chinaMap'

### 常见配置效果

- 缩放拖动：roam:true
- 名称显示：label.show:true
- 初始化缩放比例L：zoom:1
- 地图中心点：center:[87,43]
- 配置visualMap筛选

  visualMap:{
      min:0,
      max:300,
      inRange:{
          color:['white','red'], //控制颜色渐变
      },
      calculable:true
  }
  
### 地图与散点图结合

- 给series增加新的对象
- 准备散点数据，配置给series下的另一个对象
- 配置series下新对象的type值为effectScatter
- 指明散点图的坐标系统为geo :coordinateSystem:'geo'
- 调整涟漪动画效果

  rippleEffect:{
      scale:10//设置涟漪动画的比例
  }
  
## 08雷达图

### 实现步骤

- 基本代码结构
- 定义各个纬度的最大值
- 准备具体数据
-  将type的值设置为radar

### 常用配置

- 显示数值：label
- 配置雷达图最外层的图形： shape：circle/polygon
- 雷达图形成阴影的面积areaStyle: {}

## 09仪表盘

## 10七个表小结

### type类型

- bar
- line
-  scatter/effectScatter
- pie
- map
- radar
- gauge

### 显示

- 主题

	- 内置主题：light/dark
	- 自定义主题 

		- 1.在线编辑主题 https://www.echartsjs.com/theme-builder/
		- 2.下载主题的js文件
		- 3.在html中导入js文件
		- 4.在init方法中指明主题的名称

- 调色盘(就近原则)

	- 主题 ：init第二个参数自定义主题颜色
	- 全局：option下的color
	- 局部：series下的对象color
	- 颜色渐变

- 样式

	- 直接样式

		- itemStyle，textStyle，lineStyle，areaStyle，label

	- 高亮样式 在emphasis包括直接样式 

- 自适应

  window.onresize=mCharts.resize
  //-----
  window.onresize=function (){
      //调用
      mCharts.resize()
      // console.log('window.onresize...')
  }
  
	- 1.监听窗口大小变化事件
	- 2.在事件处理中调用Echarts实例对象的resize

### 动画

- 加载动画

	- 显示加载动画 mCharts.showLoading()
	- 隐藏加载动画mCharts.hideLoading()

- 增量动画  mCharts.setOption(option)

  //setOption 可以设置多次，
  //新旧option不是覆盖的关系，而是相互整合的关系
  //只需要考虑变化的部分
  
- 动画配置

	- 开启动画 animation
	- 动画时长animationDuration

## 11全局echarts对象常用

### Echarts全局对象

- init：1.初始化实例对象，2.定义主题
- registerTheme：注册主题
- registerMap:注册地图数据

  $.get('json/map/china.json',function (ret) {
      echarts.registerMap('chinaMap',ret)
  }
  
- connect图表关联

  echarts.connect([mCharts,mCharts2])//关联图
  
  
### echartsinstance对象

- setOption 1.设置或修改配置项和数据，2.可以多次调用setOption
- resize：重新计算和绘制图表

  window.onresize=mCharts.resize
  
- on/off
- dispatchAction触发图表行为，例如图例开关
- clear清空当前实例
- dispose销毁实例，销毁后实例无法再被使用

### 总结

- 显示相关

	- 主题
	- 调色盘
	- 样式
	- 自适应

- 动画相关

	- 加载动画
	- 增量动画

- 交互API

	- 全局E charts对象
	- echartsinstance对象的方法

