---
title: "如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份 | Microsoft Docs"
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
  - "日历, 设置显示格式"
  - "日历, 多个月"
  - "示例 [Windows 窗体], 日历控件"
  - "MonthCalendar 控件 [Windows 窗体], 设置显示格式"
ms.assetid: d197caa2-38a5-4cb4-acc3-562130c2ace3
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份
Windows 窗体 <xref:System.Windows.Forms.MonthCalendar> 控件最多可同时显示十二个月。  默认情况下，控件只显示一个月；但您可以指定显示多少个月以及它们在控件中的排列方式。  当更改月历尺寸时，控件的大小也会随之改变；因此应确保窗体上有足够的空间供新尺寸使用。  
  
### 显示多个月份  
  
-   将 <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A> 属性设置为以水平和垂直方式显示的月份数。  
  
    ```vb  
    MonthCalendar1.CalendarDimensions = New System.Drawing.Size (3,2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.CalendarDimensions = new System.Drawing.Size (3,2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->CalendarDimensions = System::Drawing::Size (3,2);  
    ```  
  
## 请参阅  
 [MonthCalendar 控件](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [如何：更改 Windows 窗体 MonthCalendar 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)