---
title: "如何：向 ToolStripMenuItem 添加增强功能 | Microsoft Docs"
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
  - "选中标记, 添加到菜单"
  - "命令 [Windows 窗体], 对菜单进行分组"
  - "图像 [Windows 窗体], 添加到菜单"
  - "键盘快捷键, 在菜单上显示"
  - "菜单项, 添加选中标记"
  - "菜单项, 添加图像"
  - "菜单项, 显示访问键"
  - "菜单项, 显示快捷键"
  - "菜单项, 显示分隔符"
  - "菜单, 分组命令"
  - "分隔符, 在菜单上显示"
  - "ToolStripMenuItems"
  - "ToolStripMenuItems, 添加选中标记"
  - "ToolStripMenuItems, 添加图像"
  - "ToolStripMenuItems, 显示访问键"
  - "ToolStripMenuItems, 显示快捷键"
  - "ToolStripMenuItems, 显示分隔线"
  - "ToolStripSeparators, 在 MenuStrips 上显示"
ms.assetid: aa5f19bb-b545-4378-bfa6-36ba592f0d7c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：向 ToolStripMenuItem 添加增强功能
可以采用下列方式增强 <xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 控件的可用性：  
  
-   添加选中标记以指定打开或关闭某项功能（例如是否沿字处理应用程序的边距显示标尺），或指示显示的是一列文件中的哪一个（如在**“窗口”**菜单上）。  
  
-   添加可视化地表示菜单命令的图像。  
  
-   显示快捷键以提供代替鼠标执行命令的键盘。  例如，按 Ctrl\+C 执行 **Copy** 命令。  
  
-   显示访问键以提供代替鼠标进行菜单导航的键盘。  例如，按 Alt\+F 选择**“文件”**菜单。  
  
-   显示分隔线以便对相关命令进行分组，提高菜单的可读性。  
  
### 显示菜单命令的选中标记  
  
-   将其 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 属性设置为 `true`。  
  
     这会将 <xref:System.Windows.Forms.ToolStripMenuItem.CheckState%2A> 属性也设置为 `true`。  仅在以下情况使用此过程：无论是否选择菜单命令，只要该命令出现，都希望默认情况下为选中状态。  
  
### 显示随每次单击更改状态的选中标记  
  
-   将菜单命令的 <xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A> 属性设置为 `true`。  
  
### 向菜单命令添加图像  
  
-   将菜单命令的 <xref:System.Windows.Forms.ToolStripItem.Image%2A> 属性设置为图像的名称。  如果此菜单命令的 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 属性设置为 <xref:System.Windows.Forms.ToolStripItemDisplayStyle> 或 <xref:System.Windows.Forms.ToolStripItemDisplayStyle>，则无法显示该图像。  
  
> [!NOTE]
>  图像边距也可以显示选中标记（如果您选择）。  此外，您还可以将图像的 <xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A> 属性设置为 `true`，这样，在运行时显示的图像周围将带有一个阴影框。  
  
### 显示菜单命令的快捷键  
  
-   将菜单命令的 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A> 属性设置为所需的键盘组合（如 Ctrl\+O 表示**“打开”**菜单命令），并将 <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> 属性设置为 `true`。  
  
### 显示菜单命令的自定义快捷键  
  
-   将菜单命令的 <xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A> 属性设置为所需的键盘组合（如 Ctrl\+Shift\+O，而不是 Shift\+Ctrl\+O），并将 <xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A> 属性设置为 `true`。  
  
### 显示菜单命令的访问键  
  
-   设置菜单命令的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性时，在您要为其加上下划线以作为访问键的字母前面输入一个“and”符 \(&\)。  例如，键入  `&Open`  作为菜单项的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性将使菜单命令显示为 **O**pen。  
  
     若要定位到此菜单命令，请按 Alt 键使 <xref:System.Windows.Forms.MenuStrip> 得到焦点，然后按该菜单名的访问键。  当菜单打开并显示带访问键的项时，只需按访问键就可选择菜单命令。  
  
> [!NOTE]
>  避免定义重复的访问键，如在同一个菜单系统中两次定义 Alt\+F。  重复访问键的选择顺序无法保证。  
  
### 在菜单命令之间显示分隔线  
  
-   定义了 <xref:System.Windows.Forms.MenuStrip> 及其包含的项之后，请使用 <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A> 或 <xref:System.Windows.Forms.ToolStripItemCollection.Add%2A> 方法将菜单命令和 <xref:System.Windows.Forms.ToolStripSeparator> 控件按所需顺序添加到 <xref:System.Windows.Forms.MenuStrip> 中。  
  
     \[Visual Basic\]  
  
    ```  
    ' This code adds a top-level File menu to the MenuStrip.  
    Me.menuStrip1.Items.Add(New ToolStripMenuItem() _  
    {Me.fileToolStripMenuItem})  
  
    ' This code adds the New and Open menu commands, a separator bar,   
    ' and the Save and Exit menu commands to the top-level File menu,   
    ' in that order.  
    Me.fileToolStripMenuItem.DropDownItems.AddRange(New _  
    ToolStripMenuItem() {Me.newToolStripMenuItem, _  
    Me.openToolStripMenuItem, Me.toolStripSeparator1, _  
    Me.saveToolStripMenuItem, Me.exitToolStripMenuItem})  
  
    ```  
  
     \[C\#\]  
  
    ```  
    // This code adds a top-level File menu to the MenuStrip.  
    this.menuStrip1.Items.Add(new ToolStripItem[]_  
    {this.fileToolStripMenuItem});  
  
    // This code adds the New and Open menu commands, a separator bar,   
    // and the Save and Exit menu commands to the top-level File menu,   
    // in that order.  
    this.fileToolStripMenuItem.DropDownItems.AddRange(new _  
    ToolStripItem[] {  
    this.newToolStripMenuItem,  
    this.openToolStripMenuItem,  
    this.toolStripSeparator1,  
    this.saveToolStripMenuItem,  
    this.exitToolStripMenuItem});  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.MenuStrip>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [MenuStrip 控件概述](../../../../docs/framework/winforms/controls/menustrip-control-overview-windows-forms.md)