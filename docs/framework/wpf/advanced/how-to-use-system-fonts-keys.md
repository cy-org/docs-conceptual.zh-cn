---
title: "如何：使用系统字体键 | Microsoft Docs"
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
  - "资源键, SystemFonts 类"
  - "SystemFonts 类"
ms.assetid: 036ebea7-5677-4f60-8ba4-56c9f9d9b8bd
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用系统字体键
统资源将许多系统度量值作为资源公开，以帮助开发人员创建与系统设置一致的可视元素。  <xref:System.Windows.SystemFonts> 是一个类，它包含系统字体值以及绑定到这些值的系统字体资源。例如，<xref:System.Windows.SystemFonts.CaptionFontFamily%2A> 和 <xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A>。  
  
 系统字体规格可以用作静态或动态资源。  如果您希望字体规格在应用程序运行时自动更新，请使用动态资源；否则，请使用静态资源。  
  
> [!NOTE]
>  动态资源的属性名称后面附加有 *Key* 关键字。  
  
 下面的示例演示如何访问和使用系统字体动态资源来设计或自定义按钮。  此 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例创建一个将 <xref:System.Windows.SystemFonts> 值分配给按钮的按钮样式。  
  
## 示例  
 [!code-xml[SystemRes_snip#FontDynamicResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#fontdynamicresources)]  
  
## 请参阅  
 [使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [使用 SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)   
 [使用 SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)