---
title: "如何：使用 SystemParameters | Microsoft Docs"
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
  - "类, SystemParameters"
  - "SystemParameters 类"
ms.assetid: 02e7a5de-94eb-4953-b91c-52e6c872ad5b
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 如何：使用 SystemParameters
下面的示例演示如何访问和使用 <xref:System.Windows.SystemParameters> 的属性以设置按钮样式或自定义按钮。  
  
## 示例  
 系统资源将多种基于系统的设置以资源的形式公开，以帮助您创建与系统设置协调一致的视觉效果。  <xref:System.Windows.SystemParameters> 是一个类，其中既包含系统参数值属性，又包含绑定到这些值的资源键。  例如，<xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> 是 <xref:System.Windows.SystemParameters> 属性值，<xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> 是相应的资源键。  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，可以使用 <xref:System.Windows.SystemParameters> 的成员作为静态属性用法或动态资源引用（静态属性值为资源键）。  如果您希望基于系统的值在应用程序运行时自动更新，请使用动态资源引用；否则请使用静态引用。  资源键的属性名称后面附有 `Key` 后缀。  
  
 下面的示例演示如何访问和使用 <xref:System.Windows.SystemParameters> 的静态值以设置按钮样式或自定义按钮。  此标记示例通过向按钮应用 <xref:System.Windows.SystemParameters> 值来调整按钮的大小。  
  
 [!code-xml[SystemRes_snip#ParameterStaticResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#parameterstaticresources)]  
  
 若要在代码中使用 <xref:System.Windows.SystemParameters> 的值，则不一定要使用静态引用或动态资源引用，  而可以改用 <xref:System.Windows.SystemParameters> 类的值。  尽管非键属性已明确定义为静态属性，但是系统承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的运行时行为将会实时重新计算这些属性，并且会正确考虑对系统值所进行的面向用户的更改。下面的示例演示如何使用 <xref:System.Windows.SystemParameters> 值来设置按钮的宽度和高度。  
  
 [!code-csharp[SystemRes_snip#ParameterResourcesCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#parameterresourcescode)]
 [!code-vb[SystemRes_snip#ParameterResourcesCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#parameterresourcescode)]  
  
## 请参阅  
 <xref:System.Windows.SystemParameters>   
 [使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [使用 SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)   
 [使用系统参数键](../../../../docs/framework/wpf/advanced/how-to-use-system-parameters-keys.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)