---
title: "DateTimePicker 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "DateTimePicker"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "日期和时间选择器控件"
  - "DateTimePicker 控件 [Windows 窗体], 关于"
ms.assetid: 501af106-e9fc-4efc-b9b3-c9d8dcaf8c5c
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# DateTimePicker 控件概述（Windows 窗体）
使用 Windows 窗体 <xref:System.Windows.Forms.DateTimePicker> 控件，用户可以从日期或时间列表中选择单个项。  在用来表示日期时，它显示为两部分：一个下拉列表（带有以文本形式表示的日期）和一个网格（在单击列表旁边的向下箭头时显示）。  该网格看起来很像可用于选择多个日期的 <xref:System.Windows.Forms.MonthCalendar> 控件。  有关 <xref:System.Windows.Forms.MonthCalendar> 控件的更多信息，请参见 [MonthCalendar 控件概述](../../../../docs/framework/winforms/controls/monthcalendar-control-overview-windows-forms.md)。  
  
## 主要属性  
 如果您希望 <xref:System.Windows.Forms.DateTimePicker> 作为选取或编辑时间（而不是日期）的控件出现，请将 <xref:System.Windows.Forms.DateTimePicker.ShowUpDown%2A> 属性设置为 `true`，并将 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 属性设置为 <xref:System.Windows.Forms.DateTimePickerFormat>。  有关更多信息，请参见[如何：使用 DateTimePicker 控件显示时间](../../../../docs/framework/winforms/controls/how-to-display-time-with-the-datetimepicker-control.md)。  
  
 当 <xref:System.Windows.Forms.DateTimePicker.ShowCheckBox%2A> 属性设置为 `true` 时，该控件中的选定日期旁边将显示一个复选框。  当选中该复选框时，选定的日期时间值可以更新。  当复选框为空时，值显示为不可用。  
  
 该控件的 <xref:System.Windows.Forms.DateTimePicker.MaxDate%2A> 和 <xref:System.Windows.Forms.DateTimePicker.MinDate%2A> 属性确定日期和时间的范围。  <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性包含该控件设置为的当前日期和时间。  有关详细信息，请参见[如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)。  值可以按以下四种格式显示（这些格式通过 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 属性设置）：<xref:System.Windows.Forms.DateTimePickerFormat>、<xref:System.Windows.Forms.DateTimePickerFormat>、<xref:System.Windows.Forms.DateTimePickerFormat> 或 <xref:System.Windows.Forms.DateTimePickerFormat>。  如果选择自定义格式，则必须将 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> 属性设置为适当的字符串。  有关详细信息，请参见[如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)。  
  
## 请参阅  
 [如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)   
 [如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)