---
layout: post
title: 读书笔记 - 数据可视化实践
date: 2013-05-25 10:22
comments: true
categories: book
---

# 第1章 写在前面

## 1.1 数据为什么要可视化

更容易看懂

## 1.2 为什么要写代码

手工处理效率太低
和计算机沟通

## 1.3 为什么要交互

效果更好，鼓励参与

## 1.4 为什么要在web上

方便展示

## 1.5 这是一本什么书

基于D3，设计数据可视化，交互设计和web开发

## 1.6 读者是谁

懂一点基础知识的初学者

## 1.7 这不是什么书

隐藏一些技术细节，只讲基本概念

## 1.8 使用示例代码

git clone或下载zip包

## 1.9 thanks

# 第2章 D3简介

D3是一个JavaScript库，用于创建数据可视化图形
Data-Drive Documents 数据驱动的文档

## 2.1 D3能做什么

D3帮你生成和操作带数据的文档
1. 把数据加载到浏览器
2. 把数据绑定到文档中的元素，根据需要创建元素
3. 解析每个元素的范围资料，并为其设置相应的可视化属性，实现元素的变换(transform)
4. 响应用户输入实现元素的过渡(transitioning)

学习D3的过程，就是学习告诉它如何加载，绑定数据，变换和过渡元素的语法的过程
其中变换这一步最重要，因为映射关系在这一步起作用

## 2.2 D3不能做什么

1. D3不能生成预定义的或事先处理好的视觉图形，D3主要用户生成那些解释型的，而非探索型的可视化图形，探索性工具可以帮你发现数据中明显的，有价值的模型。探索型工具有Tableau和ggplot2
2. D3不支持旧版本的浏览器
3. D3的核心功能不处理位图格式的地图贴片，d3.geo.tile插件可以辅助，也可以使用其他工具，如Leaflet或Polymaps
4. D3不隐藏你的原始数据

## 2.3 起源与背景

1996年，NetScape在浏览器中内置了JavaScript

2005年，prefuse，使用java插件运行

2007年，Flare，使用ActionScript

2009年，Protovis，使用js

2011年，D3

## 2.4 替代方案

### 2.4.1 简易图表

DataWrapper

一个非常漂亮的在线服务，上传数据并快速生成图表后，就可以到处使用或将其嵌入在自己的站点中。这个服务最初定位于专栏记者，而实际上任何人都可以使用。DataWrapper在新版本浏览器中可以显示动态图表，而在旧版本浏览器中则显示静态图片。（太聪明了！）你也可以下载代码在自己的服务器上运行。地址：http://datawrapper.de/。

Flot

一个基于jQuery的绘图库，使用HTML的canvas元素，也支持旧版本浏览器（甚至IE6）。它支持有限的视觉形式（折线、散点、条形、面积），但使用很简单。地址：http://www.flotcharts.org/。

Google Chart Tools

由早期的Image Charts API发展而来的Google Chart Tools，可以用来生成不少标准的图表，也支持旧版本的IE。地址：https://developers.google.com/chart/。

gRaphaël

基于Raphaël（参见本节后面）的一个图表库，支持旧版本浏览器（包括IE6）。与Flot相比，它更灵活，而且据说还要更漂亮一些。地址：http://g.raphaeljs.com/。

Highcharts JS

JavaScript图表库，包含一些预定义的主题和图表。它在最新浏览器中使用SVG，而在旧版本IE（包括IE6及更新版本）中使用后备的VML。这个工具只对非商业用途免费。地址：http://www.highcharts.com/。

JavaScript InfoVis Toolkit

简称JIT，它提供了一些预设的样式可用于展示不同的数据，包括很多例子，而文档的技术味道太浓。如果你喜欢它的预设样式，可以选择它，但浏览器支持情况不太清楚。地址：http://philogb.github.com/jit/。

jqPlot

jQuery绘图插件，只支持一些简单的图表，适合不需要自定义样式的情况。jqPlot支持IE7及更新版本。地址：http://www.jqplot.com/。

jQuery Sparklines

可生成波形图的jQuery插件，主要是那些可以嵌在字里行间的小条形图、折线图、面积图。支持大多数浏览器，包括IE6。地址：http://omnipotent.net/jquery.sparkline/#s-about。

Peity

jQuery插件，可生成非常小的条形图、折线图和饼图，只支持较新版本的浏览器。再强调一遍，它能生成非常小又非常精致的小型可视化图表，可爱程度加10分。地址：http://benpickles.github.com/peity/。

Timeline.js

专门用于生成交互式时间线的一个库。不用编写代码，只用其代码生成器即可。定制的空间不大，但时间线可不是那么容易做的。Timeline.js只支持IE8及之后的版本。地址：http://timeline.verite.co/。

YUI Charts

雅虎YUI（Yahoo! User Interface Library）的Charts模块，可用于创建简单的图表，支持很多浏览器。地址：http://yuilibrary.com/yui/docs/charts/。

### 2.4.2 图谱可视化

所谓“图谱”，就是具有网络结构的数据（比如B连接到A，A连接到C）。

Arbor.js

基于jQuery的图谱可视化库。就算没用过它，也该看一看它的文档，连它的文档都是用这个工具生成的（可见它有多纯粹、多meta）。这个库使用了HTML的canvas元素，因此只支持IE9和其他较新的浏览器，当然也有一些针对旧版浏览器的后备措施。地址：http://arborjs.org/。

Sigma.js

一个非常轻量级的图谱可视化库。无论如何，你得看看它的网站，在页面上方的大图上晃几下鼠标，然后再看看它的演示。Sigma.js很漂亮，速度也快，同样使用canvas。地址：http://sigmajs.org/。

### 2.4.3 地图映射

