---
title: "MonthCalendar 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "MonthCalendar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "日历控件, Windows 窗体"
  - "日历, Windows 窗体控件"
  - "MonthCalendar 控件 [Windows 窗体], 设置一周的第一天"
ms.assetid: 788c5325-b721-44ec-95bf-9b680ba0f6a2
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# MonthCalendar 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.MonthCalendar> 控件为用户查看和设置日期信息提供了一个直观的图形界面。  该控件以网格形式显示日历：网格包含月份的编号日期，这些日期排列在周一到周日下的七个列中，并且突出显示选定的日期范围。  可以单击月份标题任何一侧的箭头按钮来选择不同的月份。  与类似的 <xref:System.Windows.Forms.DateTimePicker> 控件不同，您可以使用该控件选择多个日期。  有关 <xref:System.Windows.Forms.DateTimePicker> 控件的更多信息，请参见 [DateTimePicker 控件](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md)。  
  
## 配置 MonthCalendar 控件  
 <xref:System.Windows.Forms.MonthCalendar> 控件的外观具有很高的可配置性。  默认情况下，今天的日期显示为圆形，并且在网格的底部加以说明。  通过将 <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> 和 <xref:System.Windows.Forms.MonthCalendar.ShowTodayCircle%2A> 属性设置为 `false`，可以更改此功能。  还可以通过将 <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> 属性设置为 `true`，在日历中添加周编号。  通过设置 <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A> 属性，可以水平和垂直显示多个月份。  默认情况下，星期日显示为每周的第一天，不过可以使用 <xref:System.Windows.Forms.MonthCalendar.FirstDayOfWeek%2A> 属性将任何一天指定为第一天。  
  
 此外，还可以通过向 <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A>、<xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A> 和 <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A> 属性添加 <xref:System.DateTime> 对象，将某些日期设置为一次性地、每年或每月显示为粗体。  有关更多信息，请参见 [如何：使用 Windows 窗体 MonthCalendar 控件以粗体显示特定日期](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md)。  
  
 <xref:System.Windows.Forms.MonthCalendar> 控件的主要属性是 <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A>，即该控件中选定的日期范围。  <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A> 值不能超过 <xref:System.Windows.Forms.MonthCalendar.MaxSelectionCount%2A> 属性中设置的最大可选择天数。  用户可以选择的最早和最晚日期由 <xref:System.Windows.Forms.MonthCalendar.MaxDate%2A> 和 <xref:System.Windows.Forms.MonthCalendar.MinDate%2A> 属性确定。  
  
## 请参阅  
 <xref:System.Windows.Forms.MonthCalendar>   
 [MonthCalendar 控件](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)