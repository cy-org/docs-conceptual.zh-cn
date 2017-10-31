---
title: "路径标记语法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PathGeometry 类"
  - "XAML 中的特性用法"
  - "XAML 属性用法"
  - "PathGeometry 类"
  - "图形，PathGeometry 类"
  - "XAML 对象元素用法"
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 路径标记语法
路径中讨论了[形状和 WPF 概述中的基本绘图](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)和[Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)，但是，本主题详细介绍了功能强大且复杂的最小化语言，可用于指定路径几何图形更简洁使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  
  
 本主题包含以下各节：  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>先决条件  
 若要了解本主题，您应该熟悉的基本功能<xref:System.Windows.Media.Geometry>对象。 有关详细信息，请参阅[Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
<a name="abouthisdocument"></a>   
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>StreamGeometry 和 PathFigureCollection 微型语言  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供了两个类，提供用于描述几何路径微型语言︰ <xref:System.Windows.Media.StreamGeometry>和<xref:System.Windows.Media.PathFigureCollection>。  
  
-   您使用<xref:System.Windows.Media.StreamGeometry>设置类型的属性时的最小化语言<xref:System.Windows.Media.Geometry>，如<xref:System.Windows.UIElement.Clip%2A>属性<xref:System.Windows.UIElement>或<xref:System.Windows.Shapes.Path.Data%2A>属性<xref:System.Windows.Shapes.Path>元素。 下面的示例使用的特性语法创建<xref:System.Windows.Media.StreamGeometry>。  
  
     [!code-xml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
-   您使用<xref:System.Windows.Media.PathFigureCollection>最小化语言设置时<xref:System.Windows.Media.PathGeometry.Figures%2A>属性<xref:System.Windows.Media.PathGeometry>。 下面的示例使用属性语法来创建<xref:System.Windows.Media.PathFigureCollection>为<xref:System.Windows.Media.PathGeometry>。  
  
     [!code-xml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 正如您可以看到从上面的示例中，这两种微型语言都非常相似。 它是总能够使用<xref:System.Windows.Media.PathGeometry>在任何情况下，其中您可以使用<xref:System.Windows.Media.StreamGeometry>; 因此，您应使用哪一个？ 使用<xref:System.Windows.Media.StreamGeometry>时不需要在创建; 后修改的路径使用<xref:System.Windows.Media.PathGeometry>如果确实需要修改的路径。  
  
 有关详细信息之间的差异<xref:System.Windows.Media.PathGeometry>和<xref:System.Windows.Media.StreamGeometry>对象，请参阅[Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)。  
  
### <a name="a-note-about-white-space"></a>关于空白区域的注释  
 为简洁起见，单个空格遵循，语法部分中所示，但在任何位置显示一个空格，可能也是可接受多个空格。  
  
 两个数字相加实际上没有分离，从而可通过使用逗号或空格，但这只能完成时生成的字符串是明确。 例如，`2..3`实际上两个数字:"2。 和"。&3;"。 同样，`2-3`表示"2"和"-3"。 空格不是必需的前面或后面的命令，或者。  
  
### <a name="syntax"></a>语法  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]特性的用法语法<xref:System.Windows.Media.StreamGeometry>组成一个可选<xref:System.Windows.Media.FillRule>值和一个或多个图说明。  
  
|StreamGeometry XAML 属性用法|  
|-----------------------------------------|  
|`<`*object* *property* `="`[                                         `fillRule`]                                          `figureDescription`[                                         `figureDescription`]*`" ... />`|  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]特性的用法语法<xref:System.Windows.Media.PathFigureCollection>组成一个或多个图形说明。  
  
|PathFigureCollection XAML 属性用法|  
|-----------------------------------------------|  
|`<`*object* *property* `="` `figureDescription`[                                         `figureDescription`]*`" ... />`|  
  
|术语|描述|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=fullName><br /><br /> 指定是否<xref:System.Windows.Media.StreamGeometry>使用<xref:System.Windows.Media.FillRule>或<xref:System.Windows.Media.FillRule><xref:System.Windows.Media.PathGeometry.FillRule%2A>。<br /><br /> -   `F0`指定<xref:System.Windows.Media.FillRule>填充规则。<br />-   `F1`指定<xref:System.Windows.Media.FillRule>填充规则。<br /><br /> 如果省略此命令，则子路径使用的默认行为，即<xref:System.Windows.Media.FillRule>。 如果指定此命令，则必须首先将其放置。|  
|*figureDescription*|组成移动命令、 图绘制命令和可选的关闭命令。<br /><br /> `moveCommand` `drawCommands`  `[` `closeCommand` `]`|  
|*moveCommand*|移动命令，用于指定该图中的起始点。 请参阅[移动命令](#themovecommand)部分。|  
|*drawCommands*|一个或多个绘图命令，用于描述该图的内容。 请参阅[绘制命令](#drawcommands)部分。|  
|*closeCommand*|可选的关闭命令，用于关闭图形。 请参阅[关闭命令](#closecommand)部分。|  
  
<a name="themovecommand"></a>   
## <a name="move-command"></a>移动命令  
 指定一个新图形的起始点。  
  
|语法|  
|------------|  
|`M`*起始点*<br /><br /> - 或 -<br /><br /> `m`*起始点*|  
  
|术语|描述|  
|----------|-----------------|  
|*起始点*|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 一个新图形的起点。|  
  
 大写字符`M`指示`startPoint`绝对值; 小写`m`指示`startPoint`是以前的点的偏移量或 (0，0) 如果不存在。 如果在移动命令之后列出多个点，线条绘制连接这些点，即使您指定行命令。  
  
<a name="drawcommands"></a>   
## <a name="draw-commands"></a>绘制命令  
 绘制命令可以由多个形状命令组成。 可用的形状命令如下︰ 行、 水平线、 垂直线、 三次方贝塞尔曲线、 二次贝塞尔曲线、 平滑三次方贝塞尔曲线、 平滑的二次贝塞尔曲线和椭圆弧。  
  
 通过使用大写或小写字母输入每个命令︰ 大写字母表示绝对值和小写字母表示相对值︰ 该段的控点是相对于前面的示例终结点。 依次输入时的相同类型的多个命令，则可以省略重复的命令项中;例如，`L 100,200 300,400`等同于`L 100,200 L 300,400`。 下表描述了**移动**和**绘制**命令。  
  
### <a name="line-command"></a>行命令  
 创建当前点和指定的终结点之间的直线。                           `l 20 30`和`L 20,30`都属于有效**行**命令。  
  
|语法|  
|------------|  
|`L`*终结点*<br /><br /> - 或 -<br /><br /> `l`*终结点*|  
  
|术语|描述|  
|----------|-----------------|  
|*终结点*|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 线条的终点。|  
  
### <a name="horizontal-line-command"></a>水平线命令  
 创建一条水平线当前点和指定的 x 坐标之间。                          `H 90`是有效的水平线命令的示例。  
  
|语法|  
|------------|  
|`H`  *x*<br /><br /> - 或 -<br /><br /> `h`  *x*|  
  
|术语|描述|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=fullName><br /><br /> 直线终点的 x 坐标。|  
  
### <a name="vertical-line-command"></a>垂直线命令  
 创建当前点和指定的 y 坐标之间的竖直线。                          `v 90`是一种有效的垂直行命令。  
  
|语法|  
|------------|  
|`V`  *y*<br /><br /> - 或 -<br /><br /> `v`  *y*|  
  
|术语|描述|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=fullName><br /><br /> 直线终点的 y 坐标。|  
  
### <a name="cubic-bezier-curve-command"></a>三次方贝塞尔曲线命令  
 通过使用两个指定的控件点创建当前点和指定的终结点之间的三次方贝塞尔曲线 ( `controlPoint`1 和`controlPoint`2)。                          `C 100,200 200,400 300,200`是一个示例是有效的曲线命令。  
  
|语法|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> - 或 -<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|术语|描述|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 第一个控制点的曲线，它确定曲线的起始正切值。|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 第二个控制点的曲线，它确定曲线的结束正切值。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 绘制曲线将通过的点。|  
  
### <a name="quadratic-bezier-curve-command"></a>二次贝塞尔曲线命令  
 通过使用指定的控件点创建当前点和指定的终结点之间二次贝塞尔曲线 ( `controlPoint`)。                          `q 100,200 300,200`是有效的二次贝塞尔曲线命令的示例。  
  
|语法|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> - 或 -<br /><br /> `q` `controlPoint` `endPoint`|  
  
|术语|描述|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 曲线，它确定的起始和结束该曲线的切线的控制点。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 绘制曲线将通过的点。|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>平滑三次方贝塞尔曲线命令  
 创建当前点和指定的终结点之间的三次方贝塞尔曲线。 第一个控制点假定相对于当前点为前一个命令的第二个控制点的反射。 如果没有以前的命令或前一个命令不是一个三次方贝塞尔曲线命令或平滑三次方贝塞尔曲线命令，假定第一个控制点就是当前点。 第二个控制点，由指定的曲线，最终的控制点`controlPoint`2。 例如，`S 100,200 200,300`是一个有效的平滑三次方贝塞尔曲线命令。  
  
|语法|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> - 或 -<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|术语|描述|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 曲线，它确定曲线的结束正切值的控制点。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 绘制曲线将通过的点。|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>二次贝塞尔曲线命令  
 创建当前点和指定的终结点之间二次贝塞尔曲线。 假定控点相对于当前的点前面的命令的控制点的反射。 如果没有以前的命令或前一个命令不是一个二次贝塞尔曲线命令或平滑的二次贝塞尔曲线命令，控点就是当前的点。  
  
|语法|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> - 或 -<br /><br /> `t` `controlPoint` `endPoint`|  
  
|术语|描述|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 曲线，它确定的开始和曲线的切线的控制点。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 绘制曲线将通过的点。|  
  
### <a name="elliptical-arc-command"></a>椭圆弧命令  
 创建椭圆弧当前点和指定的终结点之间。  
  
|语法|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> - 或 -<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|术语|说明|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=fullName><br /><br /> 圆弧的 x 轴和 y 轴半径。|  
|`rotationAngle`|<xref:System.Double?displayProperty=fullName><br /><br /> 以度为单位的椭圆的旋转。|  
|`isLargeArcFlag`|如果弧线的角度应为 180 度设置为 1 或更高版本;否则，设置为 0。|  
|`sweepDirectionFlag`|如果弧绘制方向正角;，设置为 1否则，设置为 0。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=fullName><br /><br /> 绘制弧将通过的点。|  
  
<a name="closecommand"></a>   
## <a name="the-close-command"></a>关闭命令  
 结束当前图，并创建一条连接到该图中的起始点的当前点线。 此命令创建的最后一段与该图中的第一个段之间连线 （角）。  
  
|语法|  
|------------|  
|`Z`<br /><br /> - 或 -<br /><br /> `z`|  
  
<a name="pointsyntax"></a>   
## <a name="point-syntax"></a>点语法  
 描述一个点 x 和 y 坐标。  
  
|语法|  
|------------|  
|`x` `,` `y`<br /><br /> - 或 -<br /><br /> `x` `y`|  
  
|术语|描述|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=fullName><br /><br /> 点的 x 坐标。|  
|`y`|<xref:System.Double?displayProperty=fullName><br /><br /> 点的 y 坐标。|  
  
<a name="specialvalues"></a>   
## <a name="special-values"></a>特殊值  
 而不是标准的数值以外，还可以使用下列特殊值。 这些值是区分大小写。  
  
 无限  
 表示<xref:System.Double.PositiveInfinity?displayProperty=fullName>。  
  
 -Infinity  
 表示<xref:System.Double.NegativeInfinity?displayProperty=fullName>。  
  
 NaN  
 表示<xref:System.Double.NaN?displayProperty=fullName>。  
  
 此外可以使用科学记数法。 例如，`+1.e17`是有效的值。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Shapes.Path>   
 <xref:System.Windows.Media.StreamGeometry>   
 <xref:System.Windows.Media.PathGeometry>   
 <xref:System.Windows.Media.PathFigureCollection>   
 [形状和基本绘图中 WPF 概述](../../../../docs/framework/wpf/graphics-multimedia/shapes-and-basic-drawing-in-wpf-overview.md)   
 [Geometry 概述](../../../../docs/framework/wpf/graphics-multimedia/geometry-overview.md)   
 [操作指南主题](../../../../docs/framework/wpf/graphics-multimedia/geometries-how-to-topics.md)