我们要区分一下地图（全部内容都是地图）和地图映射（包括地理位置数据或地理数据，比如传统的地图）。D3本身也有很多地图映射功能，但下面这些工具最好你也了解一下。

Kartograph

Gregor Aisch开发的一个基于JavaScript和Python的非常炫的、完全使用矢量的库，它的演示是必看的。最好现在就去看一看。保证你从来没见过这么漂亮的在线地图。Kartograph支持IE7及更新版本。地址：http://kartograph.org/。

Leaflet

贴片地图的库，可以在桌面和移动设备上流畅地交互。它支持在地图贴片上显示一些SVG数据层。（参见Mike的演示“Using D3 with Leaflet”：http://bost.ocks.org/mike/leaflet/。) Leaflet支持IE6（勉强）或IE7（好得多），当然还有其他更新版本的浏览器。地址：http://leafletjs.com/。

Modest Maps

作为贴片地图库中的老爷爷，Modest Maps已经被Polymaps取代了，但很多人还是喜欢它，因为它体积小巧，又支持IE和其他浏览器的老版本。Modest Maps有很多版本，包括ActionScript、Processing、Python、PHP、Cinder、openFrameworks……。总之，它属于老当益壮那种。地址：http://modestmaps.com/。

Polymaps

显示贴片地图的库，在贴片上可以叠加数据层。Polymaps依赖于SVG，因此在较新的浏览器中表现很好。地址：http://polymaps.org/。

### 2.4.4 较原始的方案

以下工具跟D3有些类似，都提供了绘制图形的方法，但没有预定义的模板。如果你愿意从头开始，希望得到更大的自由度，可能会对它们感兴趣。

Processing.js

Processing的原生JavaScript实现，是新接触编程的艺术家和设计师的梦幻式编程语言。Processing是Java写的，因此Processing草图要在网页中显示通常要靠Java小程序。有了Processing.js，常规的Processing代码就可以在浏览器中直接运行了。由于使用canvas，所以只适合现代的浏览器。地址：http://processingjs.org/。

Paper.js

在canavs上渲染矢量图形的框架。同样，它的网站也堪称互联网上最漂亮的网站之一，它们的演示做得让人难以置信。（现在就去欣赏一下吧。）地址：http://paperjs.org/。

Raphaël

也是一个绘制矢量图形的库，受欢迎的原因是语法具有亲和力，而且支持老版本浏览器。地址：http://raphaeljs.com/。

### 2.4.5 三维图形

说来也怪，D3不擅长3D，因为浏览器从一开始就是二维的东西。但随着它对WebGL的支持越来越完善，在网页中显示3D图形也会渐渐成为一种趋势。

PhiloGL

专注于3D可视化的一个WebGL框架。地址：http://www.senchalabs.org/philogl/。

Three.js

能帮你生成任何3D场景的一个库，谷歌Data Arts团队出品。它的演示可以让人整整一天都沉浸其中，兴奋不已。地址：http://mrdoob.github.com/three.js/。

### 2.4.6 基于D3的工具

如果你使用D3，但又不想写代码，可以考虑下面这些基于D3的工具。

Crossfilter

一个可以操作大型、多元数据集的库，主要作者是Mike Bostock。非常适合把你的“大数据”塞到相对小的浏览器里，地址：http://square.github.com/crossfilter/。

Cubism

时间序列数据可视化的D3插件，也是Mike Bostock写的。（我非常喜欢其中的演示。）地址：http://square.github.com/cubism/。

Dashku

用于实时更新在线控制板和小部件的在线工具，作者是Paul Jensen。地址：https://dashku.com/。

dc.js

这里的“dc”是dimensional charting（维度图表）的简写，因为这个库是专门为探索大型、多维数据集而进行优化的。地址：http://nickqizhu.github.com/dc.js/。

NVD3

可重用的D3图表。NVD3提供了很多漂亮的示例，不用像在D3里那样编写代码就可以定制很多效果。地址：http://nvd3.org/。

Polychart.js

更多可重用的图表，可选择的图表类型非常之多。Polychart.js只对非商业用途免费。地址：http://polychart.com/。

Rickshaw

显示时间序列数据的一个工具包，提供了很多定制选项。地址：http://code.shutterstock.com/rickshaw/。

Tributary

实时测试D3代码的一个好工具，作者是Ian Johnson。地址：http://tributary.io/。

## 第3章 技术基础 ---- 跳过 ----

## 第4章 安装D3 ---- 跳过 ----

## 第5章 数据

数据就是结构化的信息，反映某些事实
文本数据

#### 5.1 生成页面元素

     d3.select('body').append('p').text('New paragraph!')

### 5.2 绑定数据

数据可视化就是把数据映射为图形
绑定的意思就是把数据附加后者关联到特定的元素，以便将来引用数据的值和应用映射规则

     selection.data()

     d3.csv('food.csv', function(data) {
          console.log(data);
     });

     d3.csv('food.csv', function(err, data) {
          if(err) throw err;
          console.log(data);
     });

     var dataset = [5, 10, 15, 20, 25];
     d3.select('body')
       .selectAll('p')
       .data(dataset)
       .enter()
       .append('p')
       .text('New Paragraph!');

### 5.3 使用自己的数据

     var dataset = [5, 10, 15, 20, 25];
     d3.select('body')
       .selectAll('p')
       .data(dataset)
       .enter()
       .append('p')
       .text(function(d) {
         return d;
       });


     var dataset = [5, 10, 15, 20, 25];
     d3.select('body')
       .selectAll('p')
       .data(dataset)
       .enter()
       .append('p')
       .text(function(d) {
         return d;
       })
       .style('color', function(d) {
         if(d > 15) {
           return 'red';
         } else {
           return 'black';
         }
       });

## 第6章 基于数据绘图

## 6.1 绘制DIV

