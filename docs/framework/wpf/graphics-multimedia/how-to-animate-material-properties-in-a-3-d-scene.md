---
title: "如何：对三维场景中的材质属性进行动画处理 | Microsoft Docs"
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
  - "三维场景, 对 Material 属性进行动画处理"
  - "动画, 三维场景中的 Material 属性"
  - "Material 属性, 在三维场景中进行动画处理"
ms.assetid: 229fd6eb-7401-4992-b0c9-8b28de230c0f
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：对三维场景中的材质属性进行动画处理
此示例演示如何对 [!INCLUDE[TLA#tla_3d](../../../../includes/tlasharptla-3d-md.md)] 模型中应用的 <xref:System.Windows.Media.Media3D.Material> 的 <xref:System.Windows.Media.Brush.Opacity%2A> 属性进行动画处理。  
  
 下面的代码示例定义作为 <xref:System.Windows.Media.Media3D.Material> 应用到三维对象中的 <xref:System.Windows.Media.LinearGradientBrush>。  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline1)]  
  
 使用下面的代码示例对此 <xref:System.Windows.Media.LinearGradientBrush> 的 <xref:System.Windows.Media.Brush.Opacity%2A> 属性进行动画处理。  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleInline2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexampleinline2)]  
  
## 示例  
 下面的代码显示了完整的示例。  
  
 [!code-xml[Animation3DGallery_snip#AnimateMaterialExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/AnimateMaterialExample.xaml#animatematerialexamplewholepage)]  
  
## 请参阅  
 [创建三维场景](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)