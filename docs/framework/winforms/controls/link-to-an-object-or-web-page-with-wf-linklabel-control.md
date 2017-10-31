---
title: "如何：使用 Windows 窗体 LinkLabel 控件链接到对象或网页 | Microsoft Docs"
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
  - "示例 [Windows 窗体], LinkLabel 控件"
  - "链接, 到其他窗体"
  - "LinkLabel 控件 [Windows 窗体], 示例"
  - "LinkLabel 控件 [Windows 窗体], 链接到对象或网页"
  - "链接, 到其他窗体"
  - "网页链接控件"
  - "Windows 窗体, 链接到对象"
  - "Windows 窗体, 链接到网页"
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 Windows 窗体 LinkLabel 控件链接到对象或网页
Windows 窗体 <xref:System.Windows.Forms.LinkLabel> 控件使您可以在窗体上创建 Web 样式的链接。  单击链接后，可以更改链接的颜色来指示该链接已被访问。  有关更改颜色的更多信息，请参见 [如何：更改 Windows 窗体 LinkLabel 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)。  
  
## 链接到另一个窗体  
  
#### 使用 LinkLabel 控件链接到另一个窗体  
  
1.  将 <xref:System.Windows.Forms.LinkLabel.Text%2A> 属性设置为相应的标题。  
  
2.  设置 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性，以确定将标题的哪一部分作为链接。  指示的方式取决于该链接标签与外观相关的属性。  <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 值是用包含两个数字的 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 对象表示的，这两个数字分别表示起始字符位置和字符数目。  <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性可以在“属性”窗口中设置，也可以在代码中按类似下面的方式设置：  
  
    ```vb  
    ' In this code example, the link area has been set to begin  
    ' at the first character and extend for eight characters.  
    ' You may need to modify this based on the text entered in Step 1.  
    LinkLabel1.LinkArea = New LinkArea(0, 8)  
  
    ```  
  
    ```csharp  
    // In this code example, the link area has been set to begin  
    // at the first character and extend for eight characters.  
    // You may need to modify this based on the text entered in Step 1.  
    linkLabel1.LinkArea = new LinkArea(0,8);  
  
    ```  
  
    ```cpp  
    // In this code example, the link area has been set to begin  
    // at the first character and extend for eight characters.  
    // You may need to modify this based on the text entered in Step 1.  
    linkLabel1->LinkArea = LinkArea(0,8);  
    ```  
  
3.  在 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件处理程序中，调用 <xref:System.Windows.Forms.Form.Show%2A> 方法以打开项目中的另一个窗体，并将 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 属性设置为 `true`。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> 类的实例具有对已单击的 <xref:System.Windows.Forms.LinkLabel> 控件的引用，因此不需要强制转换`sender` 对象。  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _  
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _  
       Handles LinkLabel1.LinkClicked  
       ' Show another form.  
       Dim f2 As New Form()  
       f2.Show  
       LinkLabel1.LinkVisited = True  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)  
    {  
       // Show another form.  
       Form f2 = new Form();  
       f2.Show();  
       linkLabel1.LinkVisited = true;  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Show another form.  
          Form ^ f2 = new Form();  
          f2->Show();  
          linkLabel1->LinkVisited = true;  
       }  
    ```  
  
## 链接到网页  
 <xref:System.Windows.Forms.LinkLabel> 控件还可用于使用默认浏览器显示网页。  
  
#### 使用 LinkLabel 控件启动 Internet Explorer 并链接到 Web 页  
  
1.  将 <xref:System.Windows.Forms.LinkLabel.Text%2A> 属性设置为相应的标题。  
  
2.  设置 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性，以确定将标题的哪一部分作为链接。  
  
3.  在 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件处理程序的异常处理块中间，调用将 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 属性设置为 `true` 的第二个过程，并使用 <xref:System.Diagnostics.Process.Start%2A> 方法和一个 URL 启动默认浏览器。  若要使用 <xref:System.Diagnostics.Process.Start%2A> 方法，需要添加对 <xref:System.Diagnostics?displayProperty=fullName> 命名空间的引用。  
  
    > [!IMPORTANT]
    >  如果以下代码运行在部分信任的环境（如共享驱动器上）中，则在调用 `VisitLink` 方法时 JIT 编译器将失败。  `System.Diagnostics.Process.Start`语句生成失败的链接请求。  通过在调用 `VisitLink` 方法时捕获异常，以下代码可确保在 JIT 编译器失败时妥善处理错误。  
  
    ```vb  
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _  
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _  
       Handles LinkLabel1.LinkClicked  
       Try  
          VisitLink()  
       Catch ex As Exception  
          ' The error message  
          MessageBox.Show("Unable to open link that was clicked.")  
       End Try  
    End Sub  
  
    Sub VisitLink()  
       ' Change the color of the link text by setting LinkVisited   
       ' to True.  
       LinkLabel1.LinkVisited = True  
       ' Call the Process.Start method to open the default browser   
       ' with a URL:  
       System.Diagnostics.Process.Start("http://www.microsoft.com")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)  
    {  
       try  
       {  
          VisitLink();  
       }  
       catch (Exception ex )  
       {  
          MessageBox.Show("Unable to open link that was clicked.");  
       }  
    }  
  
    private void VisitLink()  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to true.  
       linkLabel1.LinkVisited = true;  
       //Call the Process.Start method to open the default browser   
       //with a URL:  
       System.Diagnostics.Process.Start("http://www.microsoft.com");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          try  
          {  
             VisitLink();  
          }  
          catch (Exception ^ ex)  
          {  
             MessageBox::Show("Unable to open link that was clicked.");  
          }  
       }  
    private:  
       void VisitLink()  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to true.  
          linkLabel1->LinkVisited = true;  
          // Call the Process.Start method to open the default browser   
          // with a URL:  
          System::Diagnostics::Process::Start("http://www.microsoft.com");  
       }  
    ```  
  
## 请参阅  
 <xref:System.Diagnostics.Process.Start%2A?displayProperty=fullName>   
 [LinkLabel 控件概述](../../../../docs/framework/winforms/controls/linklabel-control-overview-windows-forms.md)   
 [如何：更改 Windows 窗体 LinkLabel 控件的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)   
 [LinkLabel 控件](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)