柱形图(column chart)，矩形沿垂直方向度量的图形
条形图(bar chart)，矩形沿水平方向度量的图形

attr()方法可以设置DOM属性的值，比如class, id, src, width, alt等
classed()方法，快速的添加或删除元素的类
     .classed('bar', true) // 添加
     .classed('bar', false) // 删除

     <style type='text/css'>
     div.bar {
          display: inline-block;
          width: 30px;
          margin-right: 5px;
          background-color: teal;
     }
     </style>

     var dataset = [5, 10, 15, 20, 25];
     d3.select('body')
       .selectAll('p')
       .data(dataset)
       .enter()
       .append('div')
       .attr('class', 'bar')
       .style('height', function(d) {
         return d * 5 + 'px';
       });
     
数据驱动可视化

## 6.2 data()的魔力

     var dataset;

    dataset = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20].map(function(x) {
      return Math.random() * 30;
    });
    d3.select('body')
       .selectAll('p')
       .data(dataset)
       .enter()
       .append('div')
       .attr('class', 'bar')
       .style('height', function(d) {
         return d * 5 + 'px';
       });

## 6.3 绘制SVG

template

    var w = 500;
    var h = 500;

    var svg = d3.select('body')
                .append('svg')
                .attr('width', w)
                .attr('height', h);



    var dataset = [5, 10, 15, 20, 25];
    var circles = svg.selectAll('circle')
       .data(dataset)
       .enter()
       .append('circle');

    circles.attr('cx', function(d, i) {
      return (i * 50) + 25;
    })
    .attr('cy', h/2)
    .attr('r', function(d) {
      return d;
    });

    .attr('fill', 'yellow')
    .attr('stroke', 'orange')
    .attr('stroke-width', function(d) {
      return d/2;
    });

## 6.4 绘制条形图

    var w = 500;
    var h = 500;
    var padding = 1;

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var dataset = [5, 10, 15, 20, 25, 30, 35];
    var rects = svg.selectAll('rect')
      .data(dataset)
      .enter()
      .append('rect');

    rects.attr('x', function(d, i) {
      return i * (w / dataset.length);
    })
    .attr('y', function(d) {
      return h - d * 4;
    })
    .attr('width', w / dataset.length - padding)
    .attr('height', function(d) {
      return d * 4
    })
    .attr('fill', function(d) {
       return 'rgb(0, 0, ' + (d * 10) + ')';  
    });

    svg.select('circlr')
      .attr({
        cx: 0,
        cy: 0,
        fill: 'red'  
       });

双重编码
多值映射

加标签

     svg.selectAll('text')
      .data(dataset)
      .enter()
      .append('text')
      .text(function(d) {
        return d;
      })
      .attr('x', function(d, i) {
        return i * (w / dataset.length) + (w / dataset.length - padding) / 2;
      })
      .attr('y', function(d) {
        return h - d * 4  + 14;
      })
      .attr('font-family', 'sans-serif')
      .attr('font-size', '11px')
      .attr('fill', 'white')
      .attr('text-anchor', 'middle');

## 6.5 绘制散点图

条形图使用一维数据，散点图是在两个坐标上表现出两组对应值的常见图表

    var w = 500;
    var h = 500;
    var padding = 1;

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];

    svg.selectAll('circle')
      .data(dataset)
      .enter()
      .append('circle')
      .attr({
        cx: function(d) {
          return d[0];
        },
        cy: function(d) {
          return d[1];
        },
        r: function(d) {
          return Math.sqrt(h - d[1]);
        }
      });

    svg.selectAll('text')
      .data(dataset)
      .enter()
      .append('text')
      .text(function(d) {
        return d[0] + ', ' + d[1];
      })
      .attr({
        x: function(d) {
          return d[0];
        },
        y: function(d) {
          return d[1];
        },
        'font-family': 'sans-serif',
        'font-size': '11px',
        'fill': 'red'
      });

## 第7章 比例尺

比例尺是把一组输入域映射为输出范围的函数
D3的比例尺就是哪些你定义的带有参数的函数
线性比例尺
序数，对数，平方根比例尺

## 7.1 苹果和像素

     var dataset = [100, 200, 300, 400, 500];

## 7.2 值域和范围

比例尺的输入值域指可能的输入值范围
比例尺的输出范围指输出值的可能范围

输入 值域
输出 范围

## 7.3 归一化

归一化就是根据可能的最小值和最大值，把某个数值映射为介于0和1之间的一个新值的过程
对于线性比例尺，D3可以帮我们处理归一化过程中的数学计算，输入值根据值域先进行归一化，然后再把归一化之后的值对应到输出范围

## 7.4 创建比例尺

比例尺函数生成器`d3.scale`，如`d3.scale.linear()`
设置值域，`scale.domain([100, 500])`
设置输出范围，`scale.range([10, 350])`

可以使用链式语法
     var scale = d3.scale.linear()
          .domain([100, 500])
          .range([10, 350]);

     scale(100); // -> 10
     scale(300); // -> 180
     scale(500); // -> 350

## 7.5 缩放散点图

    var w = 500;
    var h = 200;
    var padding = 20;

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
      [410, 12], [475, 44], [25, 67], [85, 21], [220, 88],[600, 10]
              ];
    var xScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[0]
      })])
      .range([padding, w - padding * 2]);

    var yScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[1];
      })])
      .range([h - padding, padding]);

    var rScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[1];
      })])
      .range([2,5]);

    svg.selectAll('circle')
      .data(dataset)
      .enter()
      .append('circle')
      .attr({
        cx: function(d) {
          return xScale(d[0]);
        },
        cy: function(d) {
          return yScale(d[1]);
        },
        r: function(d) {
          return rScale(d[1]);
        }
      });

    svg.selectAll('text')
      .data(dataset)
      .enter()
      .append('text')
      .text(function(d) {
        return d[0] + ', ' + d[1];
      })
      .attr({
        x: function(d) {
          return xScale(d[0]);
        },
        y: function(d) {
          return yScale(d[1]);
        },
        'font-family': 'sans-serif',
        'font-size': '11px',
        'fill': 'red'
      });

