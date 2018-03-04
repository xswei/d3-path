# d3-path

在 2D canvas 中绘图时可以使用如下代码:

```js
function drawCircle(context, radius) {
  context.moveTo(radius, 0);
  context.arc(0, 0, radius, 0, 2 * Math.PI);
}
```

d3-path 模块可以将上述代码同时渲染到 [SVG](http://www.w3.org/TR/SVG/paths.html) 中。通过将 [CanvasPathMethods](http://www.w3.org/TR/2dcontext/#canvaspathmethods) [serializing(序列化)](#path_toString) 为 [SVG path data](http://www.w3.org/TR/SVG/paths.html#PathData) 实现。例如：

```js
var context = d3.path();
drawCircle(context, 40);
pathElement.setAttribute("d", context.toString());
```

因此只需要写一次绘图逻辑就可以在 Canvas 和 SVG 中同时使用。可以参考 [d3-shape](https://github.com/d3/d3-shape) 中的实际例子。

## Installing

NPM 安装：`npm install d3-path`. 也可以下载 [latest release](https://github.com/d3/d3-path/releases/latest). 此外还可以直接从 [d3js.org](https://d3js.org) 以 [standalone library](https://d3js.org/d3-path.v1.min.js) 或作为 [D3 4.0](https://github.com/d3/d3) 一部分直接载入. 支持 AMD, CommonJS 和最基本的标签引入，使用标签引入时会创建 `d3` 全局变量:

```html
<script src="https://d3js.org/d3-path.v1.min.js"></script>
<script>

var path = d3.path();
path.moveTo(1, 2);
path.lineTo(3, 4);
path.closePath();

</script>
```

[在浏览器中测试 d3-path](https://tonicdev.com/npm/d3-path)

## API Reference

<a name="path" href="#path">#</a> d3.<b>path</b>() [<>](https://github.com/d3/d3-path/blob/master/src/path.js "Source")

创建一个新的实现了 [CanvasPathMethods](http://www.w3.org/TR/2dcontext/#canvaspathmethods) 的路径序列化生成器。

<a name="path_moveTo" href="#path_moveTo">#</a> <i>path</i>.<b>moveTo</b>(<i>x</i>, <i>y</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L18 "Source")

移动到指定的点 ⟨*x*, *y*⟩。等价于 [*context*.moveTo](http://www.w3.org/TR/2dcontext/#dom-context-2d-moveto) 和 SVG 的 [“moveto” 命令](http://www.w3.org/TR/SVG/paths.html#PathDataMovetoCommands)。

<a name="path_closePath" href="#path_closePath">#</A> <i>path</i>.<b>closePath</b>() [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L21 "Source")

结束当前子路径并且自动将当前点和路径的初始点直接连接闭合。等价于 [*context*.closePath](http://www.w3.org/TR/2dcontext/#dom-context-2d-closepath) 和 SVG 的 [“closepath” 命令](http://www.w3.org/TR/SVG/paths.html#PathDataClosePathCommand).

<a name="path_lineTo" href="#path_lineTo">#</a> <i>path</i>.<b>lineTo</b>(<i>x</i>, <i>y</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L27 "Source")

从当前点画一条直线连接到指定的点 ⟨*x*, *y*⟩。等价于 [*context*.lineTo](http://www.w3.org/TR/2dcontext/#dom-context-2d-lineto) 和 SVG 的 [“lineto” 命令](http://www.w3.org/TR/SVG/paths.html#PathDataLinetoCommands).

<a name="path_quadraticCurveTo" href="#path_quadraticCurveTo">#</a> <i>path</i>.<b>quadraticCurveTo</b>(<i>cpx</i>, <i>cpy</i>, <i>x</i>, <i>y</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L30 "Source")

从当前点绘制一条二次 Bézier 曲线，终点为 ⟨*x*, *y*⟩，控制点为 ⟨*cpx*, *cpy*⟩。等价于 [*context*.quadraticCurveTo](http://www.w3.org/TR/2dcontext/#dom-context-2d-quadraticcurveto) 和 SVG 的 [quadratic Bézier curve 命令](http://www.w3.org/TR/SVG/paths.html#PathDataQuadraticBezierCommands).

<a name="path_bezierCurveTo" href="#path_bezierCurveTo">#</a> <i>path</i>.<b>bezierCurveTo</b>(<i>cpx1</i>, <i>cpy1</i>, <i>cpx2</i>, <i>cpy2</i>, <i>x</i>, <i>y</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L33 "Source")

从当前点绘制一条控制点为 ⟨*cpx1*, *cpy1*⟩ 和 ⟨*cpx2*, *cpy2*⟩、终点为 ⟨*x*, *y*⟩ 的三次 Bézier 曲线。等价于 [*context*.bezierCurveTo](http://www.w3.org/TR/2dcontext/#dom-context-2d-beziercurveto) 和 SVG 的 [cubic Bézier curve 命令](http://www.w3.org/TR/SVG/paths.html#PathDataCubicBezierCommands).

<a name="path_arcTo" href="#path_arcTo">#</a> <i>path</i>.<b>arcTo</b>(<i>x1</i>, <i>y1</i>, <i>x2</i>, <i>y2</i>, <i>radius</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L36 "Source")

根据指定的 *radius* 绘制圆弧，这个圆弧和两条线相切，其中一条为当前点和 ⟨*x1*, *y1*⟩ 的连线，另一条为 ⟨*x1*, *y1*⟩ 和 ⟨*x2*, *y2*⟩ 的连线。如果第一个切点不等于当前点，则会在当前点和第一个切点之间连线。等价于 [*context*.arcTo](http://www.w3.org/TR/2dcontext/#dom-context-2d-arcto) 和使用 SVG 的 [elliptical arc curve 命令](http://www.w3.org/TR/SVG/paths.html#PathDataEllipticalArcCommands).

<a name="path_arc" href="#path_arc">#</a> <i>path</i>.<b>arc</b>(<i>x</i>, <i>y</i>, <i>radius</i>, <i>startAngle</i>, <i>endAngle</i>[, <i>anticlockwise</i>]) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L84 "Source")

根据指定的中心 ⟨*x*, *y*⟩, *radius*, *startAngle* 和 *endAngle* 绘制一条弧线。如果 *anticlockwise* 为 true 则会以逆时针方向绘制；否则会以顺时针方向绘制。如果当前的点不等于圆弧的开始点则会从当前点连接一条直线到圆弧的开始点。等价于 [*context*.arc](http://www.w3.org/TR/2dcontext/#dom-context-2d-arc) 和使用 SVG 的 [elliptical arc curve 命令](http://www.w3.org/TR/SVG/paths.html#PathDataEllipticalArcCommands).

<a name="path_rect" href="#path_rect">#</a> <i>path</i>.<b>rect</b>(<i>x</i>, <i>y</i>, <i>w</i>, <i>h</i>) [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L122 "Source")

创建一个四个顶点为 ⟨*x*, *y*⟩, ⟨*x* + *w*, *y*⟩, ⟨*x* + *w*, *y* + *h*⟩, ⟨*x*, *y* + *h*⟩ 的子路径, 然后闭合子路径。等价于 [*context*.rect](http://www.w3.org/TR/2dcontext/#dom-context-2d-rect) 和使用 SVG 的 [“lineto” 命令](http://www.w3.org/TR/SVG/paths.html#PathDataLinetoCommands).

<a name="path_toString" href="#path_toString">#</a> <i>path</i>.<b>toString</b>() [<>](https://github.com/d3/d3-path/blob/master/src/path.js#L125 "Source")

返回当前 *path* 的序列化字符串，这个字符串符合 SVG 的 [path data specficiation(path 路径规范)](http://www.w3.org/TR/SVG/paths.html#PathData).
