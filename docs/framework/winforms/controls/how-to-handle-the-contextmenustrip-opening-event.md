---
title: "如何：处理 ContextMenuStrip 打开事件 | Microsoft Docs"
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
  - "上下文菜单, 事件处理"
  - "ContextMenuStrip 控件 [Windows 窗体]"
  - "事件处理, 上下文菜单"
  - "快捷菜单, 事件处理"
  - "ToolStrip 控件 [Windows 窗体]"
ms.assetid: b661b3dd-7815-4cc2-a1aa-a9a391ab3427
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：处理 ContextMenuStrip 打开事件
可以通过处理 <xref:System.Windows.Forms.ToolStripDropDown.Opening> 事件来自定义 <xref:System.Windows.Forms.ContextMenuStrip> 控件的行为。  
  
## 示例  
 下面的代码示例演示如何处理 <xref:System.Windows.Forms.ToolStripDropDown.Opening> 事件。  事件处理程序将项动态添加到 <xref:System.Windows.Forms.ContextMenuStrip> 控件中。  有关完整的代码示例，请参见[如何：动态添加 ToolStrip 项](../../../../docs/framework/winforms/controls/how-to-add-toolstrip-items-dynamically.md)。  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#42](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#42)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#42](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#42)]  
  
 将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A?displayProperty=fullName> 属性设置为 `true` 可以使菜单无法打开。  
  
## 请参阅  
 <xref:System.Windows.Forms.ContextMenuStrip>   
 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A>   
 <xref:System.Windows.Forms.ToolStripDropDown>   
 [ToolStrip 控件](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)