## 7.7 其他方法
其他方法
`nice()`，告诉比例尺取得为`range()`设置的任何值域，把两端的值扩展到最接近的整数
`rangeRound()`，此方法代替`range()`后，则比例尺输出的所有值都会舍入到最接近的整数值
`clamp()`，默认情况下，线性比例尺可以返回指定范围之外的值，调用`clamp(true)`后，就可以强制素有输出值都位于指定的范围之内
要使用这些方法，只需使用链式语法即可

     var scale = d3.scale.linear()
          .domain([0.123, 4.567])
          .range([0, 500])
          .nice()

## 7.8 其他比例尺

* sqrt
平方根比例尺

* pow
幂比例尺

* log
对数比例尺

* quantize
输出范围为独立的值的线性比例尺，适合把数据分类的情形

* ordinal
使用非定量值作为输出的序数比例尺，非常适合苹果和桔子 (9.1节会解释)

* d3.scale.category10() d3.scale.category20() d3.scale.category20b()和d3.scale.category20c()
能够输出10到20中类别颜色的预设序数比例尺

* d3.time.scale()
针对日期和时间值的一个比例尺方法，可以对日期刻度进行特殊处理
 
## 第8章 数轴

## 8.1 数轴简介

D3的数轴也是由你来定义的函数，但与比例尺不同，调用数轴函数不会返回值，而是会生成数轴相关的可见元素，包括轴线，标签和刻度

数轴函数只适用于SVG图形
数轴是设计与定量比例尺(与序数比例尺相对)配合使用的

## 8.2 设定数轴

     svg.append('g')
          .call(d3.svg.axis()
          .scale(xScale)
          .orient('bottom'));

## 8.3 修整数轴

     .attr('class', 'axis')

     .axis path,
     .axis line {
         fill: none;
         stroke: black;
         shape-rendering: crispEdges;
     }

     .axis text {
         font-family: sans-serif;
         font-size: 11px;
     }

transform 变换
translation 平移

     .attr('transform', 'translate(0,' + (h - padding) + ')')

## 8.4 优化刻度

     .ticks(5)
不一定按照5来执行，确保设计的可伸缩性

## 8.5 垂直数轴

     var yAxis = d3.svg.axis()
          .scale(yScale)
          .orient('left')
          .ticks(5);

     svg.append('g')
          .attr('class', 'axis')
          .attr('transform', 'translate(' + padding + ',0)')
          .call(yAxis);

## 8.6 最后的润色

     //动态的随机生成的数据集
     var dataset = [];
     var numDataPoints = 50;
     var xRange = Math.random() * 1000;
     var yRange = Math.random() * 1000;
     for (var i = 0; i < numDataPoints; i++) {
         var newNumber1 = Math.floor(Math.random() * xRange);
         var newNumber2 = Math.floor(Math.random() * yRange);
         dataset.push([newNumber1, newNumber2]);
     }

## 8.7 为刻度标签定义样式

`tickFormat()`方法可以为数值应用不同的格式，比如保留小数点后三位数字，或显示为百分比值

     var formatAsPercentage = d3.format('.1%');
     xAxis.tickFormat(formatAsPercentage);

all the code

  <style type='text/css'>
  .axis path,
    .axis line {
      fill: none;
      stroke: black;
      shape-rendering: crispEdges;
    }

    .axis text {
      font-family: sans-serif;
      font-size: 11px;
    }
  </style>


    var w = 500;
    var h = 300;
    var padding = 30;

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
      [410, 12], [475, 44], [25, 67], [85, 21], [220, 88],[600, 10]
              ];

    var numDataPoints = 50;
    var xRange = Math.random() * 1000;
    var yRange = Math.random() * 1000;

    for(var i = 0; i< numDataPoints; i++) {
      var n1 = Math.floor(Math.random() * xRange);
      var n2 = Math.floor(Math.random() * yRange);
      dataset.push([n1, n2]);
    }

    var xScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[0]
      })])
      .range([padding, w - padding * 2]);

    var yScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[1];
      })])
      .range([h - padding, padding]);

    var rScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d[1];
      })])
      .range([2,5]);

    var xAxis = d3.svg.axis()
      .scale(xScale)
      .orient('bottom')
      .ticks(5);

    var yAxis = d3.svg.axis()
      .scale(yScale)
      .orient('left')
      .ticks(5);

    svg.selectAll('circle')
      .data(dataset)
      .enter()
      .append('circle')
      .attr({
        cx: function(d) {
          return xScale(d[0]);
        },
        cy: function(d) {
          return yScale(d[1]);
        },
        r: function(d) {
          return rScale(d[1]);
        }
      });

    svg.append('g')
      .attr('class', 'axis')
      .attr('transform', 'translate(0,' + (h - padding) + ')')
      .call(xAxis);

    svg.append('g')
      .attr('class', 'axis')
      .attr('transform', 'translate(' + padding + ',0)')
      .call(yAxis);

## 第9章 更新、过渡和动画

数据的变化需要通过更新来处理
视觉上的调整需要以过渡的形式展现，而过渡则使用动画

## 9.1 更新条形图

序数比例尺，序数，就是有固定顺序的一些类别，比如大一、大二、大三、大四等

     var xScale = d3.scale.ordinal()
          .domain(d3.range(dataset.length))
          .rangeRoundBands([0, w], 0.05);

线性比例尺，返回连续的范围
序数比例尺，使用离散范围值，输出值是事先确定好的，可以是数值，也可以不是

