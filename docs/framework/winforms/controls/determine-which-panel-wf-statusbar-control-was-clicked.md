---
title: "如何：确定 Windows 窗体 StatusBar 控件中被单击的面板 | Microsoft Docs"
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
  - "Panel 控件 [Windows 窗体], 确定单击"
  - "PanelClick 事件, 确定面板已被点击"
  - "面板, 确定已被点击"
  - "状态栏, 确定面板已被点击"
  - "StatusBar 控件 [Windows 窗体], 编码面板单击事件"
  - "StatusBar 控件 [Windows 窗体], 确定面板已被点击"
ms.assetid: d14c6092-04b2-4a07-8ddf-0dd11277ff5f
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：确定 Windows 窗体 StatusBar 控件中被单击的面板
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip> 和 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件取代了 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.StatusBar> 和 <xref:System.Windows.Forms.StatusBarPanel> 控件以实现向后兼容并供将来使用。  
  
 若要对 [StatusBar 控件](../../../../docs/framework/winforms/controls/statusbar-control-windows-forms.md) 控件进行编程以响应用户的单击操作，请在 <xref:System.Windows.Forms.StatusBar.PanelClick> 事件中使用 case 语句。  该事件包含一个参数（面板参数），该参数包含对单击的 <xref:System.Windows.Forms.StatusBarPanel> 的引用。  使用该引用可以确定单击的面板的索引，从而可以相应地进行编程。  
  
> [!NOTE]
>  确保 <xref:System.Windows.Forms.StatusBar> 控件的 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 属性设置为 `true`。  
  
### 确定单击了哪个面板  
  
1.  在 <xref:System.Windows.Forms.StatusBar.PanelClick> 事件处理程序中，使用 `Select Case` （在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中）或 `switch case`（[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 或 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）语句通过检查事件参数中已单击面板的索引来确定单击了哪个面板。  
  
     下面的代码示例要求在窗体上要有一个 <xref:System.Windows.Forms.StatusBar> 控件（即 `StatusBar1`）和两个 <xref:System.Windows.Forms.StatusBarPanel> 对象（即 `StatusBarPanel1`  和 `StatusBarPanel2`）。  
  
    ```vb  
    Private Sub StatusBar1_PanelClick(ByVal sender As System.Object, ByVal e As System.Windows.Forms.StatusBarPanelClickEventArgs) Handles StatusBar1.PanelClick  
       Select Case StatusBar1.Panels.IndexOf(e.StatusBarPanel)  
         Case 0  
           MessageBox.Show("You have clicked Panel One.")  
         Case 1  
           MessageBox.Show("You have clicked Panel Two.")  
       End Select  
    End Sub  
  
    ```  
  
    ```csharp  
    private void statusBar1_PanelClick(object sender,   
    System.Windows.Forms.StatusBarPanelClickEventArgs e)  
    {  
       switch (statusBar1.Panels.IndexOf(e.StatusBarPanel))  
       {  
          case 0 :  
             MessageBox.Show("You have clicked Panel One.");  
             break;  
          case 1 :  
             MessageBox.Show("You have clicked Panel Two.");  
             break;  
       }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void statusBar1_PanelClick(System::Object ^  sender,  
          System::Windows::Forms::StatusBarPanelClickEventArgs ^  e)  
       {  
          switch (statusBar1->Panels->IndexOf(e->StatusBarPanel))  
          {  
             case 0 :  
                MessageBox::Show("You have clicked Panel One.");  
                break;  
             case 1 :  
                MessageBox::Show("You have clicked Panel Two.");  
                break;  
          }  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.statusBar1.PanelClick += new   
       System.Windows.Forms.StatusBarPanelClickEventHandler   
       (this.statusBar1_PanelClick);  
  
    ```  
  
    ```cpp  
    this->statusBar1->PanelClick += gcnew  
       System::Windows::Forms::StatusBarPanelClickEventHandler  
       (this, &Form1::statusBar1_PanelClick);  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.StatusBar>   
 <xref:System.Windows.Forms.ToolStripStatusLabel>   
 [如何：设置状态栏面板的大小](../../../../docs/framework/winforms/controls/how-to-set-the-size-of-status-bar-panels.md)   
 [演练：在运行时更新状态栏信息](../../../../docs/framework/winforms/controls/walkthrough-updating-status-bar-information-at-run-time.md)   
 [StatusBar 控件概述](../../../../docs/framework/winforms/controls/statusbar-control-overview-windows-forms.md)