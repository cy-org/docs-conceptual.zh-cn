---
title: "如何：使 Tab 键能够移出 ToolStrip 控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 在控件之间移动"
  - "Tab 键, 启用"
  - "ToolStrip 控件 [Windows 窗体], 移出"
ms.assetid: 40f9e88b-09a3-428e-8da8-c00bb65079c6
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使 Tab 键能够移出 ToolStrip 控件
使用以下过程可以使用户按 Tab 键就能以 Tab 键顺序从 <xref:System.Windows.Forms.ToolStrip> 移出到下一个控件。  
  
 <xref:System.Windows.Forms.ToolStrip> 接受第一次按 Tab 键，然后箭头键选择 <xref:System.Windows.Forms.ToolStrip> 内的项。  用户第二次按 Tab 键时，将按 Tab 键顺序移到下一个控件。  
  
### 使用户能够按 Tab 键便从 ToolStrip 移出到下一个控件  
  
-   将 <xref:System.Windows.Forms.ToolStrip> 的 <xref:System.Windows.Forms.ToolStrip.TabStop%2A> 属性设置为 `true`。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStrip.TabStop%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)