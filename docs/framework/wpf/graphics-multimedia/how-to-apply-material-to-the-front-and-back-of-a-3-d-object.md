---
title: "如何：向三维对象的正面和背面应用 Material | Microsoft Docs"
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
  - "三维对象, 应用 Material 类"
  - "类, 材料"
  - "Material 类, 应用于三维对象的两侧"
ms.assetid: d93c8ad6-4939-4d29-9544-4d16d98093c1
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：向三维对象的正面和背面应用 Material
下面的示例演示如何向三维对象的正面和背面应用 <xref:System.Windows.Media.Media3D.Material>，以及如何对该对象进行动画处理来显示它的正面和背面。  <xref:System.Windows.Media.Media3D.GeometryModel3D> 的 <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> 属性用来向该对象的正面应用红色的 <xref:System.Windows.Media.Brush>，<xref:System.Windows.Media.Media3D.GeometryModel3D> 的 <xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A> 属性用来向该对象的背面应用蓝色的 <xref:System.Windows.Media.Brush>。  下面的代码演示如何向该对象应用 Material：  
  
 [!code-xml[Animation3DGallery_snip#BackMaterialAnimationExampleInline1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexampleinline1)]  
  
## 示例  
 下面的代码显示了完整的示例。  
  
 [!code-xml[Animation3DGallery_snip#BackMaterialAnimationExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/BackMaterialAnimationExample.xaml#backmaterialanimationexamplewholepage)]  
  
## 请参阅  
 [创建三维场景](../../../../docs/framework/wpf/graphics-multimedia/how-to-create-a-3-d-scene.md)   
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)   
 [对三维场景中的材质属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-material-properties-in-a-3-d-scene.md)   
 [向三维对象应用放射材质](../../../../docs/framework/wpf/graphics-multimedia/how-to-apply-emissive-material-to-a-3-d-object.md)