映射范围时，可以使用`range()`，也可以使用`rangeBands()`，后者接受一个最小值和一个最大值，然后根据输入值域的长度自动将其切分为相等的快或档，如`rangeBands([0, w])`

可以给`rangeBands()`传入第2个参数，指定档间距，比如0.2表示档间距为每一档宽度的20%
使用`rangeRoundBands()`，会将输出的值舍入为最接近的整数

    var w = 600;
    var h = 250;

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var dataset = [ 5, 10, 13, 19, 21, 25, 22, 18, 15, 13,
                                   11, 12, 15, 20, 18, 17, 16, 18, 23, 25 ];


    var xScale = d3.scale.ordinal()
      .domain(d3.range(dataset.length))
      .rangeRoundBands([0, w], 0.05);

    var yScale = d3.scale.linear()
      .domain([0, d3.max(dataset)])
      .range([0, h]);

    var rects = svg.selectAll('rect')
      .data(dataset)
      .enter()
      .append('rect')
      .attr('x', function(d, i) {
        return xScale(i);
      })
      .attr('y', function(d) {
        return h - yScale(d);
      })
      .attr('width', xScale.rangeBand())
      .attr('height', function(d) {
        return yScale(d)
      })
      .attr('fill', function(d) {
         return 'rgb(0, 0, ' + (d * 10) + ')';
      });

    svg.selectAll('text')
      .data(dataset)
      .enter()
      .append('text')
      .text(function(d) {
        return d;
      })
      .attr('x', function(d, i) {
        return xScale(i) + xScale.rangeBand() / 2;
      })
      .attr('y', function(d) {
        return h - yScale(d) + 14;
      })
      .attr('font-family', 'sans-serif')
      .attr('font-size', '11px')
      .attr('fill', 'white')
      .attr('text-anchor', 'middle');

## 9.2 更新数据

监听事件，修改dataset，修改属性，比如y, height等

     d3.select('p')
       .on('click', function() {
         dataset = [ 11, 12, 15, 20, 18, 17, 16, 18, 23, 25,
           5, 10, 13, 19, 21, 25, 22, 18, 15, 13 ];
         svg.selectAll('rect')
           .data(dataset)
           .attr({
             y: function(d) {
               return h - yScale(d);
             },
             height: function(d) {
               return yScale(d);
             }
           })
         .attr('fill', function(d) {
           return 'rgb(0, 0, ' + (d * 10) + ')';
         });

         svg.selectAll('text')
           .data(dataset)
           .text(function(d) {
             return d;
           })
           .attr({
             x: function(d, i) {
               return xScale(i) + xScale.rangeBand() / 2;
             },
             y: function(d) {
               return h - yScale(d) + 14;
             }
           });
       });

## 9.3 过渡动画

在选择元素之后，改变属性之前加上`.transition()`即可

### 持续时间
`.duration(1000)`，放在`transition()`之后即可

### 缓动函数
控制动画速度的变化，`ease()`方法，参数默认是`"cubic-in-out"`，还可以是`"linear"`，`"poly"`，`"quad"`，`"cubic"`，`"circle"`，`"bounce"`等，放在`duration()`之前之后都可以

### 延迟时间
`delay()`方法用于指定过渡动画什么时间开始，`delay(1000)`创建一个1000毫秒的静态延迟
动态延迟，传递一个匿名函数，返回不同的值

     .delay(function(d, i) {
         return i / dataset.length * 1000;  // <-- 这里的代码是关键
     })

使用了`delay()`，则`duration()`设定的是每个元素的动画持续时间，不是总共的持续时间，如果数据器里有很多元素，那么动画整体运行时间就太长了，所以需要根据数据集的长度动态调整延迟时间

### 更新数轴
选择当前数轴，初始化一个过渡，设定过渡的持续时间，调用适当的数轴生成器

### 在过渡开始和结束时执行操作
`each()`方法

     .each('start', function() {
          d3.select(this)
               .attr('fill', 'magenta')
               .attr('r', 3);
     })

可以在过渡的外部使用`each()`，针对每个元素执行任何代码，可以忽略`"start"`或`"end"`参数，只传入匿名方法即可

### 剪切路径
在剪切路径中包含可见元素:
剪切路径(clipping path)类似PhotoShop里的蒙版，`cliPath`本身不可见，但它可以包含可见的元素

使用剪切路径的步骤如下:
* 定义`cliPath`并给它一个ID
* 在这个`cliPath`中放一个可见的元素
* 在需要使用蒙版的元素上添加一个对`cliPath`的引用

    svg.append('clipPath')
      .attr('id', 'chart-area')
      .append('rect')
      .attr('x', padding)
      .attr('y', padding)
      .attr('width', w - padding * 3)
      .attr('height', h - padding * 2);

     svg.append('g')
      .attr('id', 'circles')
      .attr('clip-path', 'url(#chart-area)')
      .selectAll('circle')
      .data(dataset)
      .enter()
      .append('circle')
      .attr({
        cx: function(d) {
          return xScale(d[0]);
        },
        cy: function(d) {
          return yScale(d[1]);
        },
        r: function(d) {
          return 2;
        }
      });

## 9.4 其他数据更新方式

### 9.4.1 添加值

1. 选择
`select()`和`selectAll()`返回DOM元素
`data()`方法返回一个元素集，称为更新元素集
     
     dataset.push(111);
     var bars = svg.selectAll('rect')
          .data(dataset);

2. 加入
修改数据但是数据集的长度不变时，不用更新元素集，只要重新绑定数据，并将新值反映到新属性值上即可

     bars.enter()
          .append('rect')
          .attr({
               x: function() {}, // func
               y: function() {}  //xxx
          });

`bars`中保存着更新元素集(所有的元素)，`enter()`会从中提取出新加入的元素

