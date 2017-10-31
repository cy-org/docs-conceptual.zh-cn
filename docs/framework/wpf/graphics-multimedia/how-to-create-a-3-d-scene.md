---
title: "如何：创建三维场景 | Microsoft Docs"
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
  - "三维场景"
  - "创建, 三维场景"
  - "场景, 三维"
ms.assetid: adb4a598-71a2-4dd5-b677-ea3fc11b78b2
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：创建三维场景
本示例演示如何创建类似于已旋转的平板纸的三维对象。  利用 <xref:System.Windows.Controls.Viewport3D> 以及下面的组件创建这一简单的三维场景：  
  
-   使用 <xref:System.Windows.Media.Media3D.PerspectiveCamera> 创建一个照相机。  该照相机指定三维场景的哪个部分是可见的。  
  
-   创建一个网格，以使用 <xref:System.Windows.Media.Media3D.GeometryModel3D> 的 <xref:System.Windows.Media.Media3D.GeometryModel3D.Geometry%2A> 属性指定三维对象（平板纸）的形状。  
  
-   使用 <xref:System.Windows.Media.Media3D.GeometryModel3D> 的 <xref:System.Windows.Media.Media3D.GeometryModel3D.Material%2A> 属性指定要在对象表面显示的材料（本示例中是线性渐变）。  
  
-   使用 <xref:System.Windows.Media.Media3D.DirectionalLight> 创建在对象上发光的光源。  
  
## 示例  
 下面的代码演示如何以 XAML 创建三维场景。  
  
 [!code-xml[3DGallery_snip#Basic3DShapeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_snip/CS/Basic3DShapeExample.xaml#basic3dshapeexamplewholepage)]  
  
## 示例  
 下面的代码演示如何以程序代码创建同一三维场景。  
  
 [!code-csharp[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Basic3DShapeExample.cs#basic3dshapecodeexamplewholepage)]
 [!code-vb[3DGallery_procedural_snip#Basic3DShapeCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/3DGallery_procedural_snip/visualbasic/basic3dshapeexample.vb#basic3dshapecodeexamplewholepage)]  
  
## 请参阅  
 [三维图形概述](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)