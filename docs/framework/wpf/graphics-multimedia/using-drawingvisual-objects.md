---
title: "使用 DrawingVisual 对象 | Microsoft Docs"
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
  - "可视化布局中的 DrawingVisual 对象"
  - "可视化层, DrawingVisual 对象"
ms.assetid: 0b4e711d-e640-40cb-81c3-8f5c59909b7d
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 使用 DrawingVisual 对象
本主题概述如何在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可视层使用 <xref:System.Windows.Media.DrawingVisual> 对象。  
  
 本主题包括以下部分。  
  
<a name="autoTopLevelSectionsOUTLINE0"></a>   
-   [绘制可视对象](#drawing_visual_object)  
  
-   [DrawingVisual 宿主容器](#drawingvisual_host_container)  
  
-   [创建 DrawingVisual 对象](#creating_drawingvisual_objects)  
  
-   [为 FrameworkElement 成员创建重写项](#creating_overrides)  
  
-   [提供命中测试支持](#providing_hit_testing_support)  
  
-   [相关主题](#seeAlsoToggle)  
  
<a name="drawingvisual_object"></a>   
## DrawingVisual 对象  
 <xref:System.Windows.Media.DrawingVisual> 是一个用于呈现形状、图像或文本的轻量绘图类。  此类之所以被视为轻量，是因为它不提供布局或事件处理功能，从而能够改善其性能。  因此，绘图最适于背景和剪贴画。  
  
<a name="drawingvisual_host_container"></a>   
## DrawingVisual 宿主容器  
 为了使用 <xref:System.Windows.Media.DrawingVisual> 对象，需要为这些对象创建一个宿主容器。  该宿主容器对象必须派生自 <xref:System.Windows.FrameworkElement> 类，该类提供 <xref:System.Windows.Media.DrawingVisual> 类所缺乏的布局和事件处理支持。  宿主容器对象不显示任何可视属性，因为它的主要用途是包含子对象。  但是，宿主容器的 <xref:System.Windows.UIElement.Visibility%2A> 属性必须设置为 <xref:System.Windows.Visibility>；否则，它的任何子元素都将不可见。  
  
 当您为可视对象创建宿主容器对象时，需要在 <xref:System.Windows.Media.VisualCollection> 中存储可视对象引用。  使用 <xref:System.Windows.Media.VisualCollection.Add%2A> 方法可以将可视对象添加到宿主容器中。  在下面的示例中，创建一个宿主容器对象，并向它的 <xref:System.Windows.Media.VisualCollection> 添加三个可视对象。  
  
 [!code-csharp[DrawingVisualSample#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[DrawingVisualSample#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#100)]  
  
> [!NOTE]
>  有关从中提取上述代码示例的完整代码示例，请参见 [Hit Test Using DrawingVisuals Sample](http://go.microsoft.com/fwlink/?LinkID=159994)（使用 DrawingVisual 的命中测试示例）。  
  
<a name="creating_drawingvisual_objects"></a>   
## 创建 DrawingVisual 对象  
 当创建一个 <xref:System.Windows.Media.DrawingVisual> 对象时，该对象没有绘图内容。  您可以通过检索对象的 <xref:System.Windows.Media.DrawingContext> 并在其中进行绘制来添加文本、图形或图像内容。  通过调用 <xref:System.Windows.Media.DrawingVisual> 对象的 <xref:System.Windows.Media.DrawingVisual.RenderOpen%2A> 方法来返回 <xref:System.Windows.Media.DrawingContext>。  
  
 要在 <xref:System.Windows.Media.DrawingContext> 中绘制一个矩形，应使用 <xref:System.Windows.Media.DrawingContext> 对象的 <xref:System.Windows.Media.DrawingContext.DrawRectangle%2A> 方法。  绘制其他类型的内容存在类似方法。  将内容绘制到 <xref:System.Windows.Media.DrawingContext> 后，调用 <xref:System.Windows.Media.DrawingContext.Close%2A> 方法来关闭 <xref:System.Windows.Media.DrawingContext> 并保存内容。  
  
 在下面的示例中，将创建一个 <xref:System.Windows.Media.DrawingVisual> 对象，并将一个矩形绘制到它的 <xref:System.Windows.Media.DrawingContext> 中。  
  
 [!code-csharp[DrawingVisualSample#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#101)]
 [!code-vb[DrawingVisualSample#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#101)]  
  
<a name="creating_overrides"></a>   
## 为 FrameworkElement 成员创建重写项  
 宿主容器对象负责管理它的可视对象集合。  这需要宿主容器为派生的 <xref:System.Windows.FrameworkElement> 类实现成员重写。  
  
 下面介绍了必须重写的两个成员：  
  
-   <xref:System.Windows.FrameworkElement.GetVisualChild%2A>：从子元素集合返回指定索引处的子级。  
  
-   <xref:System.Windows.FrameworkElement.VisualChildrenCount%2A>：获取此元素内部的可视子元素的数目。  
  
 在下面的示例中，实现了这两个 <xref:System.Windows.FrameworkElement> 成员的重写。  
  
 [!code-csharp[DrawingVisualSample#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#102)]
 [!code-vb[DrawingVisualSample#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#102)]  
  
<a name="providing_hit_testing_support"></a>   
## 提供命中测试支持  
 宿主容器对象即使不显示任何可视属性（但是，它的 <xref:System.Windows.UIElement.Visibility%2A> 属性必须设置为 <xref:System.Windows.Visibility>），也可以提供事件处理。  这样，您就可以为宿主容器创建事件处理例程，此例程可以捕获鼠标事件，如松开鼠标左键。  然后事件处理例程可以通过调用 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 方法来执行命中测试。  此方法的 <xref:System.Windows.Media.HitTestResultCallback> 参数引用一个用户定义的过程，您可以使用此过程来确定命中测试的最终操作。  
  
 在下面的示例中，为宿主容器对象以及它的子级实现命中测试支持。  
  
 [!code-csharp[DrawingVisualSample#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DrawingVisualSample/CSharp/Window1.xaml.cs#103)]
 [!code-vb[DrawingVisualSample#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DrawingVisualSample/visualbasic/window1.xaml.vb#103)]  
  
## 请参阅  
 <xref:System.Windows.Media.DrawingVisual>   
 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [可视化层中的命中测试](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)