3. 更新

     bars.transition()
          .duration(500)
          .attr({x: function() {}, y: function() {}});

### 9.4.2 删除值

和`enter()`方法对应，使用`exit()`方法退出元素

1. 退出
     bars.exit()
          .transition()
          .duration(500)
          .attr('x', w)
          .remove();

2. 温和退出
先执行过渡然后调用`remove()`方法把元素删除
使用`shift()`方法移除了`dataset`中的第1个元素，但是在条形图中，确实最后一个条形被移除，这是因为数据与条形的一致性(目标一致性)出了问题

### 9.4.3 通过键链接数据

调用`data()`方法时，会发生数据链接，默认链接是按照索引顺序，就是第1个值绑定到元素的第1个DOM元素，第2个值绑定到第2个DOM元素等等
定义键函数，即可指定数据和DOM的对应关系

1. 准备数据

      var dataset = [{ key: 0, value: 5},
          { key: 1, value: 10},
          { key: 2, value: 15}];

2. 更新所有引用
以前使用`d`的地方，现在就要使用`d.value`了
修改其他函数，添加匿名函数
      d3.max(dataset) ->
      d3.max(dataset, function(d) { return d.value;});

3. 键函数
定义键函数

      var key = function(d) { return d.key; }
        .data(dataset) ->
        .data(dataset, key)

4. 退出过渡
      bars.exit()
          .transition()
          .duration(500)
          .attr('x', -xScale.rangeBand())
          .remote();

### 9.4.4 添加和删除组合拳

     var lastKeyValue = dataset[dataset.length - 1].key;
     dataset.push({
        key: lastKeyValue + 1,
        value: newNumber
    });

### 9.4.5 简要回顾

* `data()`把数据绑定到元素，但也会返回更新元素
* 更新元素集可能包含加入和退出元素，这两个元素集可以通过`enter()`和`exit()`方法得到
* 数据值比元素多的情况下，加入元素集会引用尚不存在的占位元素
* 在元素比数据值多的情况下，退出元素集会引用没有对应数据的元素
* 数据联接用于确定数据值怎么与元素匹配
* 默认情况下，数据联接按照索引进行
* 可以指定键函数，修改数据联接方式

# 第10章 交互式图表

## 10.1 绑定事件监听器
     s3.select('p').on('click', function() {});

## 10.2 什么是行为

     svg.selectAll('rect')
          .data(dataset)
          .enter()
          .append('rect')
          .on('click', function(i, d) {
               // xxx
          });

### 悬停高亮

使用CSS控制:

     rect:hover {
          fill: orange;
     }
     rect {
          -moz-transitino: all 0.3s;
          -o-transition: all 0.3s;
          -webkit-trnasition: all 0.3s;
          transition: all 0.3s;
     }

使用js控制:

     .on('mouseover', function() {
          d3.select(this)
               .attr('fill', 'orange');
     })
     .on('mouseout', function(d) {
          d3.selet(this)
               .attr('fill', 'rgb(0, 0,' + (d * 10) + ')');
     });
     
加上过渡:

     .on('mouseout', function(d) {
          d3.selet(this)
               .transition()
               .duration()
               .attr('fill', 'rgb(0, 0,' + (d * 10) + ')');
     });

元素重叠:

     svg text {
          pointer-events: none;
     }
或者

     svg.append('text')
          .style('pointer-events', 'none');

## 10.3 分组SVG元素

使用`g`分组的元素，被包含的元素触发了事件，`g`元素的事件监听器也会被触发

### 单击排序

    var sortOrder = false;

    function sortBars() {
      sortOrder = !sortOrder;
      svg.selectAll('rect')
        .sort(function(a, b) {
          if(sortOrder) {
            return d3.ascending(a.value, b.value);
          } else {
            return d3.descending(a.value, b.value);
          }
        })
        .transition()
        .delay(function(d, i) {
          return i * 50;
        })
        .duration(1000)
        .attr('x', function(d, i) {
          return xScale(i);
        });
      svg.selectAll('text')
        .sort(function(a, b) {
          if(sortOrder) {
            return d3.ascending(a.value, b.value);
          } else {
            return d3.descending(a.value, b.value);
          }
        })
        .transition()
        .delay(function(d, i) {
          return i * 50;
        })
        .duration(1000)
        .attr('x', function(d, i) {
          return xScale(i) + xScale.rangeBand() / 2
        });
    }

## 10.4 提示条

## 10.4.1 浏览器默认提示条

加上title属性即可

    .append("title")
    .text(function(d) {
          return "This value is " + d;
    });

## 10.4.2 SVG元素提示条

`mouseover`事件时，动态创建标签，`mouseout`事件时，将标签删除；或者预生成所有标签，然后根据悬停状态切换显示和隐藏属性；再或者只创建一个标签，然后根据需要显示/隐藏并改变其位置

## 10.4.3 HTML的div提示条

HTML：
     <div id="tooltip" class="hidden"]]>
        <p><strong>Important Label Heading</strong></p>
        <p><span id="value"]]>100</span>%</p>
     </div>

  样式:

     #tooltip {
          position: absolute;
          width: 200px;
          height: auto;
          padding: 10px;
          background-color: white;
          -webkit-border-radius: 10px;
          -moz-border-radius: 10px;
          border-radius: 10px;
          -webkit-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
          -moz-box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
          box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.4);
          pointer-events: none;
       }

       #tooltip.hidden {
          display: none;
       }

       #tooltip p {
          margin: 0;
          font-family: sans-serif;
          font-size: 16px;
          line-height: 20px;
       }
