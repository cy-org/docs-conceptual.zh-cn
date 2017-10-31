---
title: "如何：在 ToolStrip 控件中创建切换按钮 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具栏"
  - "切换按钮, 创建"
  - "ToolStrip 控件 [Windows 窗体], 创建切换按钮"
ms.assetid: d9c197df-4c65-43f2-beee-b68b52b2befc
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 ToolStrip 控件中创建切换按钮
用户单击切换按钮时，按钮显示为凹陷，并且凹陷外观会保持到用户再次单击按钮为止。  
  
### 创建切换 ToolStripButton  
  
-   使用类似下面的代码示例的代码。  此代码假定您的窗体包含一个 <xref:System.Windows.Forms.ToolStrip> 控件，并且其 <xref:System.Windows.Forms.ToolStrip.Items%2A> 集合包含一个名为 `toolStripButton1` 的 <xref:System.Windows.Forms.ToolStripButton>。  它还假定您已经具有一个名为 `toolStripButton1_CheckedChanged` 的事件处理程序。  
  
     \[Visual Basic\]  
  
    ```  
    toolStripButton1.CheckOnClick = True  
    toolStripButton1.CheckedChanged AddressOf _  
    EventHandler(toolStripButton1_CheckedChanged);  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStripButton1.CheckOnClick = true;  
    toolStripButton1.CheckedChanged += new _  
    EventHandler(toolStripButton1_CheckedChanged);  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripButton>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)