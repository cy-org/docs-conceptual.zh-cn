---
title: "如何：向 ContextMenuStrip 添加菜单项 | Microsoft Docs"
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
  - "上下文菜单, 添加菜单项"
  - "ContextMenuStrips, 添加菜单项"
  - "快捷菜单, 添加项"
ms.assetid: 1ec14776-3ea2-4752-bd22-4fae0fd19e1a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：向 ContextMenuStrip 添加菜单项
一次只能向 <xref:System.Windows.Forms.ContextMenuStrip> 添加一个或几个菜单项。  
  
### 将单个菜单项添加到 ContextMenuStrip  
  
-   使用 <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> 方法可向 <xref:System.Windows.Forms.ContextMenuStrip> 添加一个菜单项。  
  
     \[Visual Basic\]  
  
    ```  
    Me.contextMenuStrip1.Items.Add(Me.toolStripMenuItem1)  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.Add(toolStripMenuItem1);  
    ```  
  
### 将几个菜单项添加到 ContextMenuStrip  
  
-   使用 <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> 方法可向 <xref:System.Windows.Forms.ContextMenuStrip> 添加若干菜单项。  
  
     \[Visual Basic\]  
  
    ```  
    Me.contextMenuStrip1.Items.AddRange(New _  
       System.Windows.Forms.ToolStripItem() {Me.toolStripMenuItem1, _  
          Me.toolStripMenuItem2})  
    ```  
  
    ```csharp  
    this.contextMenuStrip1.Items.AddRange(new   
       System.Windows.Forms.ToolStripItem[] {  
          this.toolStripMenuItem1, this.toolStripMenuItem2});  
    ```  
  
## 请参阅  
 [ContextMenuStrip 控件](../../../../docs/framework/winforms/controls/contextmenustrip-control.md)