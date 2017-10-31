---
title: "如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期 | Microsoft Docs"
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
  - "日期, 在 DateTimePicker 控件中显示"
  - "DateTimePicker 控件 [Windows 窗体], 显示样式"
  - "示例 [Windows 窗体], DateTimePicker 控件"
ms.assetid: 39767691-2d2b-46b6-a663-b7901e581a6e
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期
Windows 窗体 <xref:System.Windows.Forms.DateTimePicker> 控件在控件中的日期和时间的显示格式设置方面为您提供了灵活性。  <xref:System.Windows.Forms.DateTimePicker.Format%2A> 属性允许从预定义格式（在 <xref:System.Windows.Forms.DateTimePickerFormat> 中列出）中选择。  如果这些预定义格式中没有一个可以满足您的要求，可以使用 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> 中列出的格式字符创建您自己的格式化样式。  
  
### 显示自定义格式  
  
1.  将 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 属性设置为 `DateTimePickerFormat.Custom`。  
  
2.  将 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> 属性设置为一个格式字符串。  
  
    ```vb  
    DateTimePicker1.Format = DateTimePickerFormat.Custom  
    ' Display the date as "Mon 27 Feb 2012".  
    DateTimePicker1.CustomFormat = "ddd dd MMM yyyy"  
  
    ```  
  
    ```csharp  
    dateTimePicker1.Format = DateTimePickerFormat.Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1.CustomFormat = "ddd dd MMM yyyy";  
  
    ```  
  
    ```cpp  
    dateTimePicker1->Format = DateTimePickerFormat::Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1->CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
### 向格式化值添加文本  
  
1.  使用单引号将任何不是格式字符（如“M”）或分隔符（如“:”）的字符括起来。  例如，下面的格式字符串采用英语（美国）区域性以“Today is: 05:30:31 Friday March 02, 2012”格式来显示当前日期。  
  
    ```vb  
    DateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy"  
  
    ```  
  
    ```csharp  
    dateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
  
    ```  
  
    ```cpp  
    dateTimePicker1->CustomFormat =  
       "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
     根据区域性设置的不同，任何未括在单引号中的字符都有可能被更改。  例如，下面的格式字符串采用英语（美国）区域性以“Today is: 05:30:31 Friday March 02, 2012”格式来显示当前日期。  注意，第一个冒号应括在单引号中，因为它不是像“hh:mm:ss”中的冒号一样作为分隔字符使用。  在另一种区域性中，格式可能为“Today is: 05.30.31 Friday March 02, 2012”。  
  
## 请参阅  
 [DateTimePicker 控件](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md)   
 [如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期](../../../../docs/framework/winforms/controls/how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)