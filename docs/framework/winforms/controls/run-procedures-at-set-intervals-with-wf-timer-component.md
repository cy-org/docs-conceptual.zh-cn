---
title: "如何：使用 Windows 窗体计时器组件以设置的间隔运行过程 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 计时器"
  - "初始化, Timer 组件"
  - "过程, 特定时间间隔"
  - "Timer 组件 [Windows 窗体], 初始化"
  - "计时器, 事件间隔"
  - "计时器, 基于 Windows 的"
ms.assetid: 8025247a-2de4-4d86-b8ab-a8cb8aeab2ea
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 如何：使用 Windows 窗体计时器组件以设置的间隔运行过程
有时可能需要创建一个在循环完成之前以特定时间间隔运行或者在设定时间间隔之后运行的过程。  <xref:System.Windows.Forms.Timer> 组件可实现此过程。  
  
 此组件专为 Windows 窗体环境设计。  如果需要适用于服务器环境的计时器，请参阅[Introduction to Server\-Based Timers](http://msdn.microsoft.com/zh-cn/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。  
  
> [!NOTE]
>  使用 <xref:System.Windows.Forms.Timer> 组件时，有一些限制。  有关详细信息，请参阅 [Windows 窗体 Timer 组件的 Interval 属性的限制](../../../../docs/framework/winforms/controls/limitations-of-the-timer-component-interval-property.md)。  
  
### 若要使用 Timer 组件以设定间隔运行过程  
  
1.  在窗体中添加 <xref:System.Windows.Forms.Timer>。  请参阅下图中的示例，了解如何以编程方式执行此操作。  [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 还支持将组件添加到窗体。  另请参阅[如何：向 Windows 窗体添加无用户界面的控件](http://msdn.microsoft.com/library/becyw7bz%20\(v=vs.110\))。  
  
2.  设置计时器的 <xref:System.Windows.Forms.Timer.Interval%2A> 属性（以毫秒计）。  此属性确定过程再次运行之前的时间间隔。  
  
    > [!NOTE]
    >  计时器事件的发生频率越高，处理器用于响应事件的时间越长。  这将会降低整体性能。  时间间隔必须设置为大于所需间隔。  
  
3.  在 <xref:System.Windows.Forms.Timer.Tick> 事件处理程序中编写相应代码。  在此事件中编写的代码将以 <xref:System.Windows.Forms.Timer.Interval%2A> 属性中指定的间隔运行。  
  
4.  将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `true` 以启动计时器。  <xref:System.Windows.Forms.Timer.Tick> 事件将开始发生，进而以设定间隔运行过程。  
  
5.  在适当时间，将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `false`以阻止过程再次运行。  将间隔设置为 `0` 不会导致计时器停止。  
  
## 示例  
 第一个代码示例以一秒的增量跟踪每天的时间。  它使用窗体上的 <xref:System.Windows.Forms.Button>、<xref:System.Windows.Forms.Label> 和 <xref:System.Windows.Forms.Timer> 组件。  将 <xref:System.Windows.Forms.Timer.Interval%2A> 属性设置为 1000（等于 1 秒）。  在 <xref:System.Windows.Forms.Timer.Tick> 事件中，将标签的标题设置为当前时间。  单击按钮时，<xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `false`，使计时器停止更新标签的标题。  下面的代码示例要求你拥有的窗体具有名为 `Button1` 的 <xref:System.Windows.Forms.Button> 控件、名为 `Timer1` 的 <xref:System.Windows.Forms.Timer> 控件和名为 `Label1` 的 <xref:System.Windows.Forms.Label> 控件。  
  
```vb  
Private Sub InitializeTimer()  
   ' Run this procedure in an appropriate event.  
   ' Set to 1 second.  
   Timer1.Interval = 1000  
   ' Enable timer.  
   Timer1.Enabled = True  
   Button1.Text = "Enabled"  
End Sub  
x  
Private Sub Timer1_Tick(ByVal Sender As Object, ByVal e As EventArgs) Handles Timer1.Tick  
' Set the caption to the current time.  
   Label1.Text = DateTime.Now  
End Sub  
  
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
      If Button1.Text = "Stop" Then  
         Button1.Text = "Start"  
         Timer1.Enabled = False  
      Else  
         Button1.Text = "Stop"  
         Timer1.Enabled = True  
      End If  
End Sub  
  
```  
  
```csharp  
private void InitializeTimer()  
{  
    // Call this procedure when the application starts.  
    // Set to 1 second.  
    Timer1.Interval = 1000;  
    Timer1.Tick += new EventHandler(Timer1_Tick);  
  
    // Enable timer.  
    Timer1.Enabled = true;  
  
    Button1.Text = "Stop";  
    Button1.Click += new EventHandler(Button1_Click);  
}  
  
private void Timer1_Tick(object Sender, EventArgs e)     
{  
   // Set the caption to the current time.  
   Label1.Text = DateTime.Now.ToString();  
}  
  
private void Button1_Click(object sender, EventArgs e)  
{  
  if ( Button1.Text == "Stop" )  
  {  
    Button1.Text = "Start";  
    Timer1.Enabled = false;  
  }  
  else  
  {  
    Button1.Text = "Stop";  
    Timer1.Enabled = true;  
  }  
}  
  
```  
  
```cpp  
private:  
   void InitializeTimer()  
   {  
      // Run this procedure in an appropriate event.  
      // Set to 1 second.  
      timer1->Interval = 1000;  
      // Enable timer.  
      timer1->Enabled = true;  
      this->timer1->Tick += gcnew System::EventHandler(this,    
                               &Form1::timer1_Tick);  
  
      button1->Text = S"Stop";  
      this->button1->Click += gcnew System::EventHandler(this,   
                               &Form1::button1_Click);  
   }  
  
   void timer1_Tick(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      // Set the caption to the current time.  
      label1->Text = DateTime::Now.ToString();  
   }  
  
   void button1_Click(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      if ( button1->Text == "Stop" )  
      {  
         button1->Text = "Start";  
         timer1->Enabled = false;  
      }  
      else  
      {  
         button1->Text = "Stop";  
         timer1->Enabled = true;  
      }  
   }  
  
```  
  
## 示例  
 第二个代码示例每隔 600 毫秒运行一个过程，直至完成一个循环。  下面的代码示例要求你拥有的窗体具有名为 `Button1` 的 <xref:System.Windows.Forms.Button> 控件、名为 `Timer1` 的 <xref:System.Windows.Forms.Timer> 控件和名为 `Label1` 的 <xref:System.Windows.Forms.Label> 控件。  
  
```vb  
' This variable will be the loop counter.  
Private counter As Integer  
  
Private Sub InitializeTimer()  
   ' Run this procedure in an appropriate event.  
   counter = 0  
   Timer1.Interval = 600  
   Timer1.Enabled = True  
End Sub  
  
Private Sub Timer1_Tick(ByVal sender As Object, ByVal e As System.EventArgs) Handles Timer1.Tick  
   If counter => 10 Then  
      ' Exit loop code.  
      Timer1.Enabled = False  
      counter = 0  
   Else  
      ' Run your procedure here.  
      ' Increment counter.  
      counter = counter + 1  
      Label1.Text = "Procedures Run: " & counter.ToString  
   End If  
End Sub  
  
```  
  
```csharp  
// This variable will be the loop counter.  
private int counter;  
  
private void InitializeTimer()  
{  
   // Run this procedure in an appropriate event.  
   counter = 0;  
   timer1.Interval = 600;  
   timer1.Enabled = true;  
   // Hook up timer's tick event handler.  
   this.timer1.Tick += new System.EventHandler(this.timer1_Tick);  
}  
  
private void timer1_Tick(object sender, System.EventArgs e)     
{  
   if (counter >= 10)   
   {  
      // Exit loop code.  
      timer1.Enabled = false;  
      counter = 0;  
   }  
   else  
   {  
      // Run your procedure here.  
      // Increment counter.  
      counter = counter + 1;  
      label1.Text = "Procedures Run: " + counter.ToString();  
      }  
}  
  
```  
  
```cpp  
private:  
   int counter;  
  
   void InitializeTimer()  
   {  
      // Run this procedure in an appropriate event.  
      counter = 0;  
      timer1->Interval = 600;  
      timer1->Enabled = true;  
      // Hook up timer's tick event handler.  
      this->timer1->Tick += gcnew System::EventHandler(this, &Form1::timer1_Tick);  
   }  
  
   void timer1_Tick(System::Object ^ sender,  
      System::EventArgs ^ e)  
   {  
      if (counter >= 10)   
      {  
         // Exit loop code.  
         timer1->Enabled = false;  
         counter = 0;  
      }  
      else  
      {  
         // Run your procedure here.  
         // Increment counter.  
         counter = counter + 1;  
         label1->Text = String::Concat("Procedures Run: ",  
            counter.ToString());  
      }  
   }  
```  
  
## 请参阅  
 <xref:System.Windows.Forms.Timer>   
 [Timer 组件](../../../../docs/framework/winforms/controls/timer-component-windows-forms.md)   
 [Timer 组件概述](../../../../docs/framework/winforms/controls/timer-component-overview-windows-forms.md)