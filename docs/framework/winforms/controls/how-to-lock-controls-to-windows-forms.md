---
title: "如何：将控件锁定到 Windows 窗体 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 锁定"
  - "Windows 窗体控件, 锁定"
ms.assetid: 94efe0d2-c14e-4d14-b903-63ea9b07e290
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：将控件锁定到 Windows 窗体
当设计 Windows 应用程序的用户界面 \(UI\) 时，正确定位控件后可将其锁定，以免在设置其他属性时意外移动它或调整其大小。  
  
 另外，可一次锁定或取消锁定窗体上的所有控件，这对于有许多控件的窗体很有帮助，也可以取消锁定个别控件。  将所有控件放在窗体上的所需位置后，可就地锁定它们以防止错误的移动。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 锁定控件  
  
1.  在**“属性”**窗口中，单击**“Locked”**属性并选择 `true`。  （双击该名称将切换属性设置。）  
  
     此外，还可以右击控件并选择**“锁定控件”**。  
  
    > [!NOTE]
    >  锁定控件可以防止它们被拖动为新的大小或被拖动到设计图面上的其他位置。  然而，您仍可以通过**“属性”**窗口或在代码中更改控件的大小或位置。  
  
### 锁定窗体上的所有控件  
  
1.  从**“格式”**菜单中选择**“锁定控件”**。  
  
    > [!NOTE]
    >  此命令也会锁定窗体的大小，因为窗体是控件。  
  
### 取消锁定窗体上的所有锁定控件  
  
1.  从**“格式”**菜单中选择**“锁定控件”**。  
  
     窗体上所有以前锁定的控件现已被取消锁定。  
  
### 取消锁定个别的锁定控件  
  
1.  在**“属性”**窗口中，单击**“Locked”**属性并选择 `false`。  （双击该名称将切换属性设置。）  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)