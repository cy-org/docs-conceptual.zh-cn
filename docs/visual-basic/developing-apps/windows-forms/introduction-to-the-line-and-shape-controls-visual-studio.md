---
title: "Line 和 Shape 控件简介 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Line 控件, 概述"
  - "文本行, 绘图"
  - "Shape 控件, 概述"
  - "形状, 绘图"
ms.assetid: 5c4e8b1a-0733-4020-af6c-f582f4026728
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Line 和 Shape 控件简介 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Visual Basic Power Pack Line 和 Shape 控件由三个图形控件组成，使您可以在窗体和容器上绘制直线和形状。  <xref:Microsoft.VisualBasic.PowerPacks.LineShape> 控件用于绘制水平线、垂直线和对角线。  <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> 控件用于绘制圆形和椭圆形，<xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> 控件用于绘制矩形和正方形。  
  
## Line 和 Shape 控件  
 Line 和 Shape 控件封装了许多图形方法，这些方法包含在 <xref:System.Drawing> 命名空间中。  这样您就可以通过一步操作来绘制直线和形状，而不必创建图形对象、钢笔和画笔。  复杂的图形技术（如渐变填充）也只需通过设置一些属性即可完成。  
  
 尽管还可以通过使用图形方法来绘制直线和形状，但使用 Line 和 Shape 控件有下面几个好处：  
  
-   图形方法只能在运行时调用。  Line 和 Shape 控件可以在设计时添加到窗体。  这样您便能够看到它们的外观并对它们进行精确定位；也可以在运行时添加它们。  
  
-   Line 和 Shape 控件在运行时是可选择的，并提供 <xref:Microsoft.VisualBasic.PowerPacks.Shape.Click> 和 <xref:Microsoft.VisualBasic.PowerPacks.Shape.OnDoubleClick%2A> 等事件。  图形方法的输出是不可选择的并且不提供事件。  
  
-   Line 和 Shape 控件提供 <xref:Microsoft.VisualBasic.PowerPacks.Shape.BringToFront%2A> 和 <xref:Microsoft.VisualBasic.PowerPacks.Shape.SendToBack%2A> 方法，使您可以在设计时和运行时控制它们的 Z 顺序。  而对于图形方法，只能通过在运行时更改它们的执行顺序来控制它们的 Z 顺序。  
  
-   Line 和 Shape 控件是无窗口控件；它们没有窗口句柄，因此使用的系统资源较少。  
  
### 对象模型  
 Line 和 Shape 控件均派生自 <xref:Microsoft.VisualBasic.PowerPacks.Shape> 基类，该类定义它们的共享属性、方法和事件。  
  
 下图演示 Line 和 Shape 对象层次结构。  
  
 ![Line 和 Shape 对象层次结构示意图](../../../visual-basic/developing-apps/windows-forms/media/lineshapeobject.png "LineShapeObject")  
Line 和 Shape 对象层次结构  
  
 派生类 <xref:Microsoft.VisualBasic.PowerPacks.LineShape> 包含直线所特有的属性、方法和事件。  派生类 <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape> 是 <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> 和 <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> 的基类；它包含所有形状所共有的属性、方法和事件。  您还可以通过从 <xref:Microsoft.VisualBasic.PowerPacks.SimpleShape> 派生来创建自己的 `Shape` 控件。  
  
 <xref:Microsoft.VisualBasic.PowerPacks.OvalShape> 和 <xref:Microsoft.VisualBasic.PowerPacks.RectangleShape> 类可用于绘制圆形、椭圆形、矩形和圆角矩形。  
  
 将 Line 或 Shape 控件添加到窗体或容器中后，随即会创建一个不可见的 <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> 对象。  <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> 充当每个容器控件中各个形状的画布；每个 <xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> 均有一个对应的 <xref:Microsoft.VisualBasic.PowerPacks.ShapeCollection>，使您可以循环访问 Line 和 Shape 控件。  可以使用剪切和粘贴或通过拖放操作将形状从一个容器移动到另一个容器。  当从容器中移除最后一个形状时，<xref:Microsoft.VisualBasic.PowerPacks.ShapeContainer> 也将随即移除。  
  
> [!NOTE]
>  并不是所有容器控件都支持 Line 和 Shape 控件。  不能在 <xref:System.Windows.Forms.TableLayoutPanel> 或 <xref:System.Windows.Forms.FlowLayoutPanel> 上承载 Line 或 Shape 控件。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks>   
 [如何：使用 LineShape 控件绘制直线](../../../visual-basic/developing-apps/windows-forms/how-to-draw-lines-with-the-lineshape-control-visual-studio.md)   
 [如何：使用 OvalShape 和 RectangleShape 控件绘制形状](../../../visual-basic/developing-apps/windows-forms/how-to-draw-shapes-with-the-ovalshape-and-rectangleshape-controls.md)   
 [如何：使用 Tab 键在形状之间切换](../../../visual-basic/developing-apps/windows-forms/how-to-enable-tabbing-between-shapes-visual-studio.md)