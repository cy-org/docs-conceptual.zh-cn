---
title: "如何：将 ToolStrip 从 ToolStripContainer 移到窗体上 | Microsoft Docs"
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
  - "ToolStrip 控件 [Windows 窗体], 将窗体用作父级"
  - "Windows 窗体, 作为 ToolStrip 控件的父级"
ms.assetid: a1c94a7f-6fc5-4e4c-84cf-ff11dc573d33
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：将 ToolStrip 从 ToolStripContainer 移到窗体上
使用下面的过程将一个 <xref:System.Windows.Forms.ToolStrip> 从 <xref:System.Windows.Forms.ToolStripContainer> 移到窗体上。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 将 ToolStrip 从 ToolStripContainer 移到窗体上  
  
1.  选择 <xref:System.Windows.Forms.ToolStrip>。  
  
2.  通过按 Ctrl\+X 或右击 <xref:System.Windows.Forms.ToolStrip> 再从上下文菜单中选择**“剪切”**来剪切 <xref:System.Windows.Forms.ToolStrip>。  
  
3.  选择窗体。  
  
4.  通过按 Ctrl\+V 或从**“编辑”**菜单选择**“粘贴”**来粘贴 <xref:System.Windows.Forms.ToolStrip>。  
  
5.  将 <xref:System.Windows.Forms.ToolStrip> 的 <xref:System.Windows.Forms.ToolStrip.Dock%2A> 属性设置为**“Top”**。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripContainer>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)