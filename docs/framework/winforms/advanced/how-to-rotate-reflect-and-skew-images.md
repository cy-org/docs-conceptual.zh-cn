---
title: "如何：旋转、反射和扭曲图像 | Microsoft Docs"
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
  - "图像 [Windows 窗体], 反射"
  - "图像 [Windows 窗体], 旋转"
  - "图像 [Windows 窗体], 扭曲"
ms.assetid: a3bf97eb-63ed-425a-ba07-dcc65efb567c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：旋转、反射和扭曲图像
通过指定原始图像的左上角、右上角和左下角的目标点可旋转、反射和扭曲图像。  这三个目标点确定将原始矩形图像映射为平行四边形的仿射变换。  
  
## 示例  
 例如，假设原始图像是一个矩形，其左上角、右上角和左下角分别位于 \(0, 0\)、\(100, 0\) 和 \(0, 50\)。  现在假设我们将这三个点按以下方式映射到目标点。  
  
|原始点|目标点|  
|---------|---------|  
|左上角 \(0, 0\)|\(200, 20\)|  
|右上角 \(100, 0\)|\(110, 100\)|  
|左下角 \(0, 50\)|\(250, 30\)|  
  
 下面的插图显示原始图像以及映射为平行四边形的图像。  原始图像已被扭曲、反射、旋转和平移。  沿着原始图像上边缘的 x 轴被映射到通过 \(200, 20\) 和 \(110, 100\) 的直线。  沿着原始图像左边缘的 y 轴被映射到通过 \(200, 20\) 和 \(250, 30\) 的直线。  
  
 ![带区](../../../../docs/framework/winforms/advanced/media/stripes1.gif "Stripes1")  
  
 下面的插图显示应用到照片图像的类似变换。  
  
 ![已转换的 Climber](../../../../docs/framework/winforms/advanced/media/transformedclimber.png "TransformedClimber")  
  
 下面的插图显示应用到图元文件的类似变换。  
  
 ![已转换的元文件](../../../../docs/framework/winforms/advanced/media/transformedmetafile.png "TransformedMetafile")  
  
 下面的示例生成第一个插图中所显示的图像。  
  
 [!code-csharp[System.Drawing.WorkingWithImages#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.WorkingWithImages#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#61)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  请确保用系统上有效的图像路径替换 `Stripes.bmp`。  
  
## 请参阅  
 [使用图像、位图、图标和图元文件](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)