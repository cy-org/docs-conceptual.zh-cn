---
title: "如何：变换三维模型的比例 | Microsoft Docs"
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
  - "三维对象, 缩放"
  - "缩放, 三维对象"
ms.assetid: f3fdfe33-f7dc-44b0-84a5-e43b89947f35
caps.latest.revision: 3
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# 如何：变换三维模型的比例
此示例演示如何缩放三维对象。  若要缩放三维对象，请使用 <xref:System.Windows.Media.Media3D.ScaleTransform3D>。  <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A>、<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A> 和 <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A> 属性按照指定的比例调整元素的大小。  例如，<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleX%2A> 值为 1.5 时，会将对象拉伸到其原始宽度的 150%。  <xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleY%2A> 值为 0.5 时，会将对象的高度缩小 50%。  下面的代码演示如何将 <xref:System.Windows.Media.Media3D.ScaleTransform3D> 用作 <xref:System.Windows.Media.Media3D.GeometryModel3D> 的变换。  
  
 [!code-xml[3DGallery_snip#ScaleTransform3DExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexampleinline1)]  
  
## 示例  
 下面的代码显示了完整的示例。  
  
 [!code-xml[3DGallery_snip#ScaleTransform3DExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/ScaleTransform3DExample.xaml#scaletransform3dexamplewholepage)]  
  
## 请参阅  
 [对三维平移进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-3-d-translations.md)   
 [创建三维场景](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)