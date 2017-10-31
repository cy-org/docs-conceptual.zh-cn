---
title: "CheckBox 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CheckBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "绑定控件, 复选框"
  - "复选框, 关于复选框"
  - "CheckBox 控件 [Windows 窗体], 关于 CheckBox 控件"
  - "数据绑定, 复选框控件"
  - "数据绑定控件, 复选框"
ms.assetid: 085a4e0b-9046-473f-b141-d0edddfb2ebb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# CheckBox 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.CheckBox> 控件指示某个特定条件是处于打开还是关闭状态。  它常用于为用户提供是\/否或真\/假选项。  可以成组使用复选框 \(CheckBox\) 控件以显示多重选项，用户可以从中选择一项或多项。  
  
 复选框 \(CheckBox\) 控件和单选按钮 \(RadioButton\) 控件的相似之处在于，它们都是用于指示用户所选的选项。  它们的不同之处在于，在单选按钮组中一次只能选择一个单选按钮。  但是对于复选框 \(CheckBox\) 控件，则可以选择任意数量的复选框。  
  
 复选框可以使用简单数据绑定连接到数据库中的元素。  多个复选框可以使用 <xref:System.Windows.Forms.GroupBox> 控件进行分组。  这对于可视外观以及用户界面设计很有用，因为成组控件可以在窗体设计器上一起移动。  有关更多信息，请参见[Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)和 [GroupBox 控件](../../../../docs/framework/winforms/controls/groupbox-control-windows-forms.md)。  
  
 <xref:System.Windows.Forms.CheckBox> 控件有两个重要属性：<xref:System.Windows.Forms.CheckBox.Checked%2A> 和 <xref:System.Windows.Forms.CheckBox.CheckState%2A>。  <xref:System.Windows.Forms.CheckBox.Checked%2A> 属性返回 `true` 或 `false`。  <xref:System.Windows.Forms.CheckBox.CheckState%2A> 属性返回 <xref:System.Windows.Forms.CheckState> 或 <xref:System.Windows.Forms.CheckState>；如果 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 属性被设置为 `true`，则 <xref:System.Windows.Forms.CheckBox.CheckState%2A> 还可能返回 <xref:System.Windows.Forms.CheckState>。  处于不确定状态时，该框会显示为灰显外观，指示该选项不可用。  
  
## 请参阅  
 <xref:System.Windows.Forms.CheckBox>   
 [如何：使用 Windows 窗体 CheckBox 控件设置选项](../../../../docs/framework/winforms/controls/how-to-set-options-with-windows-forms-checkbox-controls.md)   
 [如何：响应 Windows 窗体 CheckBox 的单击](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-checkbox-clicks.md)   
 [CheckBox 控件](../../../../docs/framework/winforms/controls/checkbox-control-windows-forms.md)