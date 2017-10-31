---
title: "GDI+ 中的图元文件 | Microsoft Docs"
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
  - "GDI+, 图元文件"
  - "图像 [Windows 窗体], 图元文件"
  - "图元文件"
ms.assetid: 51da872c-c783-440f-8bf6-1e580a966c31
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# GDI+ 中的图元文件
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供 <xref:System.Drawing.Imaging.Metafile> 类，以便能够记录和显示图元文件。  图元文件，也称为矢量图像，是一种存储为一系列绘图命令和设置的图像。  <xref:System.Drawing.Imaging.Metafile> 对象记录的命令和设置可存储在内存中，或者保存到文件或流。  
  
## 图元文件格式  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 能够显示以以下格式存储的图元文件：  
  
-   Windows 图元文件 \(WMF\)  
  
-   增强性图元文件 \(EMF\)  
  
-   EMF\+  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 能够用 EMF 和 EMF\+ 格式记录图元文件，但不能使用 WMF 格式。  
  
 EMF\+ 是对 EMF 的扩展，可存储 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 记录。  EMF\+ 格式有两种变体：“EMF\+ 唯一”和“EMF\+ 双重”。  “EMF\+ 唯一”图元文件只包含 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 记录。  此类图元文件可以由 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 显示，但不能由 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 显示。  “EMF\+ 双重”图元文件包含 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 和 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 记录。  “EMF\+ 双重”图元文件中的每个 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 记录与一个备用的 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 记录成对使用。  此类图元文件可以由 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 或 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 显示。  
  
 下面的示例显示了一个以前另存为文件的图元文件。  该图元文件在显示时，左上角的位置是 \(100，100\)。  
  
 [!code-csharp[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.ImagesBitmapsMetafiles#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ImagesBitmapsMetafiles/VB/Class1.vb#21)]  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)