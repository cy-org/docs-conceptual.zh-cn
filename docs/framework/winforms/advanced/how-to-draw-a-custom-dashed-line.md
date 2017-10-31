---
title: "如何：绘制自定义虚线 | Microsoft Docs"
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
  - "文本行, 自定义"
  - "文本行, 虚线"
  - "文本行, 绘图"
ms.assetid: cd0ed96a-cce4-47b9-b58a-3bae2e3d1bee
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：绘制自定义虚线
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供 <xref:System.Drawing.Drawing2D.DashStyle> 枚举中列出的几种虚线样式。  如果这些标准的虚线样式不能满足需求，则可创建自定义的虚线模式。  
  
## 示例  
 若要绘制自定义虚线，请将短划线和间距的长度放在一个数组中，并将该数组指定为 <xref:System.Drawing.Pen> 对象的 <xref:System.Drawing.Pen.DashPattern%2A> 属性的值。  下面的示例绘制了一条基于  `{5, 2, 15, 4}` 数组的自定义的虚线。  如果将数组元素乘以钢笔的宽度 5，可得到 `{25, 10, 75, 20}`。  显示的短划线的长度在 25 和 75 之间交替，间距的长度在 10 和 20 之间交替。  
  
 下面的插图显示结果虚线。  请注意，最后一段短划线不得不短于 25 个单位，以便线条的终点落在 \(405, 5\) 上。  
  
 ![钢笔](../../../../docs/framework/winforms/advanced/media/pens6.png "pens6")  
  
 [!code-csharp[System.Drawing.UsingAPen#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.UsingAPen#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#51)]  
  
## 编译代码  
 创建一个 Windows 窗体并处理窗体的 <xref:System.Windows.Forms.Control.Paint> 事件。  将上面的代码粘贴到 <xref:System.Windows.Forms.Control.Paint> 事件处理程序中。  
  
## 请参阅  
 [使用钢笔绘制线条和形状](../../../../docs/framework/winforms/advanced/using-a-pen-to-draw-lines-and-shapes.md)