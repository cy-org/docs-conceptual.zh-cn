---
title: "如何：使用 Windows 窗体 MonthCalendar 控件以粗体显示特定日期 | Microsoft Docs"
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
  - "日历, 以粗体显示日期"
  - "示例 [Windows 窗体], 日历控件"
  - "GetDayBold 事件"
  - "MonthCalendar 控件 [Windows 窗体], 以粗体显示的日期"
ms.assetid: 8b20db5b-8118-4825-90e8-2c45c186ac7d
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 MonthCalendar 控件以粗体显示特定日期
Windows 窗体 <xref:System.Windows.Forms.MonthCalendar> 控件能以粗体显示特殊的日期或重复出现的日子。  这样做可以引起对特殊日期（如假日和周末）的注意。  
  
 三个属性控制此功能。  <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A> 属性包含单个日期。  <xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A> 属性包含每年以粗体显示的日期。  <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A> 属性包含每月以粗体显示的日期。  这些属性中的每一个都含有一个 <xref:System.DateTime> 对象数组。  若要从这些列表之一添加或移除日期，必须添加或移除 <xref:System.DateTime> 对象。  
  
### 使日期以粗体显示  
  
1.  创建 <xref:System.DateTime> 对象。  
  
    ```vb  
    Dim myVacation1 As Date = New DateTime(2001, 6, 10)  
    Dim myVacation2 As Date = New DateTime(2001, 6, 17)  
  
    ```  
  
    ```csharp  
    DateTime myVacation1 = new DateTime(2001, 6, 10);  
    DateTime myVacation2 = new DateTime(2001, 6, 17);  
  
    ```  
  
    ```cpp  
    DateTime myVacation1 = DateTime(2001, 6, 10);  
    DateTime myVacation2 = DateTime(2001, 6, 17);  
    ```  
  
2.  调用 <xref:System.Windows.Forms.MonthCalendar> 控件的 <xref:System.Windows.Forms.MonthCalendar.AddBoldedDate%2A>、<xref:System.Windows.Forms.MonthCalendar.AddAnnuallyBoldedDate%2A> 或 <xref:System.Windows.Forms.MonthCalendar.AddMonthlyBoldedDate%2A> 方法，将单个日期变为粗体。  
  
    ```vb  
    MonthCalendar1.AddBoldedDate(myVacation1)  
    MonthCalendar1.AddBoldedDate(myVacation2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.AddBoldedDate(myVacation1);  
    monthCalendar1.AddBoldedDate(myVacation2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->AddBoldedDate(myVacation1);  
    monthCalendar1->AddBoldedDate(myVacation2);  
    ```  
  
     \- 或 \-  
  
     创建一个 <xref:System.DateTime> 对象数组并将其分配给其中的某个属性，使一组日期集同时以粗体显示。  
  
    ```vb  
    Dim VacationDates As DateTime() = {myVacation1, myVacation2}  
    MonthCalendar1.BoldedDates = VacationDates  
  
    ```  
  
    ```csharp  
    DateTime[] VacationDates = {myVacation1, myVacation2};  
    monthCalendar1.BoldedDates = VacationDates;  
  
    ```  
  
    ```cpp  
    Array<DateTime>^ VacationDates = {myVacation1, myVacation2};  
    monthCalendar1->BoldedDates = VacationDates;  
    ```  
  
### 使日期以常规字体显示  
  
1.  调用 <xref:System.Windows.Forms.MonthCalendar.RemoveBoldedDate%2A>、<xref:System.Windows.Forms.MonthCalendar.RemoveAnnuallyBoldedDate%2A> 或 <xref:System.Windows.Forms.MonthCalendar.RemoveMonthlyBoldedDate%2A> 方法，使单个粗体日期按常规字体显示。  
  
    ```vb  
    MonthCalendar1.RemoveBoldedDate(myVacation1)  
    MonthCalendar1.RemoveBoldedDate(myVacation2)  
  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveBoldedDate(myVacation1);  
    monthCalendar1.RemoveBoldedDate(myVacation2);  
  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveBoldedDate(myVacation1);  
    monthCalendar1->RemoveBoldedDate(myVacation2);  
    ```  
  
     \- 或 \-  
  
     调用 <xref:System.Windows.Forms.MonthCalendar.RemoveAllBoldedDates%2A>、<xref:System.Windows.Forms.MonthCalendar.RemoveAllAnnuallyBoldedDates%2A> 或 <xref:System.Windows.Forms.MonthCalendar.RemoveAllMonthlyBoldedDates%2A> 方法，从三个列表之一移除所有的粗体日期。  
  
    ```vb  
    MonthCalendar1.RemoveAllBoldedDates()  
  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveAllBoldedDates();  
  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveAllBoldedDates();  
    ```  
  
2.  调用 <xref:System.Windows.Forms.MonthCalendar.UpdateBoldedDates%2A> 方法，更新字体的外观。  
  
    ```vb  
    MonthCalendar1.UpdateBoldedDates()  
  
    ```  
  
    ```csharp  
    monthCalendar1.UpdateBoldedDates();  
  
    ```  
  
    ```cpp  
    monthCalendar1->UpdateBoldedDates();  
    ```  
  
## 请参阅  
 [MonthCalendar 控件](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [如何：更改 Windows 窗体 MonthCalendar 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-monthcalendar-control-appearance.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)