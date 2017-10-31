---
title: "如何：填充开放图形 | Microsoft Docs"
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
  - "图形, 填充"
  - "打开图形, 填充"
ms.assetid: 5a36b0e4-f1f4-46c0-a85a-22ae98491950
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：填充开放图形
可通过将 <xref:System.Drawing.Drawing2D.GraphicsPath> 对象传递给 <xref:System.Drawing.Graphics.FillPath%2A> 方法来填充轨迹。  <xref:System.Drawing.Graphics.FillPath%2A> 方法根据当前为轨迹设置的填充模式（交替或缠绕）填充轨迹。  如果轨迹包含任何非闭合图形，则也会像这些图形是闭合图形一样来填充轨迹。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 通过绘制一条从图形终点到起点的直线来闭合图形。  
  
## 示例  
 下面的示例创建包含一个非闭合图形（弧）和一个闭合式图形（椭圆）的轨迹。  <xref:System.Drawing.Graphics.FillPath%2A> 方法按照默认的填充模式（即 <xref:System.Drawing.Drawing2D.FillMode>）填充轨迹。  
  
 下面的插图显示代码示例的输出。  请注意，如同用一条从开放式图形终点到起点的直线闭合了非闭合图形一样填充了轨迹（<xref:System.Drawing.Drawing2D.FillMode>）。  
  
 ![填充开放路径](../../../../docs/framework/winforms/advanced/media/fillopenpath.png "FillOpenPath")  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#11)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Drawing2D.GraphicsPath>   
 [GDI\+ 中的图形路径](../../../../docs/framework/winforms/advanced/graphics-paths-in-gdi.md)