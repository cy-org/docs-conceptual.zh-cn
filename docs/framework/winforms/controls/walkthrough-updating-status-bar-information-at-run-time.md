---
title: "演练：在运行时更新状态栏信息 | Microsoft Docs"
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
  - "面板, 刷新状态栏"
  - "状态栏, 刷新面板"
  - "状态栏, 在运行时更新"
  - "StatusBar 控件 [Windows 窗体], 刷新面板"
ms.assetid: cc2abb06-c082-49f7-a5a3-2fd1bbcb58d1
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 演练：在运行时更新状态栏信息
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip> 和 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件取代了 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件以实现向后兼容并供将来使用。  
  
 经常会有程序要求您根据应用程序状态的更改或其他用户交互情况，在运行时动态更新状态栏面板的内容。  这是一种用于执行以下任务的常用方式：通知用户启用了 Caps Lock、Num Lock 或 Scroll Lock 之类的键，或者将日期或时钟作为方便的引用来提供。  
  
 在下面的示例中，将使用 <xref:System.Windows.Forms.StatusBarPanel> 类的一个实例来承载时钟。  
  
### 准备更新状态栏  
  
1.  创建新的 Windows 窗体。  
  
2.  将 <xref:System.Windows.Forms.StatusBar> 控件添加到您的窗体。  有关详细信息，请参见 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
3.  将状态栏面板添加到您的 <xref:System.Windows.Forms.StatusBar> 控件。  有关详细信息，请参见 [如何：向 StatusBar 控件添加面板](../../../../docs/framework/winforms/controls/how-to-add-panels-to-a-statusbar-control.md)。  
  
4.  对于添加至窗体的 <xref:System.Windows.Forms.StatusBar> 控件，将 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 属性设置为 `true`。  
  
5.  将 Windows 窗体 <xref:System.Windows.Forms.Timer> 组件添加到该窗体。  
  
    > [!NOTE]
    >  Windows 窗体 <xref:System.Windows.Forms.Timer?displayProperty=fullName> 组件是为 Windows 窗体环境设计的。  如果您需要适合服务器环境的计时器，请参见 [Introduction to Server\-Based Timers](http://msdn.microsoft.com/zh-cn/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。  
  
6.  将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `true`。  
  
7.  将 <xref:System.Windows.Forms.Timer> 的 <xref:System.Windows.Forms.Timer.Interval%2A> 属性设置为 30000。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.Timer> 组件的 <xref:System.Windows.Forms.Timer.Interval%2A> 属性应设置为 30 秒（30,000 毫秒）以确保所显示的时间反映准确的时间。  
  
### 通过实现计时器更新状态栏  
  
1.  将下面的代码插入 <xref:System.Windows.Forms.Timer> 组件的事件处理程序，以更新 <xref:System.Windows.Forms.StatusBar> 控件的面板。  
  
    ```vb  
    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick  
       StatusBar1.Panels(0).Text = Now.ToShortTimeString  
    End Sub  
  
    ```  
  
    ```csharp  
    private void timer1_Tick(object sender, System.EventArgs e)  
    {  
       statusBar1.Panels[0].Text = DateTime.Now.ToShortTimeString();  
    }  
  
    ```  
  
    ```cpp  
    private:  
      System::Void timer1_Tick(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        statusBar1->Panels[0]->Text =  
          DateTime::Now.ToShortTimeString();  
      }  
    ```  
  
     此时，您就可以运行该应用程序并观察在状态栏面板中运行的时钟。  
  
### 测试应用程序  
  
1.  调试该应用程序，然后按 F5 运行。  有关调试的详细信息，请参见 [使用 Visual Studio 进行调试](../Topic/Debugging%20in%20Visual%20Studio.md)。  
  
    > [!NOTE]
    >  大约 30 秒之后，时钟才会出现在状态栏上。  这样可以获得最精确的时间。  相反地，要使时钟早些出现，应当减小在上文步骤 7 中设置的 <xref:System.Windows.Forms.Timer.Interval%2A> 属性的值。  
  
## 请参阅  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [如何：向 StatusBar 控件添加面板](../../../../docs/framework/winforms/controls/how-to-add-panels-to-a-statusbar-control.md)   
 [如何：确定 Windows 窗体 StatusBar 控件中被单击的面板](../../../../docs/framework/winforms/controls/determine-which-panel-wf-statusbar-control-was-clicked.md)   
 [StatusBar 控件概述](../../../../docs/framework/winforms/controls/statusbar-control-overview-windows-forms.md)