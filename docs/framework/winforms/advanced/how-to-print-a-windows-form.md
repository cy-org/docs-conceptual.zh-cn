---
title: "如何：打印 Windows 窗体 | Microsoft Docs"
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
  - "打印 [Windows 窗体], 打印窗体"
  - "打印 [Windows 窗体]"
  - "打印窗体"
  - "Windows 窗体, 打印"
ms.assetid: c8dff5f8-f56a-4c07-ae31-64643b31f8fc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：打印 Windows 窗体
作为开发过程的一部分，通常会希望打印 Windows 窗体的副本。  下面的代码示例演示如何使用 <xref:System.Drawing.Graphics.CopyFromScreen%2A> 方法来打印当前窗体的副本。  
  
## 示例  
 [!code-csharp[System.Drawing.Graphics.CopyFromScreen#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/CS/Form1.cs#1)]
 [!code-vb[System.Drawing.Graphics.CopyFromScreen#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Graphics.CopyFromScreen/VB/Form1.vb#1)]  
  
## 编译代码  
 这是一个完整的代码示例，其中包含 `Main` 方法。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   您没有访问该打印机的权限。  
  
-   没有安装打印机。  
  
## .NET Framework 安全性  
 为了运行此代码示例，您必须能够访问与计算机一起使用的打印机。  
  
## 请参阅  
 <xref:System.Drawing.Printing.PrintDocument>   
 [如何：使用 GDI\+ 呈现图像](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)   
 [如何：在 Windows 窗体中打印图形](../../../../docs/framework/winforms/advanced/how-to-print-graphics-in-windows-forms.md)