---
title: "使用嵌套的 Graphics 容器 | Microsoft Docs"
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
  - "图形 [Windows 窗体], 剪辑"
  - "图形, 嵌套的容器"
  - "图形, 嵌套对象中的转换"
ms.assetid: a0d9f178-43a4-4323-bb5a-d3e3f77ae6c1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 使用嵌套的 Graphics 容器
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供可用于在 <xref:System.Drawing.Graphics> 对象中临时替换或增加状态部件的容器。  通过调用 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.BeginContainer%2A> 方法创建容器。  可重复调用 <xref:System.Drawing.Graphics.BeginContainer%2A> 以形成嵌套容器。  每调用一次 <xref:System.Drawing.Graphics.BeginContainer%2A>，都要调用一次 <xref:System.Drawing.Graphics.EndContainer%2A>。  
  
## 嵌套容器中的变换  
 下面的示例创建一个 <xref:System.Drawing.Graphics> 对象并在该 <xref:System.Drawing.Graphics> 对象中创建一个容器。  <xref:System.Drawing.Graphics> 对象的世界变换是在 x 方向平移 100 个单位，在 y 方向平移 80 个单位。  该容器的世界变换是旋转 30 度。  该代码调用两次  `DrawRectangle(pen, -60, -30, 120, 60)` 。  对 <xref:System.Drawing.Graphics.DrawRectangle%2A> 的第一次调用是在容器的内部，也就是说，此调用是在调用 <xref:System.Drawing.Graphics.BeginContainer%2A> 和 <xref:System.Drawing.Graphics.EndContainer%2A> 之间发生的。  对 <xref:System.Drawing.Graphics.DrawRectangle%2A> 的第二次调用是在调用 <xref:System.Drawing.Graphics.EndContainer%2A> 之后。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#61](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.MiscLegacyTopics#61](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#61)]  
  
 在上面的代码中，从容器内部绘制的矩形依次经过容器的世界变换（旋转）和 <xref:System.Drawing.Graphics> 对象的世界变换（平移）。  从容器外部绘制的矩形只经过 <xref:System.Drawing.Graphics> 对象的世界变换（平移）。  下面的插图显示这两个矩形。  
  
 ![嵌套容器](../../../../docs/framework/winforms/advanced/media/csnestedcontainers1.png "csnestedcontainers1")  
  
## 在嵌套容器中剪辑  
 下面的示例演示嵌套容器如何处理剪辑区域。  该代码创建一个 <xref:System.Drawing.Graphics> 对象并在该 <xref:System.Drawing.Graphics> 对象中创建一个容器。  <xref:System.Drawing.Graphics> 对象的剪辑区域是矩形，容器的剪辑区域是椭圆。  该代码调用两次 <xref:System.Drawing.Graphics.DrawLine%2A> 方法。  第一次调用 <xref:System.Drawing.Graphics.DrawLine%2A> 是在容器内部，第二次调用 <xref:System.Drawing.Graphics.DrawLine%2A> 是在容器的外部（在调用 <xref:System.Drawing.Graphics.EndContainer%2A> 之后）。  第一条直线被两个剪辑区域的相交部分剪辑。  第二条直线只被 <xref:System.Drawing.Graphics> 对象的矩形剪辑区域剪辑。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#62](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#62)]
 [!code-vb[System.Drawing.MiscLegacyTopics#62](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#62)]  
  
 下面的插图显示这两条剪辑过的直线。  
  
 ![嵌套容器](../../../../docs/framework/winforms/advanced/media/nestedcontainers2.png "nestedcontainers2")  
  
 正如上面的示例所示，变换和剪辑区域在嵌套容器中是累积的。  如果设置容器和 <xref:System.Drawing.Graphics> 对象的世界变换，则这两种变换都将应用于从容器内部绘制的项目。  首先应用容器的变换，再应用 <xref:System.Drawing.Graphics> 对象的变换。  如果设置容器和 <xref:System.Drawing.Graphics> 对象的剪辑区域，则从容器内部绘制的项目将被两个剪辑区域的相交部分剪辑。  
  
## 嵌套容器中的品质设置  
 嵌套容器中的品质设置（<xref:System.Drawing.Graphics.SmoothingMode%2A> 和 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 等）是不累积的；相反，容器的品质设置会临时替换 <xref:System.Drawing.Graphics> 对象的品质设置。  在创建新容器时，该容器的品质设置将被设置为默认值。  例如，假设有一个 <xref:System.Drawing.Graphics> 对象，其平滑模式为 <xref:System.Drawing.Drawing2D.SmoothingMode>。  在创建容器时，容器内部的平滑模式是默认的平滑模式。  您可随意设置该容器的平滑模式，而在容器内部绘制的任何项目将按照您所设置的模式绘制。  在调用 <xref:System.Drawing.Graphics.EndContainer%2A> 之后绘制的项目，将按照在调用 <xref:System.Drawing.Graphics.BeginContainer%2A> 之前就已设置好的 \(<xref:System.Drawing.Drawing2D.SmoothingMode>\) 平滑模式绘制。  
  
## 多层嵌套容器  
 在 <xref:System.Drawing.Graphics> 对象中，并不限于只有一个容器。  您可创建一系列容器，每个容器都嵌套在前一个容器中；您可为每个嵌套容器指定世界变换、剪辑区域和品质设置。  如果从最里边的容器内部调用绘图方法，则变换将按顺序应用，即，始于最里边的容器，终于最外边的容器。  从最里边的容器内部绘制的项目将被所有剪辑区域的相交部分剪辑。  
  
 下面的示例创建 <xref:System.Drawing.Graphics> 对象并将其文本呈现提示设置为 <xref:System.Drawing.Drawing2D.SmoothingMode>。  该代码创建两个容器，一个嵌套在另一个中。  外部容器和内部容器的文本呈现提示分别设置为 <xref:System.Drawing.Text.TextRenderingHint> 和 <xref:System.Drawing.Drawing2D.SmoothingMode>。  该代码绘制三个字符串：一个从内部容器绘制，另一个从外部容器绘制，第三个从 <xref:System.Drawing.Graphics> 对象本身绘制。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#63](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#63)]
 [!code-vb[System.Drawing.MiscLegacyTopics#63](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#63)]  
  
 下面的插图显示这三个字符串。  从内部容器和 <xref:System.Drawing.Graphics> 对象绘制的字符串都由“抗锯齿”平滑。  从外部容器绘制的字符串不由“抗锯齿”平滑，这是由于 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 属性被设置为 <xref:System.Drawing.Text.TextRenderingHint>。  
  
 ![嵌套容器](../../../../docs/framework/winforms/advanced/media/nestedcontainers3.png "nestedcontainers3")  
  
## 请参阅  
 <xref:System.Drawing.Graphics>   
 [管理 Graphics 对象的状态](../../../../docs/framework/winforms/advanced/managing-the-state-of-a-graphics-object.md)