代码：
     .on("mouseover", function(d) {

          //取得条形的x/y值，增大后作为提示条的坐标
          var xPosition = parseFloat(d3.select(this).attr("x")) + xScale.rangeBand() / 2;
          var yPosition = parseFloat(d3.select(this).attr("y")) / 2 + h / 2;

          //更新提示条的位置和值
          d3.select("#tooltip")
            .style("left", xPosition + "px")
            .style("top", yPosition + "px")
            .select("#value")
            .text(d);

          //显示提示条
          d3.select("#tooltip").classed("hidden", false);

      })

     .on("mouseout", function() {

         //隐藏提示条
         d3.select("#tooltip").classed("hidden", true);

     })

## 10.5 适应触摸设备

iOS和Android设备上的浏览器能够自动将触摸时间转换为鼠标事件，代码基本上可以用，但是D3不能自动处理多点触摸事件
D3提供了`d3.touches`的API，可以按需使用

## 10.6 更进一步

绑定数据，基于数据生成元素并设定样式，创建比例尺和绘制数轴，根据数据修改已有元素，实现动画过滤，实现交互

# 第11章 布局

D3的布局方法:

* Bundle: 把霍尔顿的分层捆绑算法应用到连线
* Chord: 根据矩阵关系生成弦形图
* Cluster: 聚集实体生成系统树图
* Force: 根据物理模拟定位链接的节点
* Hierarchy: 派生自定义的系统布局实现
* Histogram: 基于量化的分组计算数据分布
* Pack: 基于递归原型填充产生分层布局
* Partition: 递归细分节点数，呈射线或冰挂状
* Pie: 计算一系列堆叠的条形或面积图的基线
* Stack: 计算一系列堆叠的条形或面积图的基线
* Tree: 计算一系列堆叠的条形或面积图的基线
* Tree: 整齐的定位树节点
* Treemap: 基于递归空间细分来显示节点树



## 11.1 饼图布局

    var w = 300;
    var h = 300;

    var outerRadius = w / 2;
    var innerRadius = 0;
    var arc = d3.svg.arc()
      .innerRadius(innerRadius)
      .outerRadius(outerRadius);

    var dataset = [5, 10, 20, 45, 6, 25];
    var pie = d3.layout.pie();
    var color = d3.scale.category10();

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var arcs = svg.selectAll('g.arc')
      .data(pie(dataset))
      .enter()
      .append('g')
      .attr('class', 'arc')
      .attr('transform', 'translate(' + outerRadius + ',' + outerRadius + ')');

    arcs.append('path')
    .attr('fill', function(d, i) {
      return color(i);
    })
    .attr('d', arc);

    arcs.append('text')
    .attr('transform', function(d) {
      return 'translate(' + arc.centroid(d) + ')';
    })
    .attr('text-anchor', 'middle')
    .text(function(d) {
      return d.value;
    })

## 11.2 堆叠布局

    var w = 300;
    var h = 300;

    var outerRadius = w / 2;
    var innerRadius = 0;
    var arc = d3.svg.arc()
      .innerRadius(innerRadius)
      .outerRadius(outerRadius);

    var dataset = [
        { apples: 5, oranges: 10, grapes: 22 },
        { apples: 4, oranges: 12, grapes: 28 },
        { apples: 2, oranges: 19, grapes: 32 },
        { apples: 7, oranges: 23, grapes: 35 },
        { apples: 23, oranges: 17, grapes: 43 }
    ];
    // 上面的数据需要转换为下面这样
    var dataset = [
        [
                { x: 0, y: 5 },
                { x: 1, y: 4 },
                { x: 2, y: 2 },
                { x: 3, y: 7 },
                { x: 4, y: 23 }
        ],
        [
                { x: 0, y: 10 },
                { x: 1, y: 12 },
                { x: 2, y: 19 },
                { x: 3, y: 23 },
                { x: 4, y: 17 }
        ],
        [
                { x: 0, y: 22 },
                { x: 1, y: 28 },
                { x: 2, y: 32 },
                { x: 3, y: 35 },
                { x: 4, y: 43 }
        ]
    ];

    var stack = d3.layout.stack();
    stack(dataset);

    var xScale = d3.scale.ordinal()
      .domain(d3.range(dataset[0].length))
      .rangeRoundBands([0, w], 0.05);
    var yScale = d3.scale.linear()
      .domain([0, d3.max(dataset, function(d) {
        return d3.max(d, function(d) {
          return d.y0 + d.y;
        });
      })
    ])
    .range([0, h]);

    var colors = d3.scale.category10();

    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var groups = svg.selectAll('g')
      .data(dataset)
      .enter()
      .append('g')
      .style('fill', function(d, i) {
        return colors(i);
      });

    var rects = groups.selectAll('rect')
      .data(function(d) {
        return d;
      })
      .enter()
      .append('rect')
      .attr('x', function(d, i) {
        return xScale(i);
      })
      .attr('y', function(d, i) {
        return yScale(d.y0);
      })
      .attr('height', function(d) {
        return yScale(d.y);
      })
      .attr('width', xScale.rangeBand());

`ordinal`比例尺是离散的，接收固定的数组，作为x轴的比例尺

