---
title: "如何：按功能分组 Windows 窗体 RadioButton 控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 分组"
  - "单选按钮, 分组"
  - "RadioButton 控件 [Windows 窗体], 分组"
  - "Windows 窗体控件, 分组"
ms.assetid: 58f8fe34-50b7-49d8-a2be-c271be3c6b32
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：按功能分组 Windows 窗体 RadioButton 控件
设计 Windows 窗体 <xref:System.Windows.Forms.RadioButton> 控件是为了使用户可以从两种或多种设置中进行选择（只能将其中一种设置分配给某个过程或对象）。  例如，一组 <xref:System.Windows.Forms.RadioButton> 控件可以显示一组可供选择的货物运输工具，但只能使用其中的一种工具。  因此，每次只能选择一个 <xref:System.Windows.Forms.RadioButton>，即使它是功能组的一部分也不例外。  
  
 在一个容器（如 <xref:System.Windows.Forms.Panel> 控件、<xref:System.Windows.Forms.GroupBox> 控件或窗体）内绘制单选按钮即可将它们分组。  直接添加到一个窗体中的所有单选按钮将形成一个组。  若要添加不同的组，必须将它们放到面板或分组框中。  有关面板或分组框的更多信息，请参见 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md) 或 [GroupBox 控件概述](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md)。  
  
### 将 RadioButton 控件分组使之独立于其他组工作  
  
1.  从**“工具箱”**的**“Windows 窗体”**选项卡中，将 <xref:System.Windows.Forms.GroupBox> 或 <xref:System.Windows.Forms.Panel> 控件拖到窗体上。  
  
2.  在 <xref:System.Windows.Forms.GroupBox> 或 <xref:System.Windows.Forms.Panel> 控件上绘制 <xref:System.Windows.Forms.RadioButton> 控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.RadioButton>   
 [RadioButton 控件概述](../../../../docs/framework/winforms/controls/radiobutton-control-overview-windows-forms.md)   
 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [GroupBox 控件概述](../../../../docs/framework/winforms/controls/groupbox-control-overview-windows-forms.md)   
 [CheckBox 控件概述](../../../../docs/framework/winforms/controls/checkbox-control-overview-windows-forms.md)   
 [RadioButton 控件](../../../../docs/framework/winforms/controls/radiobutton-control-windows-forms.md)