---
title: "如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期 | Microsoft Docs"
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
  - "日期, 在 DateTimePicker 中设置"
  - "DateTimePicker 控件 [Windows 窗体], 设置和返回日期"
  - "示例 [Windows 窗体], DateTimePicker 控件"
ms.assetid: a8a48d68-e4b5-426e-9764-51230fc9acd2
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期
Windows 窗体 <xref:System.Windows.Forms.DateTimePicker> 控件中的当前所选日期或时间由 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性确定。  可在显示控件前（例如，在设计时或在窗体的 <xref:System.Windows.Forms.Form.Load> 事件中）设置 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性来确定控件中最初将选定的日期。  默认情况下，该控件的 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 设置为当前日期。  如果更改代码中控件的 <xref:System.Windows.Forms.DateTimePicker.Value%2A>，该控件将自动在窗体上更新以反映新设置。  
  
 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性返回 <xref:System.DateTime> 结构作为其值。  存在几个 <xref:System.DateTime> 结构的属性，这些属性返回有关所显示日期的特定信息。  这些属性仅可用于返回值；不要使用它们来设置值。  
  
-   对于日期值，<xref:System.DateTime.Month%2A>、<xref:System.DateTime.Day%2A> 和 <xref:System.DateTime.Year%2A> 属性为这些所选日期的时间单位返回整数值。  <xref:System.DateTime.DayOfWeek%2A> 属性返回的值指示所选的日期是星期几（<xref:System.DayOfWeek> 枚举中列出了可能的值）。  
  
-   对于时间值，<xref:System.DateTime.Hour%2A>、<xref:System.DateTime.Minute%2A>、<xref:System.DateTime.Second%2A> 和 <xref:System.DateTime.Millisecond%2A> 属性为这些时间单位返回整数值。  若要配置控件以显示时间，请参阅[如何：使用 DateTimePicker 控件显示时间](../../../../docs/framework/winforms/controls/how-to-display-time-with-the-datetimepicker-control.md)。  
  
### 设置控件的日期和时间值  
  
-   将 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性设置为日期或时间值。  
  
    ```vb  
    DateTimePicker1.Value = New DateTime(2001, 10, 20)  
  
    ```  
  
    ```csharp  
    dateTimePicker1.Value = new DateTime(2001, 10, 20);  
  
    ```  
  
    ```cpp  
    dateTimePicker1->Value = DateTime(2001, 10, 20);  
    ```  
  
### 返回日期和时间值  
  
-   调用 <xref:System.Windows.Forms.DateTimePicker.Text%2A> 属性以按照控件中设置的格式返回完整值，或调用 <xref:System.Windows.Forms.DateTimePicker.Value%2A> 属性的合适方法以返回值的一部分。  使用 <xref:System.Windows.Forms.DateTimePicker.ToString%2A> 将信息转换为可向用户显示的字符串。  
  
    ```vb  
    MessageBox.Show("The selected value is ", DateTimePicker1.Text)  
    MessageBox.Show("The day of the week is ",   
       DateTimePicker1.Value.DayOfWeek.ToString)  
    MessageBox.Show("Millisecond is: ",   
       DateTimePicker1.Value.Millisecond.ToString)  
  
    ```  
  
    ```csharp  
    MessageBox.Show ("The selected value is " +   
       dateTimePicker1.Text);  
    MessageBox.Show ("The day of the week is " +   
       dateTimePicker1.Value.DayOfWeek.ToString());  
    MessageBox.Show("Millisecond is: " +   
       dateTimePicker1.Value.Millisecond.ToString());  
  
    ```  
  
    ```cpp  
    MessageBox::Show (String::Concat("The selected value is ",  
       dateTimePicker1->Text));  
    MessageBox::Show (String::Concat("The day of the week is ",  
       dateTimePicker1->Value.DayOfWeek.ToString()));  
    MessageBox::Show(String::Concat("Millisecond is: ",  
       dateTimePicker1->Value.Millisecond.ToString()));  
    ```  
  
## 请参阅  
 [DateTimePicker 控件](../../../../docs/framework/winforms/controls/datetimepicker-control-windows-forms.md)   
 [如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期](../../../../docs/framework/winforms/controls/display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)