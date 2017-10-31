---
title: "如何：使用系统画笔绘制区域 | Microsoft Docs"
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
  - "画笔, 使用系统画笔进行绘制"
  - "绘制, 使用系统画笔"
  - "系统画笔, 绘制"
ms.assetid: 5141a763-9235-42cb-a6bb-afc75513eac7
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用系统画笔绘制区域
<xref:System.Windows.SystemColors> 类提供对系统画笔和颜色（如 <xref:System.Windows.SystemColors.ControlBrush%2A>、<xref:System.Windows.SystemColors.ControlBrushKey%2A> 和 <xref:System.Windows.SystemColors.DesktopBrush%2A>）的访问权限。  系统画笔是使用指定的系统颜色来绘制区域的 <xref:System.Windows.Media.SolidColorBrush> 对象。  系统画笔总是生成纯色填充，它不能用于创建渐变。  
  
 您可以将系统画笔用作静态资源，也可以用作动态资源。  如果您希望在应用程序运行期间当用户更改系统画笔时画笔自动进行更新，请使用动态资源；否则请使用静态资源。  SystemColors 类包含有大量静态属性，这些属性遵循严格的命名约定：  
  
-   *\<系统颜色\>*Brush  
  
     获取对指定的系统颜色的 <xref:System.Windows.Media.SolidColorBrush> 的静态引用。  
  
-   *\<系统颜色\>*BrushKey  
  
     获取对指定的系统颜色的 <xref:System.Windows.Media.SolidColorBrush> 的动态引用。  
  
-   *\<系统颜色\>*Color  
  
     获取对指定的系统颜色的 <xref:System.Windows.Media.Color> 结构的静态引用。  
  
-   *\<系统颜色\>*ColorKey  
  
     获取对指定的系统颜色的 <xref:System.Windows.Media.Color> 结构的动态引用。  
  
 系统颜色是一种可用于配置画笔的 <xref:System.Windows.Media.Color> 结构。  例如，您可以通过使用系统颜色设置 <xref:System.Windows.Media.LinearGradientBrush> 对象的渐变停止点的 <xref:System.Windows.Media.GradientStop.Color%2A> 属性来创建渐变。  有关示例，请参见[在渐变中使用系统颜色](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md)。  
  
## 示例  
 下面的示例使用动态系统画笔引用来设置按钮的背景。  
  
 [!code-xml[brushsamples_snip#GraphicsMMDynamicSystemColorDesktopBrushKeyExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemBrushExample.xaml#graphicsmmdynamicsystemcolordesktopbrushkeyexamplewholepage)]  
  
 接下来的示例使用静态系统画笔引用来设置按钮的背景。  
  
 [!code-xml[brushsamples_snip#GraphicsMMStaticSystemColorDesktopBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemBrushExample.xaml#graphicsmmstaticsystemcolordesktopbrushexamplewholepage)]  
  
 有关演示如何在渐变中使用系统颜色的示例，请参见[在渐变中使用系统颜色](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md)。  
  
## 请参阅  
 [在渐变中使用系统颜色](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-system-colors-in-a-gradient.md)   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)