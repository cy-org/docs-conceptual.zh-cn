---
title: "如何：测试 Point4D 结构是否相等和不相等 | Microsoft Docs"
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
  - "相等, 测试 Point4D 结构"
  - "不相等, 测试 Point4D 结构"
  - "Point4D 结构, 测试是否相等"
  - "Point4D 结构, 测试是否不相等"
  - "测试, Point4D 结构是否相等"
  - "测试, Point4D 结构是否不相等"
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：测试 Point4D 结构是否相等和不相等
本示例演示如何测试 <xref:System.Windows.Media.Media3D.Point4D> 结构是相等还是不相等。  
  
 下面的代码阐释如何使用 <xref:System.Windows.Media.Media3D.Point4D> 相等方法来测试 <xref:System.Windows.Media.Media3D.Point4D> 结构是相等还是不相等。  先使用重载的等于 \(`==`\) 运算符来测试 <xref:System.Windows.Media.Media3D.Point4D> 结构是否相等，然后使用重载的不等 \(`!=`\) 运算符测试这些结构是否不相等，最后使用静态 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A> 方法检查 <xref:System.Windows.Media.Media3D.Point3D> 结构和 <xref:System.Windows.Media.Media3D.Point4D> 结构是否相等。  
  
## 示例  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](../../../../samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## 请参阅  
 <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>   
 <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>   
 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>