---
title: "如何：调整 Windows 窗体标签控件大小以适应其内容 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "标题, 调整大小"
  - "Label 控件 [Windows 窗体], 调整大小以适应内容"
  - "标签, 调整大小以适应内容"
  - "大小, 控件"
  - "调整控件大小"
ms.assetid: 99648964-63b2-438c-980e-d24103ad602b
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：调整 Windows 窗体标签控件大小以适应其内容
Windows 窗体 <xref:System.Windows.Forms.Label> 控件可为单行或多行，可以为固定大小，也可以自动调整自身大小以容纳其标题。  <xref:System.Windows.Forms.Label.AutoSize%2A> 属性帮助您调整控件大小以适应较大或较小的标题。如果标题在运行时会发生更改，这个属性尤为有用。  
  
### 使标签控件 \(Label\) 动态调整大小以适应其内容  
  
1.  将其 <xref:System.Windows.Forms.Label.AutoSize%2A> 属性设置为 `true`。  
  
 如果将 <xref:System.Windows.Forms.Label.AutoSize%2A> 设置为 `false`，则在 <xref:System.Windows.Forms.Label.Text%2A> 属性中指定的文字将切换到下一行（如果可能），但该控件不会增大。  
  
## 请参阅  
 [如何：使用 Windows 窗体 Label 控件创建访问键](../../../../docs/framework/winforms/controls/how-to-create-access-keys-with-windows-forms-label-controls.md)   
 [Label 控件概述](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)   
 [Label 控件](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)