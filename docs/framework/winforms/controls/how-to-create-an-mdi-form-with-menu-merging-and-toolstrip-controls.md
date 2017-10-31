---
title: "如何：创建合并了菜单并具有 ToolStrip 控件的 MDI 窗体 | Microsoft Docs"
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
  - "MenuStrip 控件 [Windows 窗体]"
  - "工具栏 [Windows 窗体]"
  - "ToolStrip 控件 [Windows 窗体]"
  - "ToolStripPanel 控件 [Windows 窗体]"
ms.assetid: 64992ed9-44af-4baf-b45f-863e6ab35711
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：创建合并了菜单并具有 ToolStrip 控件的 MDI 窗体
<xref:System.Windows.Forms?displayProperty=fullName> 命名空间支持多文档界面 \(MDI\) 应用程序，而 <xref:System.Windows.Forms.MenuStrip> 控件支持菜单合并。  MDI 窗体还可支持 <xref:System.Windows.Forms.ToolStrip> 控件。  
  
 在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中，对此功能提供广泛支持。  
  
 另请参阅[演练：创建具有菜单合并和 ToolStrip 控件的 MDI 窗体](http://msdn.microsoft.com/library/ms233676\(v=vs.110\))。  
  
## 示例  
 以下代码示例演示如何将 <xref:System.Windows.Forms.ToolStripPanel> 控件和 MDI 窗体配合使用。  此窗体还支持菜单与子菜单合并。  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.MdiForm#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.MdiForm#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.MdiForm/VB/Form1.vb#1)]  
  
## 编译代码  
 此代码示例需要：  
  
-   对 System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 [ToolStrip 控件](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)