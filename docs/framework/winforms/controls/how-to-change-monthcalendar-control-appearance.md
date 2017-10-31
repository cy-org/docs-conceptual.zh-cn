---
title: "如何：更改 Windows 窗体 MonthCalendar 控件的外观 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 日历控件"
  - "MonthBackColor 属性"
  - "MonthCalendar 控件 [Windows 窗体], 设置显示格式"
  - "TitleBackColor 属性"
  - "TitleForeColor 属性"
  - "TrailingForeColor 属性"
ms.assetid: d09b95c9-e108-4608-9b31-b9100c0677bf
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：更改 Windows 窗体 MonthCalendar 控件的外观
Windows 窗体 <xref:System.Windows.Forms.MonthCalendar> 控件允许用多种方法自定义月历的外观。  例如，可以设置配色方案并选择显示或隐藏周数和当前日期。  
  
### 更改月历的配色方案  
  
-   设置 <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>、<xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> 和 <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> 等属性。  <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A> 属性也确定星期数的字体颜色。  <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> 属性确定所显示的月份之前和之后的日期颜色。  
  
    ```vb  
    MonthCalendar1.TitleBackColor = System.Drawing.Color.Blue  
    MonthCalendar1.TrailingForeColor = System.Drawing.Color.Red  
    MonthCalendar1.TitleForeColor = System.Drawing.Color.Yellow  
    ```  
  
    ```csharp  
    monthCalendar1.TitleBackColor = System.Drawing.Color.Blue;  
    monthCalendar1.TrailingForeColor = System.Drawing.Color.Red;  
    monthCalendar1.TitleForeColor = System.Drawing.Color.Yellow;  
    ```  
  
    ```cpp  
    monthCalendar1->TitleBackColor = System::Drawing::Color::Blue;  
    monthCalendar1->TrailingForeColor = System::Drawing::Color::Red;  
    monthCalendar1->TitleForeColor = System::Drawing::Color::Yellow;  
    ```  
  
    > [!NOTE]
    >  从 Windows Vista 开始并且根据主题，设置某些属性可能不会更改日历的外观。  例如，如果 Windows 设置为使用 Aero 主题，则设置 <xref:System.Windows.Forms.MonthCalendar.BackColor%2A>、<xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>、<xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> 或 <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> 属性没有效果。  这是因为已更新的日历版本所呈现的外观在运行时派生自当前操作系统主题。  如果希望使用这些属性并启用早期版本的日历，则可以禁用应用程序的视觉样式。  禁用视觉样式可能会影响应用程序中其他控件的外观和行为。  要在 Visual Basic 中禁用视觉样式，请打开项目设计器并取消选中**“启用 XP 视觉样式”**复选框。  要在 C\# 中禁用视觉样式，请打开 Program.cs 并注释掉 `Application.EnableVisualStyles();`。  有关视觉样式的更多信息，请参见[How to: Enable Windows XP Visual Styles](http://msdn.microsoft.com/zh-cn/0a038ade-31cf-4e56-9cfe-7a1e6b83b57f)。  
  
### 在控件底部显示当前日期  
  
-   将 <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> 属性设置为 `true`。  当双击窗体时，下例在显示和省略今天的日期之间切换。  
  
    ```vb  
    Private Sub Form1_DoubleClick(ByVal sender As Object, _  
    ByVal e As System.EventArgs) Handles MyBase.DoubleClick  
       ' Toggle between True and False.  
       MonthCalendar1.ShowToday = Not MonthCalendar1.ShowToday  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_DoubleClick(object sender, System.EventArgs e)  
    {  
       // Toggle between True and False.  
       monthCalendar1.ShowToday = !monthCalendar1.ShowToday;  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void Form1_DoubleClick(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // Toggle between True and False.  
          monthCalendar1->ShowToday = !monthCalendar1->ShowToday;  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.DoubleClick += new System.EventHandler(this.Form1_DoubleClick);  
    ```  
  
    ```cpp  
    this->DoubleClick += gcnew System::EventHandler(this,  
       &Form1::Form1_DoubleClick);  
    ```  
  
### 显示周数  
  
-   将 <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> 属性设置为 `true`。  可以用代码或在“属性”窗口中设置此属性。  
  
     周数以单独的列出现在一周的第一天的左边。  
  
    ```vb  
    MonthCalendar1.ShowWeekNumbers = True  
    ```  
  
    ```csharp  
    monthCalendar1.ShowWeekNumbers = true;  
    ```  
  
    ```cpp  
    monthCalendar1->ShowWeekNumbers = true;  
    ```  
  
## 请参阅  
 [MonthCalendar 控件](../../../../docs/framework/winforms/controls/monthcalendar-control-windows-forms.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围](../../../../docs/framework/winforms/controls/how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)   
 [如何：使用 Windows 窗体 MonthCalendar 控件以粗体显示特定日期](../../../../docs/framework/winforms/controls/display-specific-days-in-bold-with-wf-monthcalendar-control.md)   
 [如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份](../../../../docs/framework/winforms/controls/display-more-than-one-month-wf-monthcalendar-control.md)