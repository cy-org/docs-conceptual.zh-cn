---
title: "如何：触发工具栏按钮的菜单事件 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具栏"
  - "ToolBar 控件 [Windows 窗体], Click 事件处理程序"
  - "ToolBar 控件 [Windows 窗体], 编码按钮单击事件"
  - "工具栏 [Windows 窗体], Click 事件处理程序"
ms.assetid: 98374f70-993d-4ca4-89fb-48fea6ce5b45
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：触发工具栏按钮的菜单事件
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 如果 Windows 窗体有带工具栏按钮的 <xref:System.Windows.Forms.ToolBar>，则需要知道用户单击了哪个按钮。  
  
 对于 <xref:System.Windows.Forms.ToolBar> 控件的 <xref:System.Windows.Forms.ToolBar.ButtonClick> 事件，可以计算 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 类的 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> 属性。  下面的示例中显示一个消息框，该框指示单击了哪个按钮。  有关详细信息，请参见 [MessageBox 类](frlrfSystemWindowsFormsMessageBoxClassTopic)。  
  
 下面的示例假定已向 Windows 窗体添加了一个 <xref:System.Windows.Forms.ToolBar> 控件。  
  
### 处理工具栏上的 Click 事件  
  
1.  在过程中，向 <xref:System.Windows.Forms.ToolBar> 控件添加工具栏按钮。  
  
    ```vb  
    Public Sub ToolBarConfig()  
    ' Instantiate the toolbar buttons, set their Text properties  
    ' and add them to the ToolBar control.  
       ToolBar1.Buttons.Add(New ToolBarButton("One"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Two"))  
       ToolBar1.Buttons.Add(New ToolBarButton("Three"))  
    ' Add the event handler delegate.  
       AddHandler ToolBar1.ButtonClick, AddressOf Me.ToolBar1_ButtonClick  
    End Sub  
  
    ```  
  
    ```csharp  
    public void ToolBarConfig()   
    {  
       toolBar1.Buttons.Add(new ToolBarButton("One"));  
       toolBar1.Buttons.Add(new ToolBarButton("Two"));  
       toolBar1.Buttons.Add(new ToolBarButton("Three"));  
  
       toolBar1.ButtonClick +=   
          new ToolBarButtonClickEventHandler(this.toolBar1_ButtonClick);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void ToolBarConfig()  
       {  
          toolBar1->Buttons->Add(gcnew ToolBarButton("One"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Two"));  
          toolBar1->Buttons->Add(gcnew ToolBarButton("Three"));  
  
          toolBar1->ButtonClick +=   
             gcnew ToolBarButtonClickEventHandler(this,  
             &Form1::toolBar1_ButtonClick);  
       }  
    ```  
  
2.  为 <xref:System.Windows.Forms.ToolBar> 控件的 <xref:System.Windows.Forms.ToolBar.ButtonClick> 事件添加事件处理程序。  使用 Case 开关语句和 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 类来确定单击的工具栏按钮。  并据此显示相应的消息框。  
  
    > [!NOTE]
    >  在这个示例中，消息框只用作占位符。  可随意添加在单击工具栏按钮时执行的其他代码。  
  
    ```vb  
    Protected Sub ToolBar1_ButtonClick(ByVal sender As Object, _  
    ByVal e As ToolBarButtonClickEventArgs)  
    ' Evaluate the Button property of the ToolBarButtonClickEventArgs  
    ' to determine which button was clicked.  
       Select Case ToolBar1.Buttons.IndexOf(e.Button)  
         Case 0  
           MessageBox.Show("First toolbar button clicked")  
         Case 1  
           MessageBox.Show("Second toolbar button clicked")  
         Case 2  
           MessageBox.Show("Third toolbar button clicked")  
       End Select  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void toolBar1_ButtonClick(object sender,  
    ToolBarButtonClickEventArgs e)  
    {  
       // Evaluate the Button property of the ToolBarButtonClickEventArgs  
       // to determine which button was clicked.  
       switch (toolBar1.Buttons.IndexOf(e.Button))  
       {  
          case 0 :  
             MessageBox.Show("First toolbar button clicked");  
             break;  
          case 1 :  
             MessageBox.Show("Second toolbar button clicked");  
             break;  
          case 2 :  
             MessageBox.Show("Third toolbar button clicked");  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    protected:  
       void toolBar1_ButtonClick(System::Object ^ sender,  
          ToolBarButtonClickEventArgs ^ e)  
       {  
         // Evaluate the Button property of the ToolBarButtonClickEventArgs  
         // to determine which button was clicked.  
          switch (toolBar1->Buttons->IndexOf(e->Button))  
          {  
             case 0 :  
                MessageBox::Show("First toolbar button clicked");  
                break;  
             case 1 :  
                MessageBox::Show("Second toolbar button clicked");  
                break;  
             case 2 :  
                MessageBox::Show("Third toolbar button clicked");  
                break;  
          }  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolBar>   
 [如何：向 ToolBar 控件添加按钮](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)   
 [如何：定义工具栏按钮的图标](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [ToolBar 控件](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)