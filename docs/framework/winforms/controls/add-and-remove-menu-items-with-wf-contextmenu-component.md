---
title: "如何：使用 Windows 窗体 ContextMenu 组件添加和移除菜单项 | Microsoft Docs"
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
  - "上下文菜单, 添加项"
  - "上下文菜单, 示例"
  - "上下文菜单, 移除项"
  - "ContextMenu 组件 [Windows 窗体], 添加项"
  - "ContextMenu 组件 [Windows 窗体], 移除项"
  - "示例 [Windows 窗体], 上下文菜单"
  - "快捷菜单, 添加项"
  - "快捷菜单, 示例"
  - "快捷菜单, 移除项"
ms.assetid: 426d1eaf-7fb8-4b0b-8a33-5e8721786ea4
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用 Windows 窗体 ContextMenu 组件添加和移除菜单项
说明如何在 Windows 窗体中添加和移除快捷菜单项。  
  
 Windows 窗体 <xref:System.Windows.Forms.ContextMenu> 组件提供与选定对象相关的常用命令的菜单。  可以通过向 <xref:System.Windows.Forms.Menu.MenuItems%2A> 集合中添加 <xref:System.Windows.Forms.MenuItem> 对象来向快捷菜单中添加项。  
  
 可以从快捷菜单中永久地移除项；但是在运行时隐藏或禁用项可能更为妥当。  
  
> [!IMPORTANT]
>  尽管 <xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 取代了早期版本的 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 控件并添加了功能，但是，可以选择保留 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 以实现向后兼容并供将来使用。  
  
### 从快捷菜单中移除项  
  
1.  使用 <xref:System.Windows.Forms.ContextMenu> 组件的 <xref:System.Windows.Forms.Menu.MenuItems%2A> 集合的 <xref:System.Windows.Forms.Menu.MenuItemCollection.Remove%2A> 或 <xref:System.Windows.Forms.Menu.MenuItemCollection.RemoveAt%2A> 方法移除特定菜单项。  
  
    ```vb  
    ' Removes the first item in the shortcut menu.  
    ContextMenu1.MenuItems.RemoveAt(0)  
    ' Removes a particular object from the shortcut menu.  
    ContextMenu1.MenuItems.Remove(mnuItemNew)  
  
    ```  
  
    ```csharp  
    // Removes the first item in the shortcut menu.  
    contextMenu1.MenuItems.RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1.MenuItems.Remove(mnuItemNew);  
  
    ```  
  
    ```cpp  
    // Removes the first item in the shortcut menu.  
    contextMenu1->MenuItems->RemoveAt(0);  
    // Removes a particular object from the shortcut menu.  
    contextMenu1->MenuItems->Remove(mnuItemNew);  
    ```  
  
     \- 或 \-  
  
2.  使用 <xref:System.Windows.Forms.ContextMenu> 组件的 `MenuItems` 集合的 `Clear` 方法，移除菜单中的所有项。  
  
    ```vb  
    ContextMenu1.MenuItems.Clear()  
  
    ```  
  
    ```csharp  
    contextMenu1.MenuItems.Clear();  
  
    ```  
  
    ```cpp  
    contextMenu1->MenuItems->Clear();  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ContextMenu>   
 [ContextMenu 组件](../../../../docs/framework/winforms/controls/contextmenu-component-windows-forms.md)   
 [ContextMenu 组件概述](../../../../docs/framework/winforms/controls/contextmenu-component-overview-windows-forms.md)