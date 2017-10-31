---
title: "使用世界变换 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "图形, 全局转换"
  - "全局转换, 示例"
ms.assetid: 1e717711-1361-448e-aa49-0f3ec43110c9
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 使用世界变换
世界变换是 <xref:System.Drawing.Graphics> 类的一个属性。  指定世界变换的数字存储在表示一个 3×3 矩阵的 <xref:System.Drawing.Drawing2D.Matrix> 对象中。  <xref:System.Drawing.Drawing2D.Matrix> 和 <xref:System.Drawing.Graphics> 类有几种方法用于设置世界变换矩阵中的数字。  
  
## 不同类型的变换  
 在下面的示例中，该代码先创建 50×50 的矩形，然后将其定位到原点 \(0, 0\)。  原点位于工作区的左上角。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.MiscLegacyTopics#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#11)]  
  
 下面的代码应用缩放变换，将矩形的 x 方向放大到 1.75 倍；将 y 方向缩小到 0.5 倍：  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#12)]
 [!code-vb[System.Drawing.MiscLegacyTopics#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#12)]  
  
 其结果是一个比原矩形在 x 方向上变长、在 y 方向上变短的矩形。  
  
 若要旋转而非缩放矩形，请使用下面的代码：  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#13)]
 [!code-vb[System.Drawing.MiscLegacyTopics#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#13)]  
  
 若要平移矩形，请使用下面的代码：  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.MiscLegacyTopics#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#14)]  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.Matrix>   
 [坐标系和坐标变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [在托管 GDI\+ 中使用变换](../../../../docs/framework/winforms/advanced/using-transformations-in-managed-gdi.md)