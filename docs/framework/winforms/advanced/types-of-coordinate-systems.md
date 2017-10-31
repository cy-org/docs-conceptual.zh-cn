---
title: "坐标系类型 | Microsoft Docs"
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
  - "坐标系统"
  - "设备坐标系统"
  - "页坐标系统"
  - "页转换"
  - "转换, page"
  - "转换, 全局"
  - "度量单位"
  - "全局坐标系统"
  - "全局转换"
ms.assetid: c61ff50a-eb1d-4e6c-83cd-f7e9764cfa9f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 坐标系类型
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 使用三个坐标空间：世界、页面和设备。  世界坐标是用于建立特殊图形世界模型的坐标系，也是在 .NET Framework 中传递给方法的坐标系。  页面坐标系是指绘图图面（如窗体或控件）使用的坐标系。  设备坐标系是在其上进行绘制的物理设备（如屏幕或纸张）所使用的坐标系。  当调用 `myGraphics.DrawLine(myPen, 0, 0, 160, 80)` 时，传递给 <xref:System.Drawing.Graphics.DrawLine%2A> 方法的点（`(0, 0)` 和 `(160, 80)`）位于世界坐标空间内。  在 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可以在屏幕上绘制线条之前，坐标先要经过一系列变换。  一种称为“世界变换”的变换可将世界坐标转换为页面坐标，而另一种称为“页面变换”的变换可将页面坐标转换为设备坐标。  
  
## 变换和坐标系  
 假定您想使用原点位于工作区的主体而非左上角的坐标系统。  例如，您需要让原点位于距工作区左边缘 100 像素、距顶部 50 像素的位置。  下图显示了这样的坐标系统。  
  
 ![坐标系](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art01.png "AboutGdip05\_art01")  
  
 当调用 `myGraphics.DrawLine(myPen, 0, 0, 160, 80)` 时，可得到下面的插图中所显示的线条。  
  
 ![坐标系](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art02.png "AboutGdip05\_art02")  
  
 下表显示了三种坐标空间中线条终点的坐标：  
  
|||  
|-|-|  
|World|\(0, 0\) 到 \(160, 80\)|  
|页|\(100, 50\) 到 \(260, 130\)|  
|设备|\(100, 50\) 到 \(260, 130\)|  
  
 请注意，页面坐标空间的原点在工作区的左上角，情况将总是如此。  另外请注意，由于度量单位是像素，所以设备坐标与页面坐标是相同的。  如果将度量单位设置为像素以外的其他单位（例如英寸），设备坐标将不同于页面坐标。  
  
 用于将世界坐标映射到页面坐标的世界变换保存在 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.Transform%2A> 属性中。  在前面的示例中，世界变换是在 x 方向平移 100 个单位、在 y 方向平移 50 个单位。  下面的示例设置了 <xref:System.Drawing.Graphics> 对象的世界变换，然后使用该 <xref:System.Drawing.Graphics> 对象绘制前图中显示的线条：  
  
 [!code-csharp[System.Drawing.CoordinateSystems#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.CoordinateSystems#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#31)]  
  
 页面变换将页面坐标映射到设备坐标。  <xref:System.Drawing.Graphics> 类提供了用于操作页面变换的 <xref:System.Drawing.Graphics.PageUnit%2A> 和 <xref:System.Drawing.Graphics.PageScale%2A> 属性。  <xref:System.Drawing.Graphics> 类还提供了两个只读属性：<xref:System.Drawing.Graphics.DpiX%2A> 和 <xref:System.Drawing.Graphics.DpiY%2A>，用于检查显示设备每英寸的水平点数和垂直点数。  
  
 可使用 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.PageUnit%2A> 属性指定除像素以外的其他度量单位。  
  
> [!NOTE]
>  不能将 <xref:System.Drawing.Graphics.PageUnit%2A> 属性设置为 <xref:System.Drawing.GraphicsUnit>，因为这不是物理单元，将导致异常。  
  
 下面的示例从 \(0, 0\) 至 \(2, 1\) 绘制线条，其中点 \(2, 1\) 位于点 \(0, 0\) 的右边 2 英寸和下边 1 英寸处：  
  
 [!code-csharp[System.Drawing.CoordinateSystems#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.CoordinateSystems#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#32)]  
  
> [!NOTE]
>  如果在构造钢笔时没有指定钢笔的宽度，前面的示例将绘制一条一英寸宽的线条。  可以在 <xref:System.Drawing.Pen> 构造函数的第二个参数中指定钢笔的宽度：  
  
 [!code-csharp[System.Drawing.CoordinateSystems#33](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#33)]
 [!code-vb[System.Drawing.CoordinateSystems#33](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#33)]  
  
 如果我们假定显示设备在水平方向和垂直方向每英寸都有 96 个点，则上例中直线的终结点在三个坐标空间中分别具有以下坐标：  
  
|||  
|-|-|  
|World|\(0, 0\) 到 \(2, 1\)|  
|页|\(0, 0\) 到 \(2, 1\)|  
|设备|\(0, 0\) 到 \(192, 96\)|  
  
 请注意，由于世界坐标空间的原点在工作区的左上角，因此页面坐标与世界坐标相同。  
  
 您可以合并世界变换和页面变换，以实现多种效果。  例如，假定您想使用英寸作为度量单位，并且想让坐标系统的原点距工作区左边缘 2 英寸、距工作区顶部 1\/2 英寸。  下面的示例设置 <xref:System.Drawing.Graphics> 对象的世界变换和页面变换，然后绘制一条从 \(0, 0\) 到 \(2, 1\) 的直线：  
  
 [!code-csharp[System.Drawing.CoordinateSystems#34](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.CoordinateSystems#34](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.CoordinateSystems/VB/Class1.vb#34)]  
  
 下图显示了线条和坐标系统。  
  
 ![坐标系](../../../../docs/framework/winforms/advanced/media/aboutgdip05-art03.png "AboutGdip05\_art03")  
  
 如果我们假定显示设备在水平方向和垂直方向每英寸都有 96 个点，则上例中直线的终结点在三个坐标空间中分别具有以下坐标：  
  
|||  
|-|-|  
|World|\(0, 0\) 到 \(2, 1\)|  
|页|\(2, 0.5\) 到 \(4, 1.5\)|  
|设备|\(192, 48\) 到 \(384, 144\)|  
  
## 请参阅  
 [坐标系和坐标变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)   
 [变换的矩阵表示形式](../../../../docs/framework/winforms/advanced/matrix-representation-of-transformations.md)