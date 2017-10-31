---
title: "如何：使用 SystemFonts | Microsoft Docs"
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
  - "类, SystemFonts"
  - "字体, 系统字体"
  - "系统字体"
  - "SystemFonts 类"
ms.assetid: 3f46a4ec-2225-408a-8123-8838a8f7057a
caps.latest.revision: 27
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 如何：使用 SystemFonts
此示例演示如何使用 <xref:System.Windows.SystemFonts> 类的静态资源来设置按钮样式或自定义按钮。  
  
## 示例  
 系统资源将系统确定的许多值以资源和属性的形式公开，以帮助您创建与系统设置协调一致的视觉效果。  <xref:System.Windows.SystemFonts> 是一个类，其中既包含作为静态属性的系统字体值，又包含引用可用于在运行时动态访问这些值的资源键的属性。  例如，<xref:System.Windows.SystemFonts.CaptionFontFamily%2A> 是 <xref:System.Windows.SystemFonts> 值，<xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A> 是相应的资源键。  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，可以使用 <xref:System.Windows.SystemFonts> 的成员作为静态属性或动态资源引用（静态属性值为资源键）。  如果您希望字体规格在应用程序运行时自动更新，请使用动态资源引用；否则，请使用静态值引用。  
  
> [!NOTE]
>  资源键的属性名称后面附有“Key”后缀。  
  
 下面的示例演示如何访问和使用作为静态值的 <xref:System.Windows.SystemFonts> 的属性以设置按钮样式或自定义按钮。  此标记示例会将 <xref:System.Windows.SystemFonts> 值分配给按钮。  
  
 [!code-xml[SystemRes_snip#FontStaticResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#fontstaticresources)]  
  
 若要在代码中使用 <xref:System.Windows.SystemFonts> 的值，不一定要使用静态值或动态资源引用，  而可以改用 <xref:System.Windows.SystemFonts> 类的非键属性。  尽管非键属性已明确定义为静态属性，但是系统承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的运行时行为将会实时重新评估这些属性，并且会正确考虑对系统值所进行的面向用户的更改。  下面的示例演示如何指定按钮的字体设置。  
  
 [!code-csharp[SystemRes_snip#FontResourcesCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#fontresourcescode)]
 [!code-vb[SystemRes_snip#FontResourcesCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#fontresourcescode)]  
  
## 请参阅  
 <xref:System.Windows.SystemFonts>   
 [使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [使用 SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)   
 [使用系统字体键](../../../../docs/framework/wpf/advanced/how-to-use-system-fonts-keys.md)   
 [帮助主题](../../../../docs/framework/wpf/advanced/resources-how-to-topics.md)   
 [x:Static 标记扩展](../../../../docs/framework/xaml-services/x-static-markup-extension.md)   
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [DynamicResource 标记扩展](../../../../docs/framework/wpf/advanced/dynamicresource-markup-extension.md)