## 11.3 力导向布局


    var w = 300;
    var h = 300;

    var dataset = {
                    nodes: [
                         { name: "Adam" },
                         { name: "Bob" },
                         { name: "Carrie" },
                         { name: "Donovan" },
                         { name: "Edward" },
                         { name: "Felicity" },
                         { name: "George" },
                         { name: "Hannah" },
                         { name: "Iris" },
                         { name: "Jerry" }
                    ],
                    edges: [
                         { source: 0, target: 1 },
                         { source: 0, target: 2 },
                         { source: 0, target: 3 },
                         { source: 0, target: 4 },
                         { source: 1, target: 5 },
                         { source: 2, target: 5 },
                         { source: 2, target: 5 },
                         { source: 3, target: 4 },
                         { source: 5, target: 8 },
                         { source: 5, target: 9 },
                         { source: 6, target: 7 },
                         { source: 7, target: 8 },
                         { source: 8, target: 9 }
                    ]
               };

    var force = d3.layout.force()
      .nodes(dataset.nodes)
      .links(dataset.edges)
      .size([w, h])
      .linkDistance([50])
      .charge([-100])
      .start();

    var colors = d3.scale.category10();
    var svg = d3.select('body')
      .append('svg')
      .attr('width', w)
      .attr('height', h);

    var edges = svg.selectAll('link')
      .data(dataset.edges)
      .enter()
      .append('line')
      .style('stroke', '#ccc')
      .style('stroke-width', 1);

    var nodes = svg.selectAll('circle')
      .data(dataset.nodes)
      .enter()
      .append('circle')
      .attr('r', 10)
      .style('fill', function(d, i) {
        return colors(i);
      })
      .call(force.drag);

    force.on('tick', function() {
      edges.attr('x1', function(d) {
        return d.source.x;
      })
      .attr('y1', function(d) {
        return d.source.y;
      })
      .attr('x2', function(d) {
        return d.target.x;
      })
      .attr('y2', function(d) {
        return d.target.y;
      });

      nodes.attr('cx', function(d) {
        return d.x;
      })
      .attr('cy', function(d) {
        return d.y;
      });
    });

# 第12章 地图

## 12.1 JSON与GeoJSON

经度和纬度

* 经度，纵向，南北走向的
* 纬度，横向，东西走向的

## 12.2 路径

     var path = d3.geo.path();
     svg.selectAll('path')
          .data(json.features)
          .enter()
          .append('path')
          .attr('d', path);

## 12.3 投影

投影是一种折中算法，把3D空间映射到2D平面的方法
     
     var projection = d3.geo.albersUsa()
                      .translate([w/2, h/2])
                      .scale([500]);

## 12.4 等值区域

不同的区域填充了不同的值或颜色，以反映关联数据值的地图

     var color = d3.scale.quantize()
                    .range(["rgb(237,248,233)", "rgb(186,228,179)",
                    "rgb(116,196,118)", "rgb(49,163,84)","rgb(0,109,44)"]);

## 12.5 添加定位点

二维比例尺方法`projection()`方法

     svg.selectAll("circle")
    .data(data)
    .enter()
    .append("circle")
    .attr("cx", function(d) {
            return projection([d.lon, d.lat])[0];
    })
    .attr("cy", function(d) {
            return projection([d.lon, d.lat])[1];
    })
    .attr("r", 5)
    .style("fill", "yellow")
    .style("opacity", 0.75);

## 12.6 取得和解析地图数据

### 12.6.1 查找shapefile文件

在线地图和可视化流行之前的一种文件，不是纯文本数据

### 12.6.2 选择解析度

shapefile都是矢量数据，包含了地理信息的详尽程度或粒度

### 12.6.3 简化数据文件

使用工具简化数据文件

### 12.6.4 转化为GeoJSON

使用`ogr2ogr`将shapefile转化为GeoJSON文件

# 第13章 导出文件

## 13.1 导出位图

截图就好了。。

## 13.2 导出pdf

浏览器的打印后者其他工具

## 13.3 导出SVG

到浏览器里复制SVG代码出来保存成`.svg`即可

# 扩展阅读

## 网站


   * d3js.org
学习D3一切的起点。
   * github.com/mbostock/d3/wiki/Gallery
D3的代码库，包含数以百计的示例。把你作品也加进去！
   * bl.ocks.org/mbostock
例子更多，而且都是Mike Bostock亲手编写的，每一个都反映了D3的一项功能。
   * github.com/mbostock/d3/wiki/API-Reference
D3 API参考，包括所有方法和参数的详细说明。
   * stackoverflow.com/questions/tagged/d3.js
遇到什么难题的时候，可以在StackOverflow上用d3.js标签提个问。
   * groups.google.com/forum/?fromgroups#!forum/d3-js
鱼龙混杂的D3 Google Group。在这里可以看到最新的项目和进展。（技术问题一定到StackOverflow上问。）
   * bl.ocks.org
用于发表托管在GitHub Gist中的代码，作者是Mike Bostock。非常适合快速与他人分享你的代码，比如在StackOverflow上寻求帮助的时候，或者显摆你在Google Group上挖到的新玩艺儿的时候，都可以用到它。
   * blog.visual.ly/creating-animations-and-transitions-with-d3-js/
Jérôme Cukier写的一个关于使用D3来创建动画和过渡效果的教程，极其精彩，有很多当场可交互的例子。
   * d3noob.org
新的介绍D3技巧和经验的资源网站，不错。
   * tributary.io
用于试验D3代码的一个实时编码环境，作者是Ian Johnson。
   * D3 Plug-ins（https://github.com/d3/d3-plugins）
包含扩展D3功能的所有官方插件，以备不时之需。

## Twitter


   * @mbostock
Mike Bostock，了解D3的进展和《纽约时报》新的可视化项目。
   * @jasondavies
Jason Davies，了解地理和数学映射的各种实验方法。
   * @d3visualization
Christophe Viau，了解D3世界的各种更新。
   * @enjalot
Ian Johnson，了解新编码工作和技术，还有视频教程。
   * @syntagmatic
Kai Chang，了解非常多的D3设计方法，难以计数。
   * @jcukier
Jérôme Cukier，了解极具创造性的可视化项目，还有关于流程每一步的关键提示。
   * @darkgreener
Anna Powell-Smith，了解探索个人数据的交互可视化项目，非常漂亮。
   * @vlandham
Jim Vallandingham，了解做项目过程中的注意事项，还有不错的教程。
   * @alignedleft
Scott Murray，了解本书勘误、更新和修订，以及未来的数据驱动的项目。


哇，看完了。。  
2013.6.5 21：49