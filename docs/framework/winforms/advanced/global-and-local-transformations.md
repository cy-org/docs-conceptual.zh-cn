---
title: "全局变换和局部变换 | Microsoft Docs"
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
  - "矩阵, 使用转换"
  - "转换, 全局"
  - "转换, 本地"
ms.assetid: b601d66d-d572-4f11-9d2e-92f0dc8893f3
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 全局变换和局部变换
全局变换是应用于由给定的 <xref:System.Drawing.Graphics> 对象绘制的每个项目的变换。  与此相反，局部变换则是应用于要绘制的特定项目的变换。  
  
## 全局变换  
 若要创建全局变换，请构造 <xref:System.Drawing.Graphics> 对象，再操作其 <xref:System.Drawing.Graphics.Transform%2A> 属性。  <xref:System.Drawing.Graphics.Transform%2A> 属性是 <xref:System.Drawing.Drawing2D.Matrix> 对象，因此，它能够保存仿射变换的任何序列。  存储在 <xref:System.Drawing.Graphics.Transform%2A> 属性中的变换被称为世界变换。  <xref:System.Drawing.Graphics> 类提供了几个构建复合世界变换的方法：<xref:System.Drawing.Graphics.MultiplyTransform%2A>、<xref:System.Drawing.Graphics.RotateTransform%2A>、<xref:System.Drawing.Graphics.ScaleTransform%2A> 和 <xref:System.Drawing.Graphics.TranslateTransform%2A>。  下面的示例绘制了两次椭圆：一次在创建世界变换之前，一次在创建世界变换之后。  变换首先在 y 方向上缩放 0.5 倍，再在 x 方向平移 50 个单位，然后旋转 30 度。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.CoordinateSystems#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#21)]  
  
 下图显示了变换中涉及的矩阵。  
  
 ![变换](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art14.gif "AboutGdip05\_art14")  
  
> [!NOTE]
>  在前面的示例中，椭圆围绕坐标系的原点旋转。原点位于工作区的左上角。  与椭圆围绕其自身中心旋转相比，这样会产生不同的结果。  
  
## 局部变换  
 局部变换应用于要绘制的特定项目。  例如，<xref:System.Drawing.Drawing2D.GraphicsPath> 对象具有 <xref:System.Drawing.Drawing2D.GraphicsPath.Transform%2A> 方法，可用来对该路径的数据点进行变换。  下面的示例绘制了一个没有变换的矩形以及一个有旋转变换的路径。  （假定没有世界变换）。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#22](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#22)]
 [!code-vb[System.Drawing.CoordinateSystems#22](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#22)]  
  
 世界变换可与局部变换合并，以得到多种结果。  例如，世界变换可用于修正坐标系统，而局部变换可用于旋转和缩放在新坐标系统上绘制的对象。  
  
 假定您需要原点距工作区左边缘 200 像素、距工作区顶部 150 像素的坐标系统。  此外，假定您需要的度量单位是像素，且 x 轴指向右方，y 轴指向上方。  默认的坐标系统是 y 轴指向下方，因此您需要执行绕水平坐标轴的反射。  下图显示了这样的矩阵反射。  
  
 ![变换](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art15.png "AboutGdip05\_art15")  
  
 下一步，假定您需要执行一个向右 200 个单位、向下 150 个单位的平移。  
  
 下面的示例通过设置 <xref:System.Drawing.Graphics> 对象的世界变换，建立前面刚刚描述过的坐标系统。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#23)]
 [!code-vb[System.Drawing.CoordinateSystems#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#23)]  
  
 下面的代码（置于前面示例的结尾处）创建了由一个单独矩形组成的路径，该矩形的左下角在新坐标系统的原点。  矩形经过两次填充：一次不使用局部变换，一次使用局部变换。  局部变换包括在水平方向上缩放 2 倍，然后再旋转 30 度。  
  
 [!code-csharp[System.Drawing.CoordinateSystems#24](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#24)]
 [!code-vb[System.Drawing.CoordinateSystems#24](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#24)]  
  
 下图显示了新的坐标系统和两个矩形。  
  
 ![变换](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art16.png "AboutGdip05\_art16")  
  
## 请参阅  
 [坐标系和坐标变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [在托管 GDI\+ 中使用变换](../../../../docs/framework/winforms/advanced/using-transformations-in-managed-gdi.md)