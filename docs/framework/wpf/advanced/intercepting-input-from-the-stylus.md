---
title: "截获触笔输入 | Microsoft Docs"
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
  - "体系结构, System.Windows.Input.StylusPlugIns"
  - "InkCanvas, 添加插件到"
  - "插件, 触笔"
  - "StylusPlugIns 体系结构"
  - "System.Windows.Input.StylusPlugIns 体系结构"
ms.assetid: 791bb2f0-4e5c-4569-ac3c-211996808d44
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 截获触笔输入
<xref:System.Windows.Input.StylusPlugIns> 体系结构提供了一种机制，用于对 <xref:System.Windows.Input.Stylus> 输入和数字墨迹 <xref:System.Windows.Ink.Stroke> 对象的创建实现低级别控制。  <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 类提供了一种机制，用于实现自定义行为并将其应用于来自触笔设备的数据流以获得最佳性能。  
  
 本主题包含以下小节：  
  
-   [体系结构](#Architecture)  
  
-   [实现触笔插件](#ImplementingStylusPlugins)  
  
-   [将插件添加到 InkCanvas](#AddingYourPluginToAnInkCanvas)  
  
-   [结束语](#Conclusion)  
  
<a name="Architecture"></a>   
## 体系结构  
 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 是在 [Microsoft Windows XP Tablet PC Edition Software Development Kit 1.7](http://go.microsoft.com/fwlink/?linkid=11782&clcid=0x409)（Microsoft Windows XP Tablet PC Edition 软件开发工具包 1.7）中的 [StylusInput](http://go.microsoft.com/fwlink/?LinkId=50753&clcid=0x409) API 的基础上发展而来，[Accessing and Manipulating Pen Input](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)（访问和处理笔输入）中对此 API 进行了描述。  
  
 每个 <xref:System.Windows.UIElement> 都有一个属于 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 的 <xref:System.Windows.UIElement.StylusPlugIns%2A> 属性。  可以将 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 添加到元素的 <xref:System.Windows.UIElement.StylusPlugIns%2A> 属性中，以在生成 <xref:System.Windows.Input.StylusPoint> 数据时对其进行处理。  <xref:System.Windows.Input.StylusPoint> 数据由系统数字化器支持的所有属性组成，其中包括 <xref:System.Windows.Input.StylusPoint.X%2A> 和 <xref:System.Windows.Input.StylusPoint.Y%2A> 点数据以及 <xref:System.Windows.Input.StylusPoint.PressureFactor%2A> 数据。  
  
 将 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 添加到 <xref:System.Windows.UIElement.StylusPlugIns%2A> 属性时，会将 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 对象直接插入到来自 <xref:System.Windows.Input.Stylus> 设备的数据流中。  将插件添加到 <xref:System.Windows.UIElement.StylusPlugIns%2A> 集合的顺序指定了这些插件接收 <xref:System.Windows.Input.StylusPoint> 数据的顺序。  例如，如果添加一个对特定区域的输入加以限制的筛选器插件，然后添加一个识别书写笔势的插件，则识别笔势的插件将接收经过筛选的 <xref:System.Windows.Input.StylusPoint> 数据。  
  
<a name="ImplementingStylusPlugins"></a>   
## 实现触笔插件  
 若要实现插件，请从 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 中派生一个类。  该类在数据流从 <xref:System.Windows.Input.Stylus> 进入时应用于数据流。  在这个类中，您可以修改 <xref:System.Windows.Input.StylusPoint> 数据的值。  
  
> [!CAUTION]
>  如果 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 引发或导致异常，应用程序将关闭。  您应对使用 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 的控件进行全面测试，并且仅在确信 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 将不会引发异常时才使用控件。  
  
 下面的示例演示一个对触笔输入加以限制的插件，该示例在 <xref:System.Windows.Input.StylusPoint> 数据从 <xref:System.Windows.Input.Stylus> 设备进入时修改数据中的 <xref:System.Windows.Input.StylusPoint.X%2A> 和 <xref:System.Windows.Input.StylusPoint.Y%2A> 值。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#3)]
[!code-vb[AdvancedInkTopicsSamples#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#3)]  
  
<a name="AddingYourPluginToAnInkCanvas"></a>   
## 将插件添加到 InkCanvas  
 使用自定义插件的最简单途径是实现一个从 InkCanvas 中派生的类，并将其添加到 <xref:System.Windows.UIElement.StylusPlugIns%2A> 属性。  
  
 下面的示例演示一个对墨迹进行筛选的自定义 <xref:System.Windows.Controls.InkCanvas>。  
  
 [!code-csharp[AdvancedInkTopicsSamples#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#4)]  
  
 如果将 `FilterInkCanvas` 添加到应用程序并运行，您将注意到在用户写完笔划之前，墨迹不会被限制在某个区域中。  这是因为 <xref:System.Windows.Controls.InkCanvas> 具有 <xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A> 属性，该属性是 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>，并且已经是 <xref:System.Windows.UIElement.StylusPlugIns%2A> 集合的成员。  您添加到 <xref:System.Windows.UIElement.StylusPlugIns%2A> 集合的自定义 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 在 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 接收数据后接收 <xref:System.Windows.Input.StylusPoint> 数据。  因此，在用户提起笔结束笔画之前，将不会对 <xref:System.Windows.Input.StylusPoint> 数据进行筛选。  若要在用户写出墨迹时对墨迹进行筛选，您必须在 <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 之前插入 `FilterPlugin`。  
  
 下面的 C\# 代码演示一个在写出墨迹时对墨迹进行筛选的自定义 <xref:System.Windows.Controls.InkCanvas>。  
  
 [!code-csharp[AdvancedInkTopicsSamples#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#5)]  
  
<a name="Conclusion"></a>   
## 结束语  
 通过派生您自己的 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> 类并将这些类插入 <xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection> 集合，您可以极大改进数字墨迹的行为。  您可以在 <xref:System.Windows.Input.StylusPoint> 数据生成时对其进行访问，从而能够自定义 <xref:System.Windows.Input.Stylus> 输入。  由于能够对 <xref:System.Windows.Input.StylusPoint> 数据进行这种低级别访问，因此，您可以实现墨迹收集和呈现的同时获得应用程序的最佳性能。  
  
## 请参阅  
 [高级墨迹处理](../../../../docs/framework/wpf/advanced/advanced-ink-handling.md)   
 [Accessing and Manipulating Pen Input](http://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)