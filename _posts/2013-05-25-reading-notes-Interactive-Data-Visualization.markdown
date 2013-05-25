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
使用非定量值作为输出的序数比例尺，非常适合苹果和桔子？？？

* d3.scale.category10() d3.scale.category20() d3.scale.category20b()和d3.scale.category20c()
能够输出10到20中类别颜色的预设序数比例尺

* d3.time.scale()
针对日期和时间值的一个比例尺方法，可以对日期刻度进行特殊处理
 