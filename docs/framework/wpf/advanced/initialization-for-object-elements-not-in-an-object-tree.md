---
title: "不在对象树中的对象元素的初始化 | Microsoft Docs"
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
  - "元素, 初始化"
  - "初始化元素"
  - "Logical Tree — 逻辑树"
  - "Visual Tree — 可视化树"
ms.assetid: 7b8dfc9b-46ac-4ce8-b7bb-035734d688b7
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 不在对象树中的对象元素的初始化
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 初始化的某些方面被推迟到通常依赖连接到[逻辑树](GTMT)或[可视化树](GTMT)的元素的进程。  本主题介绍初始化未连接到两种树之一的元素可能需要的步骤。  
  
   
  
## 元素和逻辑树  
 当在代码中创建 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的实例时，应注意 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的对象初始化的几个方面特意不在调用类构造函数时所执行的代码的某一部分实现。  这种情况对于控件类尤为突出，该控件的大部分可视化表示都不是由构造函数定义的，  而是由控件的模板定义的。  模板可能来自于各种源，但是最常见的情况是来自于主题样式。  模板实际上是后期绑定的；只有在相应的控件已准备好应用布局时，才会将所需的模板附加到该控件上。  并且控件只有在已附加到连接到根级别的呈现图面的逻辑树时，才能准备好应用布局。  将由根级元素启动在逻辑树中定义的所有子元素的呈现。  
  
 可视化树也参与此过程。  通过模板成为可视化树一部分的元素也是在连接后才完全实例化的。  
  
 此行为的结果是，依赖元素的已完成可视化特征的某些操作需要额外的步骤。  例如，如果您尝试获取一个已构造但还未附加到树的类的可视化特征，就需要额外的步骤。  例如，如果您需要对 <xref:System.Windows.Media.Imaging.RenderTargetBitmap> 调用 <xref:System.Windows.Media.Imaging.RenderTargetBitmap.Render%2A>，并且要传递的 Visual 是未连接到树的元素，则直到完成了额外的初始化步骤，该元素在可视化效果方面才完成。  
  
### 使用 BeginInit 和 EndInit 初始化元素  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中有多个类实现 <xref:System.ComponentModel.ISupportInitialize> 接口。  使用该接口的 <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A> 和 <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> 方法可以表示代码中包含初始化步骤（例如，设置影响呈现的属性值）的一个区域。  在按顺序调用 <xref:System.ComponentModel.ISupportInitialize.EndInit%2A> 之后，布局系统就可以处理元素并开始查找隐式样式。  
  
 如果针对其设置属性的元素是 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 派生类，则您可以调用 <xref:System.Windows.FrameworkElement.BeginInit%2A> 和 <xref:System.Windows.FrameworkElement.EndInit%2A> 的类版本，而不是强制转换为 <xref:System.ComponentModel.ISupportInitialize>。  
  
### 代码示例  
 下面的示例是一个控制台应用程序的代码示例，该应用程序使用呈现 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 和一个松散 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件的 <xref:System.Windows.Markup.XamlReader.Load%28System.IO.Stream%29?displayProperty=fullName> 来演示 <xref:System.Windows.FrameworkElement.BeginInit%2A> 和 <xref:System.Windows.FrameworkElement.EndInit%2A> 相对于其他调整影响呈现的属性的 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 调用的正确位置。  
  
 此示例仅演示主要函数。  函数 `Rasterize` 和 `Save`（未显示）是负责图像处理和 IO 的实用程序函数。  
  
 [!code-csharp[InitializeElements#Main](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InitializeElements/CSharp/initializeelements.cs#main)]
 [!code-vb[InitializeElements#Main](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InitializeElements/VisualBasic/initializeelements.vb#main)]  
  
## 请参阅  
 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)   
 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)