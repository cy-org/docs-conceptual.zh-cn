---
title: "如何：向三维模型应用绘图 | Microsoft Docs"
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
  - "三维模型, 应用绘图于"
  - "绘图, 应用于三维模型"
ms.assetid: 68357577-b7fc-446e-8be9-a8cc7df3a350
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：向三维模型应用绘图
此示例演示如何将 <xref:System.Windows.Media.DrawingBrush> 用作应用于[!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)]模型的 <xref:System.Windows.Media.Media3D.Material>。  
  
 下面的代码将 <xref:System.Windows.Media.DrawingGroup> 定义为 <xref:System.Windows.Media.DrawingBrush> 的内容。  <xref:System.Windows.Media.DrawingBrush> 设置为应用于[!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)]平面的 <xref:System.Windows.Media.Media3D.DiffuseMaterial> 的 <xref:System.Windows.Media.Media3D.DiffuseMaterial.Brush%2A> 属性。  
  
 **注意：**您通常会希望将类似如下绘图的复杂对象和值定义为可以重用的资源，并希望简化您的代码。  有关更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
 [!code-xml[3DGallery_snip#ApplyDrawingToMaterialInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialinline1)]  
  
## 示例  
 下面的代码显示了完整的示例。  
  
 [!code-xml[3DGallery_snip#ApplyDrawingToMaterialExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ApplyDrawingToMaterialExample.xaml#applydrawingtomaterialexamplewholepage)]  
  
## 请参阅  
 [XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)   
 [创建三维场景](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [Drawing 对象概述](../../../../docs/framework/wpf/graphics-multimedia/drawing-objects-overview.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)