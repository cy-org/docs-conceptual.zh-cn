---
title: "如何：在渐变中使用系统颜色 | Microsoft Docs"
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
  - "渐变, 系统颜色"
  - "渐变中的系统颜色"
ms.assetid: 11942e7e-6300-4b50-8ed1-f50e8d20e7d2
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在渐变中使用系统颜色
若要在渐变中使用系统颜色，您需要使用 <xref:System.Windows.SystemColors> 类的 *\<系统颜色\>* Color 和 *\<系统颜色\>* ColorKey 静态属性来获取对颜色的引用，其中 *\<系统颜色\>* 是所需系统颜色的名称。  当您希望创建随系统主题变化而自动更新的动态引用时，请使用 *\<系统颜色\>* ColorKey 属性。  否则，请使用 *\<系统颜色\>* Color 属性。  
  
## 示例  
 下面的示例使用动态系统颜色资源创建渐变。  
  
 [!code-xml[brushsamples_snip#GraphicsMMDynamicSystemColorGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/DynamicSystemColorExample.xaml#graphicsmmdynamicsystemcolorgradientexamplewholepage)]  
  
 接下来的示例使用静态系统颜色资源创建渐变。  
  
 [!code-xml[brushsamples_snip#GraphicsMMStaticSystemColorGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/StaticSystemColorExample.xaml#graphicsmmstaticsystemcolorgradientexamplewholepage)]  
  
## 请参阅  
 <xref:System.Windows.SystemColors>   
 [使用系统画笔绘制区域](../../../../docs/framework/wpf/graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)   
 [使用纯色和渐变进行绘制概述](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)