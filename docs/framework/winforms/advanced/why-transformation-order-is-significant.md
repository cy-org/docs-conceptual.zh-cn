---
title: "为什么变换顺序非常重要 | Microsoft Docs"
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
  - "转换, 顺序重要性"
ms.assetid: 37d5f9dc-a5cf-4475-aa5d-34d714e808a9
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 为什么变换顺序非常重要
单个 <xref:System.Drawing.Drawing2D.Matrix> 对象可存储一个变换或一系列变换。  后者称为“复合变换”。  复合变换的矩阵是通过单个变换的矩阵相乘得到的。  
  
## 复合变换示例  
 在复合变换中，单个变换的顺序非常重要。  例如，依次旋转、缩放和平移与依次平移、旋转和缩放得到的结果不同。  在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 中，复合变换是从左到右构造的。  如果用 S、R 和 T 分别代表缩放、旋转和平移矩阵，则乘积 SRT（按照这个顺序）就是依次缩放、旋转和平移获得的复合变换的矩阵。  由乘积 SRT 生成的矩阵与由乘积 TRS 生成的矩阵不同。  
  
 造成顺序很重要的一个原因就是，像旋转和缩放这样的变换是针对坐标系的原点进行的。  缩放以原点为中心的对象与缩放已离开原点的对象所得到的结果不同。  同样，旋转以原点为中心的对象与旋转已离开原点的对象所得到的结果也不同。  
  
 下面的示例结合缩放、旋转和平移（按照这个顺序）以形成复合变换。  传递给 <xref:System.Drawing.Graphics.RotateTransform%2A> 方法的 <xref:System.Drawing.Drawing2D.MatrixOrder> 参数指示将在缩放之后进行旋转。  同样地，传递给 <xref:System.Drawing.Graphics.TranslateTransform%2A> 方法的参数 <xref:System.Drawing.Drawing2D.MatrixOrder> 指示将在旋转之后进行平移。  <xref:System.Drawing.Drawing2D.MatrixOrder> 和 <xref:System.Drawing.Drawing2D.MatrixOrder> 是 <xref:System.Drawing.Drawing2D.MatrixOrder> 枚举的成员。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.MiscLegacyTopics#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#21)]  
  
 下面的示例与上面的示例调用相同的方法，但是调用的顺序完全相反。  作为其结果的操作顺序依次是平移、旋转和缩放，与依次缩放、旋转和平移所产生的结果大不相同。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.MiscLegacyTopics#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#22)]  
  
 在复合变换中，颠倒单个变换顺序的一种方法是颠倒方法调用序列的顺序。  控制操作顺序的第二种方法是更改矩阵顺序的参数。  下面的示例与上面的示例相同，不同的是 <xref:System.Drawing.Drawing2D.MatrixOrder> 已更改为 <xref:System.Drawing.Drawing2D.MatrixOrder>。  矩阵是按照 SRT 顺序进行相乘的，其中 S、R 和 T 分别表示缩放、旋转和平移的矩阵。  复合变换的顺序依次是缩放、旋转和平移。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.MiscLegacyTopics#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#23)]  
  
 刚才的示例与本主题中的第一个示例所产生的结果完全相同。  这是因为我们同时颠倒了方法调用的顺序和矩阵相乘的顺序。  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.Matrix>   
 [坐标系和坐标变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [在托管 GDI\+ 中使用变换](../../../../docs/framework/winforms/advanced/using-transformations-in-managed-gdi.md)