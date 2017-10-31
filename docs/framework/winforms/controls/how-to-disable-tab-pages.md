---
title: "如何：禁用选项卡页 | Microsoft Docs"
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
  - "选项卡页, 在窗体中隐藏"
  - "TabControl 控件 [Windows 窗体], 禁用页"
ms.assetid: adcc6618-8a34-4ee1-bbe3-47e732de6a59
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：禁用选项卡页
在某些时候，您将希望限制对 Windows 窗体应用程序内可用的数据的访问。  这种情况的一个例子是您将数据显示在选项卡控件的选项卡页中时；管理员可能在选项卡页上放置了您不希望来宾或低级别用户访问的信息。  
  
### 以编程方式禁用选项卡页  
  
1.  编写用来处理选项卡控件 <xref:System.Windows.Forms.TabControl.SelectedIndexChanged> 事件的代码。  这是在用户从一个选项卡切换到另一个选项卡时引发的事件。  
  
2.  检查凭据。  根据提供的信息，您可能希望在允许用户查看选项卡之前，检查用户登录所使用的用户名或某个其他形式的凭据。  
  
3.  如果用户具有适当的凭据，则显示已单击的选项卡。  如果用户没有适当的凭据，则显示一个消息框或某个其他用户界面以指示用户没有访问权限，然后返回到初始选项卡。  
  
    > [!NOTE]
    >  在生产应用程序中实现此功能时，可以在窗体的 <xref:System.Windows.Forms.Form.Load> 事件期间执行此凭据检查。  这样，您就可以在显示任何用户界面之前隐藏选项卡（这是一种更简洁的编程方法）。  下面使用的方法（在 <xref:System.Windows.Forms.TabControl.SelectedIndexChanged> 事件期间检查凭据并禁用选项卡）对这一点进行了阐述。  
  
4.  或者，如果有两个以上的选项卡页，则显示与原始选项卡页不同的选项卡页。  
  
     在下面的示例中，用 <xref:System.Windows.Forms.CheckBox> 控件代替检查凭据，因为访问选项卡的标准会因应用程序而异。  在引发 <xref:System.Windows.Forms.TabControl.SelectedIndexChanged> 事件时，如果凭据检查为真（即选中了复选框）且选定的选项卡为 `TabPage2`（本示例中为带有机密信息的选项卡），则显示 `TabPage2`。  否则，显示 `TabPage3`，并向用户显示一个消息框，指出他们没有相应的访问特权。  下面的代码假定窗体具有一个 <xref:System.Windows.Forms.CheckBox> 控件 \(`CredentialCheck`\) 和一个具有三个选项卡页的 <xref:System.Windows.Forms.TabControl> 控件。  
  
    ```vb  
    Private Sub TabControl1_SelectedIndexChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles TabControl1.SelectedIndexChanged  
       ' Check Credentials Here  
  
       If CredentialCheck.Checked = True And _   
       TabControl1.SelectedTab Is TabPage2 Then  
          TabControl1.SelectedTab = TabPage2  
       ElseIf CredentialCheck.Checked = False _   
       And TabControl1.SelectedTab Is TabPage2 Then  
          MessageBox.Show _   
         ("Unable to load tab. You have insufficient access privileges.")  
          TabControl1.SelectedTab = TabPage3  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void tabControl1_SelectedIndexChanged(object sender, System.EventArgs e)  
    {  
        // Check Credentials Here  
  
        if ((CredentialCheck.Checked == true) && (tabControl1.SelectedTab == tabPage2))   
        {  
            tabControl1.SelectedTab = tabPage2;  
        }  
        else if ((CredentialCheck.Checked == false) && (tabControl1.SelectedTab == tabPage2))  
        {  
            MessageBox.Show("Unable to load tab. You have insufficient access privileges.");  
            tabControl1.SelectedTab = tabPage3;  
        }  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void tabControl1_SelectedIndexChanged(  
          System::Object ^ sender,  
          System::EventArgs ^  e)  
       {  
          // Check Credentials Here  
          if ((CredentialCheck->Checked == true) &&  
              (tabControl1->SelectedTab == tabPage2))  
          {  
             tabControl1->SelectedTab = tabPage2;  
          }  
          else if ((CredentialCheck->Checked == false) &&  
                   (tabControl1->SelectedTab == tabPage2))  
          {  
             MessageBox::Show(String::Concat("Unable to load tab. ",  
                "You have insufficient access privileges."));  
             tabControl1->SelectedTab = tabPage3;  
          }  
       }  
    ```  
  
     （Visual C\# 和 Visual C\+\+）在窗体的构造函数中放置以下代码，以注册事件处理程序。  
  
    ```csharp  
    this.tabControl1.SelectedIndexChanged +=   
       new System.EventHandler(this.tabControl1_SelectedIndexChanged);  
  
    ```  
  
    ```cpp  
    this->tabControl1->SelectedIndexChanged +=  
       gcnew System::EventHandler(this, &Form1::tabControl1_SelectedIndexChanged);  
    ```  
  
## 请参阅  
 [TabControl 控件概述](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [如何：将控件添加到选项卡页](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [如何：使用 Windows 窗体 TabControl 添加和移除选项卡](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)   
 [如何：更改 Windows 窗体 TabControl 的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)