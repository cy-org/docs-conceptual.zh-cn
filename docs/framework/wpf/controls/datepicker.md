---
title: "DatePicker | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件 [WPF], DatePicker"
  - "DatePicker 控件 [WPF]"
ms.assetid: 619765c8-8d25-4315-aec2-79aea08fed9f
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# DatePicker
<xref:System.Windows.Controls.DatePicker> 控件允许用户通过在文本字段中键入日期或使用下拉 <xref:System.Windows.Controls.Calendar> 控件来选择日期。  
  
 下图显示了 <xref:System.Windows.Controls.DatePicker>。  
  
 ![DatePicker 控件](../../../../docs/framework/wpf/controls/media/ndp-datepicker.png "NDP\_DatePicker")  
DatePicker 控件  
  
 <xref:System.Windows.Controls.DatePicker> 控件的许多属性用于管理其内置的 <xref:System.Windows.Controls.Calendar>，在功能方面与 <xref:System.Windows.Controls.Calendar> 中的等效属性完全相同。  尤其是，<xref:System.Windows.Controls.DatePicker.IsTodayHighlighted%2A?displayProperty=fullName>、<xref:System.Windows.Controls.DatePicker.FirstDayOfWeek%2A?displayProperty=fullName>、<xref:System.Windows.Controls.DatePicker.BlackoutDates%2A?displayProperty=fullName>、<xref:System.Windows.Controls.DatePicker.DisplayDateStart%2A?displayProperty=fullName>、<xref:System.Windows.Controls.DatePicker.DisplayDateEnd%2A?displayProperty=fullName>、<xref:System.Windows.Controls.DatePicker.DisplayDate%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.DatePicker.SelectedDate%2A?displayProperty=fullName> 属性在功能上与其 <xref:System.Windows.Controls.Calendar> 对等属性完全相同。  有关更多信息，请参见 <xref:System.Windows.Controls.Calendar>。  
  
 用户可以在文本字段中直接键入日期，这将设置 <xref:System.Windows.Controls.DatePicker.Text%2A> 属性。  如果 <xref:System.Windows.Controls.DatePicker> 无法将输入的字符串转换为有效日期，则将引发 <xref:System.Windows.Controls.DatePicker.DateValidationError> 事件。  默认情况下，这将导致异常，但 <xref:System.Windows.Controls.DatePicker.DateValidationError> 的事件处理程序可以将 <xref:System.Windows.Controls.DatePickerDateValidationErrorEventArgs.ThrowException%2A> 属性设置为 `false` 并防止引发异常。  
  
## 请参阅  
 [控件](../../../../docs/framework/wpf/controls/index.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)