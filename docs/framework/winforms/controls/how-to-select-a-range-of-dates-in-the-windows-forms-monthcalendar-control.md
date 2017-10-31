---
title: "如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围 | Microsoft Docs"
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
  - "日历, 选择日期范围"
  - "日期, 在日历控件中选择日期范围"
  - "示例 [Windows 窗体], 日历控件"
  - "MonthCalendar 控件 [Windows 窗体], 选择日期范围"
ms.assetid: 95d9ab95-b0f8-4c19-9f63-b5cd4593a5d0
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围
Windows 窗体控件 <xref:System.Windows.Forms.MonthCalendar> 的一个重要功能是用户可以选择日期的范围。  此功能是对 <xref:System.Windows.Forms.DateTimePicker> 控件的日期选择功能的一个改进，后者只允许用户选择单个日期\/时间值。  通过使用 <xref:System.Windows.Forms.MonthCalendar> 控件的属性，您可以设置一个日期范围或者获取用户设置的选择范围。  下面的代码示例演示如何设置选择范围。  
  
### 选择日期范围  
  
1.  创建表示日期范围中第一个和最后一个日期的 <xref:System.DateTime> 对象。  
  
    ```vb  
    Dim projectStart As Date = New DateTime(2001, 2, 13)  
    Dim projectEnd As Date = New DateTime(2001, 2, 28)  
    ```  
  
    ```csharp  
    DateTime projectStart = new DateTime(2001, 2, 13);  
    DateTime projectEnd = new DateTime(2001, 2, 28);  
    ```  
  
    ```cpp  
    DateTime projectStart = DateTime(2001, 2, 13);  
    DateTime projectEnd = DateTime(2001, 2, 28);  
    ```  
  
2.  设置 <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A> 属性。  
  
    ```vb  
    MonthCalendar1.SelectionRange = New SelectionRange(projectStart, projectEnd)  
    ```  
  
    ```csharp  
    monthCalendar1.SelectionRange = new SelectionRange(projectStart, projectEnd);  
    ```  
  
    ```cpp  
    monthCalendar1->SelectionRange = gcnew  
       SelectionRange(projectStart, projectEnd);  
    ```  
  
     \- 或 \-  
  
     设置 <xref:System.Windows.Forms.MonthCalendar.SelectionStart%2A> 和 <xref:System.Windows.Forms.MonthCalendar.SelectionEnd%2A> 属性。  
  
    ```vb  
    MonthCalendar1.SelectionStart = projectStart  
    MonthCalendar1.SelectionEnd = projectEnd  
    ```  
  
    ```csharp  
    monthCalendar1.SelectionStart = projectStart;  
    monthCalendar1.SelectionEnd = projectEnd;  
    ```  
  
    ```cpp  
    monthCalendar1->SelectionStart = projectStart;  
    monthCalendar1->SelectionEnd = projectEnd;  
    ```  
  
## 请参阅  
 [MonthCalendar 控件](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [如何：更改 Windows 窗体 MonthCalendar 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)   
 [如何：使用 Windows 窗体 MonthCalendar 控件以粗体显示特定日期](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)