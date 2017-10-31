---
title: "如何：使用系统参数键 | Microsoft Docs"
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
  - "资源键, SystemParameters 类"
  - "SystemParameters 类"
ms.assetid: 77571283-d16c-45bb-9f69-cafbbf72b21e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：使用系统参数键
统资源将许多系统度量值作为资源公开，以帮助开发人员创建与系统设置一致的可视元素。  <xref:System.Windows.SystemParameters> 是一个类，它包含系统参数值以及绑定到这些值的资源键，例如，<xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A> 和 <xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A>。  系统参数度量值可以用作静态或动态资源。  如果您希望参数度量值在应用程序运行时自动更新，请使用动态资源；否则，请使用静态资源。  
  
> [!NOTE]
>  动态资源的属性名称后面附加有 *Key* 关键字。  
  
 下面的示例演示如何访问和使用系统参数动态资源来设计按钮的样式或自定义按钮。  此 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 示例通过将 <xref:System.Windows.SystemParameters> 的值赋给按钮的宽度和高度来设置按钮的大小。  
  
## 示例  
 [!code-xml[SystemRes_snip#ParameterDynamicResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#parameterdynamicresources)]  
  
## 请参阅  
 [使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [使用 SystemFonts](../../../../docs/framework/wpf/advanced/how-to-use-systemfonts.md)   
 [使用 SystemParameters](../../../../docs/framework/wpf/advanced/how-to-use-systemparameters.md)