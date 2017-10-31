---
title: "如何：更改 DataRepeater 控件的外观 (Visual Studio) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DataRepeater, 更改运行时外观"
  - "DataRepeater, 自定义"
ms.assetid: 2af6dfce-760b-489e-b863-8da967f315c3
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 如何：更改 DataRepeater 控件的外观 (Visual Studio)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

可通过在设计时设置属性或在运行时处理 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件来更改 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的外观。  
  
 在运行时将对每个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeaterItem> 重复您在设计时在选中控件的项模板部分的情况下设置的属性。  仅当容器没有被完全覆盖时（例如，<xref:System.Windows.Forms.Control.Padding%2A> 属性设置为较大的值时），才能在运行时看到 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件本身与外观相关的属性。  
  
 在运行时，可基于条件设置与外观相关的属性。  例如，在日程安排应用程序中，您可以更改某个项的背景颜色来警告用户该项已过期。  在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件处理程序中，如果在诸如 `If Then` 这样的条件语句中设置属性，还必须使用 `Else` 子句来指定不满足条件时的外观。  
  
### 在设计时更改外观  
  
1.  在 Windows 窗体设计器中选择 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的项模板（上半部分）区域。  
  
2.  在“属性”窗口中选择某个属性并更改它的值。  影响外观的常见属性包括 <xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.BackgroundImage%2A>、<xref:System.Windows.Forms.Panel.BorderStyle%2A> 和 <xref:System.Windows.Forms.Control.ForeColor%2A>。  
  
### 在运行时更改外观  
  
1.  在代码编辑器中，在“事件”下拉列表中单击**“DrawItem”**。  
  
2.  在 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem> 事件处理程序中添加下面的代码来设置属性：  
  
     [!code-cs[VbPowerPacksDataRepeaterAppearance#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_1.cs)]
     [!code-vb[VbPowerPacksDataRepeaterAppearance#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_1.vb)]  
  
## 示例  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件的一些常见自定义包括以交替颜色显示行以及基于条件更改字段的颜色。  下面的示例演示如何执行这些自定义项。  此示例假定您有一个 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater> 控件，该控件绑定到 Northwind 数据库的 Products 表。  
  
 [!code-vb[VbPowerPacksDataRepeaterAlternateBackColor#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/VisualBasic/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_2.vb)]
 [!code-cs[VbPowerPacksDataRepeaterAlternateBackColor#1](../../../visual-basic/developing-apps/windows-forms/codesnippet/CSharp/how-to-change-the-appearance-of-a-datarepeater-control-visual-studio_2.cs)]  
  
 请注意，对于这两个自定义，您必须提供代码来设置满足和不满足条件的属性。  如果未指定 `Else` 条件，您将在运行时看到意外的结果。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater>   
 <xref:Microsoft.VisualBasic.PowerPacks.DataRepeater.DrawItem>   
 [DataRepeater 控件简介](../../../visual-basic/developing-apps/windows-forms/introduction-to-the-datarepeater-control-visual-studio.md)   
 [DataRepeater 控件疑难解答](../../../visual-basic/developing-apps/windows-forms/troubleshooting-the-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示绑定数据](../../../visual-basic/developing-apps/windows-forms/how-to-display-bound-data-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示未绑定的控件](../../../visual-basic/developing-apps/windows-forms/how-to-display-unbound-controls-in-a-datarepeater-control-visual-studio.md)   
 [如何：在 DataRepeater 控件中显示项标题](../../../visual-basic/developing-apps/windows-forms/how-to-display-item-headers-in-a-datarepeater-control-visual-studio.md)