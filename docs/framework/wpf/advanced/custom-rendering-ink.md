---
title: "自定义呈现墨迹 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "类, DynamicRenderer"
  - "类, InkCanvas"
  - "类, 边框"
  - "自定义呈现墨迹"
  - "DynamicRenderer 类"
  - "墨迹, 自定义呈现"
  - "InkCanvas 类"
  - "Stroke 类"
ms.assetid: 65c978a7-0ee0-454f-ac7f-b1bd2efecac5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 自定义呈现墨迹
通过笔画的 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 属性可以指定笔画的外观，例如笔画的大小、颜色和形状，但有时除了 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 允许的那些外观之外，您可能还希望自定义外观。  您可能希望通过在喷枪、油彩和许多其他效果中呈现来自定义墨迹的外观。  [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 允许您通过实现自定义 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 和 <xref:System.Windows.Ink.Stroke> 对象来自定义呈现墨迹。  
  
 本主题包含以下小节：  
  
-   [体系结构](#Architecture)  
  
-   [实现动态呈现程序](#ImplementingADynamicRenderer)  
  
-   [Implementing a Custom Stroke](#ImplementingACustomStroke)  
  
-   [实现自定义 InkCanvas](#ImplementingACustomInkCanvas)  
  
-   [结束语](#Conclusion)  
  
<a name="Architecture"></a>   
## 体系结构  
 墨迹呈现发生两次：当用户在墨迹图面上书写墨迹时，以及将笔画添加到支持墨迹的图面上之后。  当用户将触笔移动到数字化仪上时，<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 将呈现墨迹，一旦将<xref:System.Windows.Ink.Stroke>添加到元素上，它会呈现其自身。  
  
 动态呈现墨迹时需要实现三个类。  
  
1.  **DynamicRenderer**：实现从 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 派生的类。  此类是一个专用的 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>，它在绘制笔画时呈现笔画。  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 在单独的线程上进行呈现，因此即使应用程序用户界面 \(UI\) 线程被阻止，墨迹图面也会显示为正在收集墨迹。  有关线程模型的更多信息，请参见[墨迹线程处理模型](../../../../docs/framework/wpf/advanced/the-ink-threading-model.md)。  若要自定义动态呈现笔画，请重写 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> 方法。  
  
2.  **Stroke**：实现从 <xref:System.Windows.Ink.Stroke> 派生的类。  此类负责在 <xref:System.Windows.Input.StylusPoint> 数据转换为 <xref:System.Windows.Ink.Stroke> 对象后静态呈现该数据。  重写 <xref:System.Windows.Ink.Stroke.DrawCore%2A> 方法，以确保笔画的静态呈现与动态呈现保持一致。  
  
3.  **InkCanvas**：实现从 <xref:System.Windows.Controls.InkCanvas> 派生的类。  请将自定义的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 分配给 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> 属性。  重写 <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> 方法，并将自定义笔画添加到 <xref:System.Windows.Controls.InkCanvas.Strokes%2A> 属性中。  这样可以确保墨迹的外观保持一致。  
  
<a name="ImplementingADynamicRenderer"></a>   
## 实现动态呈现程序  
 尽管 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 类是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的标准组成部分，但若要进行更专业的呈现，您必须创建从 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 派生的自定义动态呈现程序并重写 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.OnDraw%2A> 方法。  
  
 下面的示例演示使用线性渐变画笔效果绘制墨迹的自定义 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#1)]
[!code-vb[AdvancedInkTopicsSamples#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#1)]  
  
<a name="ImplementingCustomStrokes"></a>   
## 实现自定义笔画  
 实现从 <xref:System.Windows.Ink.Stroke> 派生的类。  此类负责在 <xref:System.Windows.Input.StylusPoint> 数据转换为 <xref:System.Windows.Ink.Stroke> 对象后呈现该数据。  重写 <xref:System.Windows.Ink.Stroke.DrawCore%2A> 类以完成实际的绘制。  
  
 通过使用 <xref:System.Windows.Ink.Stroke.AddPropertyData%2A> 方法，您的 Stroke 类还可以存储自定义数据。  持久性保存数据时，此数据与笔画数据存储在一起。  
  
 <xref:System.Windows.Ink.Stroke> 类还可以执行命中测试。  通过重写 <xref:System.Windows.Ink.Stroke.HitTest%2A> 方法，您还可以在当前类中实现自己的命中测试算法。  
  
 下面的 C\# 代码演示将 <xref:System.Windows.Input.StylusPoint> 数据呈现为三维笔画的自定义 <xref:System.Windows.Ink.Stroke> 类。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#2)]
[!code-vb[AdvancedInkTopicsSamples#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#2)]  
  
<a name="ImplementingACustomInkCanvas"></a>   
## 实现自定义 InkCanvas  
 使用自定义 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 和笔画的最简单方式是实现一个从 <xref:System.Windows.Controls.InkCanvas> 派生的类，并使用这些类。  <xref:System.Windows.Controls.InkCanvas> 具有一个 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> 属性，它指定当用户绘制笔画时如何呈现笔画。  
  
 若要在 <xref:System.Windows.Controls.InkCanvas> 上自定义呈现笔画，请执行以下操作：  
  
-   创建一个从 <xref:System.Windows.Controls.InkCanvas> 派生的类。  
  
-   将自定义的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 分配给 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A?displayProperty=fullName> 属性。  
  
-   重写 <xref:System.Windows.Controls.InkCanvas.OnStrokeCollected%2A> 方法。  在此方法中，移除已添加到 InkCanvas 中的原始笔画。  然后创建一个自定义笔画，将其添加到 <xref:System.Windows.Controls.InkCanvas.Strokes%2A> 属性中，然后使用包含该自定义笔画的新 <xref:System.Windows.Controls.InkCanvasStrokeCollectedEventArgs> 调用基类。  
  
 下面的 C\# 代码演示使用自定义 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 并收集自定义笔画的自定义 <xref:System.Windows.Controls.InkCanvas> 类。  
  
 [!code-csharp[AdvancedInkTopicsSamples#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#9)]  
  
 一个 <xref:System.Windows.Controls.InkCanvas> 可以具有一个或多个 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>。  您可以通过将多个 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 对象添加到 <xref:System.Windows.UIElement.StylusPlugIns%2A> 属性中，从而将它们添加到 <xref:System.Windows.Controls.InkCanvas> 中。  
  
<a name="Conclusion"></a>   
## 结束语  
 您可以通过派生自己的 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>、<xref:System.Windows.Ink.Stroke> 和 <xref:System.Windows.Controls.InkCanvas> 类来自定义墨迹的外观。  将这些类结合使用可以确保在用户绘制笔画以及收集笔画后，笔画的外观保持一致。  
  
## 请参阅  
 [高级墨迹处理](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)