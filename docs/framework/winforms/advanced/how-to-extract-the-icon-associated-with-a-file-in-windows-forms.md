---
title: "如何：提取与 Windows 窗体中的文件关联的图标 | Microsoft Docs"
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
  - "在 ListView 控件中显示文件名及其文件类型图标 [Windows 窗体]"
  - "提取与文件类型关联的图标 [Windows 窗体]"
  - "文件扩展名图标 [Windows 窗体], 在 ListView 中显示"
ms.assetid: 88e2ad8b-c34f-415a-84f2-dad756b5c928
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：提取与 Windows 窗体中的文件关联的图标
很多文件都有嵌入式图标，为关联的文件类型提供可视化表示形式。  例如，Microsoft Word 文档包含一个将其标识为 Word 文档的图标。  在列表控件或表控件中显示文件时，您可能希望将表示文件类型的图标显示在每个文件名旁边。  可以使用 <xref:System.Drawing.Icon.ExtractAssociatedIcon%2A> 方法轻松实现此目的。  
  
## 示例  
 下面的代码示例演示如何提取与文件关联的图标并在 <xref:System.Windows.Forms.ListView> 控件中显示文件名及其关联图标。  
  
 [!code-csharp[System.Drawing.Icon.ExtractAssociatedIconEx#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Icon.ExtractAssociatedIconEx#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Icon.ExtractAssociatedIconEx/VB/Form1.vb#1)]  
  
## 编译代码  
 编译此示例：  
  
-   将前面的代码粘贴到一个 Windows 窗体中，并从该窗体的构造函数或 <xref:System.Windows.Forms.Form.Load> 事件处理方法中调用 `ExtractAssociatedIconExample` 方法。  
  
     您需要确保窗体导入 <xref:System.IO> 命名空间。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [ListView 控件](../../../../docs/framework/winforms/controls/listview-control-windows-forms.md)