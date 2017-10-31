---
title: "如何：拉伸 ToolStripTextBox 以填充 ToolStrip 的其余宽度（Windows 窗体） | Microsoft Docs"
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
  - "文本框, 在 ToolStrip 控件中拉伸 [Windows 窗体]"
  - "ToolStrip 控件 [Windows 窗体], 拉伸文本框"
ms.assetid: 0e610fbf-85fe-414c-900c-9704a5dd5cc6
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：拉伸 ToolStripTextBox 以填充 ToolStrip 的其余宽度（Windows 窗体）
将 <xref:System.Windows.Forms.ToolStrip> 控件的 <xref:System.Windows.Forms.ToolStrip.Stretch%2A> 属性设置为 `true` 时，控件会从端到端填充其容器，并和其容器一起调整大小。  在此配置中，您可能会发现拉伸控件中的项（例如 <xref:System.Windows.Forms.ToolStripTextBox>）、填充可用空间以及与控件一起调整大小是很有用的。  举例来说，如果要实现与 Microsoft® Internet Explorer 中的地址栏相似的外观和行为，此拉伸非常有用。  
  
## 示例  
 下面的代码示例提供了一个派生自 <xref:System.Windows.Forms.ToolStripTextBox> 的称为 `ToolStripSpringTextBox` 的类。  此类重写 <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A> 方法，以便在减去所有其他项的组合宽度后计算父 <xref:System.Windows.Forms.ToolStrip> 控件的可用宽度。  此代码示例还提供一个 <xref:System.Windows.Forms.Form> 类和一个 `Program` 类以演示新的行为。  
  
 [!code-csharp[ToolStripSpringTextBox#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ToolStripSpringTextBox/cs/ToolStripSpringTextBox.cs#00)]
 [!code-vb[ToolStripSpringTextBox#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ToolStripSpringTextBox/vb/ToolStripSpringTextBox.vb#00)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStrip.Stretch%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ToolStripTextBox>   
 <xref:System.Windows.Forms.ToolStripTextBox.GetPreferredSize%2A?displayProperty=fullName>   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [如何：在 StatusStrip 中以交互方式使用 Spring 属性](../../../../docs/framework/winforms/controls/how-to-use-the-spring-property-interactively-in-a-statusstrip.md)