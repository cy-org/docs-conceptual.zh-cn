---
title: "如何：使用颜色矩阵对单色进行变换 | Microsoft Docs"
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
  - "颜色矩阵, using"
  - "图像颜色, 转换"
ms.assetid: 44df4556-a433-49c0-ac0f-9a12063a5860
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：使用颜色矩阵对单色进行变换
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供用于存储和操作图像的 <xref:System.Drawing.Image> 和 <xref:System.Drawing.Bitmap> 类。  <xref:System.Drawing.Image> 和 <xref:System.Drawing.Bitmap> 对象用一个 32 位数字存储每个像素的颜色：红、绿、蓝和 Alpha 各 8 位。  这四个分量的值都是 0 到 255，其中 0 表示没有亮度，255 表示最大亮度。  alpha 分量指定颜色的透明度：0 表示完全透明，255 表示完全不透明。  
  
 颜色矢量采用 4 元组形式（红色、绿色、蓝色、alpha）。  例如，颜色矢量 \(0, 255, 0, 255\) 表示一种没有红色和蓝色但绿色达到最大亮度的不透明颜色。  
  
 表示颜色的另一种惯例是用数字 1 表示亮度达到最大。  通过使用这种约定，上一段中描述的颜色将可以由矢量 \(0, 1, 0, 1\) 表示。  在执行颜色变换时，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 遵循使用 1 为最大亮度的惯例。  
  
 可通过用 4×4 矩阵乘以这些颜色矢量将线性变换（旋转和缩放等）应用到颜色矢量中。  但是，您不能使用 4×4 矩阵进行平移（非线性）。  如果在每个颜色矢量中再添加一个虚拟的第 5 坐标（例如，数字 1），则可使用 5×5 矩阵应用任何组合形式的线性变换和平移。  由线性变换组成的后跟平移的变换称为仿射变换。  
  
 例如，假设您希望从颜色 \(0.2, 0.0, 0.4, 1.0\) 开始并应用下面的变换：  
  
1.  将红色分量乘以 2。  
  
2.  将 0.2 添加到红色、绿色和蓝色分量中。  
  
 下面的矩阵乘法将按照列出的顺序进行这对变换。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring01.png "recoloring01")  
  
 颜色矩阵的元素按照先行后列（从 0 开始）的顺序进行索引。  例如，矩阵 M 的第五行第三列由 M\[4\]\[2\] 表示。  
  
 5×5 单位矩阵（在下面的插图中显示）在对角线上为 1，在其他任何地方为 0。  如果用单位矩阵乘以颜色矢量，则颜色矢量不会发生改变。  形成颜色变换矩阵的一种简便方法是从单位矩阵开始，然后进行较小的改动以产生所需的变换。  
  
 ![重新着色](../../../../docs/framework/winforms/advanced/media/recoloring02.gif "recoloring02")  
  
 有关矩阵和变换的更详细的讨论，请参见[坐标系统和变形](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)。  
  
## 示例  
 下面的示例采用一个使用一种颜色 \(0.2, 0.0, 0.4, 1.0\) 的图像，并应用上一段中描述的变换。  
  
 下面的插图在左侧显示原来的图像，在右侧显示变换后的图像。  
  
 ![颜色](../../../../docs/framework/winforms/advanced/media/colortrans1.png "colortrans1")  
  
 下面示例中的代码使用以下步骤进行重新着色：  
  
1.  初始化 <xref:System.Drawing.Imaging.ColorMatrix> 对象。  
  
2.  创建一个 <xref:System.Drawing.Imaging.ImageAttributes> 对象，并将 <xref:System.Drawing.Imaging.ColorMatrix> 对象传递给 <xref:System.Drawing.Imaging.ImageAttributes> 对象的 <xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A> 方法。  
  
3.  将 <xref:System.Drawing.Imaging.ImageAttributes> 对象传递给 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.DrawImage%2A> 方法。  
  
 [!code-csharp[System.Drawing.RecoloringImages#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.RecoloringImages/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.RecoloringImages#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.RecoloringImages/VB/Class1.vb#21)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 [对图像重新着色](../../../../docs/framework/winforms/advanced/recoloring-images.md)   
 [坐标系和坐标变换](../../../../docs/framework/winforms/advanced/coordinate-systems-and-transformations.md)