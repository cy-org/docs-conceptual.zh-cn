---
title: "如何：在形状中平铺图像 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 填充形状"
  - "图像 [Windows 窗体], 填充形状"
  - "形状, 使用图像平铺显示"
  - "纹理画笔, 平铺显示图像"
ms.assetid: 6d407891-6e5c-4495-a546-3da5604e9fb8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：在形状中平铺图像
正如瓷砖可一块挨一块地放置以覆盖地面一样，矩形图像也可一个挨一个地放置以填充（平铺）形状。  若要平铺形状的内部，请使用纹理画笔。  在构造 <xref:System.Drawing.TextureBrush> 对象时，传递给构造函数的一个参数是 <xref:System.Drawing.Image> 对象。  在使用纹理画笔为形状的内部涂色时，将用该图像的重复副本填充该形状。  
  
 <xref:System.Drawing.TextureBrush> 对象的覆盖模式属性确定图像在矩形网格中重复时的定向方式。  既可让网格中所有平铺图像的方向都相同，也可让平铺图像在相邻网格间翻转。  可水平或垂直翻转，也可同时进行水平和垂直翻转。  下面的示例演示用不同类型的翻转进行平铺。  
  
### 平铺图像  
  
-   该示例使用下面的 75×75 图像来平铺 200×200 的矩形。  
  
 ![平铺 1](../../../../docs/framework/winforms/advanced/media/tile1.png "tile1")  
  
-   下面的插图显示如何使用图像平铺此矩形。  请注意，所有的平铺图像都采用相同的方向，没有翻转。  
  
 ![平铺 2](../../../../docs/framework/winforms/advanced/media/tile2.png "tile2")  
  
 [!code-csharp[System.Drawing.UsingABrush#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingABrush#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#31)]  
  
### 平铺时水平翻转图像  
  
-   该示例使用相同的 75×75 图像来填充 200×200 的矩形。  覆盖模式被设置为水平翻转图像。  下面的插图显示如何使用图像平铺此矩形。  请注意，在给定行中从一个平铺图像移到下一个时，图像将水平翻转。  
  
 ![平铺 3](../../../../docs/framework/winforms/advanced/media/tile3.png "tile3")  
  
 [!code-csharp[System.Drawing.UsingABrush#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.UsingABrush#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#32)]  
  
### 平铺时垂直翻转图像  
  
-   该示例使用相同的 75×75 图像来填充 200×200 的矩形。  覆盖模式被设置为垂直翻转图像。  
  
     [!code-csharp[System.Drawing.UsingABrush#33](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#33)]
     [!code-vb[System.Drawing.UsingABrush#33](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#33)]  
  
### 平铺时水平和垂直翻转图像  
  
-   该示例使用相同的 75×75 图像来平铺 200×200 的矩形。  覆盖模式被设置为同时在水平和垂直方向翻转图像。  下面的插图显示如何使用图像平铺此矩形。  请注意，在给定行中从一个平铺图像移到下一个时，图像将水平翻转；在给定列中从一个平铺图像移到下一个时，图像将被垂直翻转。  
  
 ![平铺 5](../../../../docs/framework/winforms/advanced/media/tile5.png "tile5")  
  
 [!code-csharp[System.Drawing.UsingABrush#34](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#34)]
 [!code-vb[System.Drawing.UsingABrush#34](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#34)]  
  
## 请参阅  
 [使用画笔填充形状](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)