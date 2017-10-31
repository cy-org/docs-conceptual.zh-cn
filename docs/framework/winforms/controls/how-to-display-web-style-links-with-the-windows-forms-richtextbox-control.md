---
title: "如何：使用 Windows 窗体 RichTextBox 控件显示 Web 样式的链接 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 文本框"
  - "RichTextBox 控件 [Windows 窗体], 链接到网页"
  - "文本框, 显示 Web 链接"
ms.assetid: 95089a37-a202-4f7a-94ee-6ee312908851
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 RichTextBox 控件显示 Web 样式的链接
Windows 窗体 <xref:System.Windows.Forms.RichTextBox> 控件可以将 Web 链接显示为彩色或下划线形式。  可以编写代码，在单击链接时打开浏览器窗口，该窗口中显示链接文本中指定的网站。  
  
### 使用 RichTextBox 控件链接到网页  
  
1.  将 <xref:System.Windows.Forms.RichTextBox.Text%2A> 属性设置为包含有效 URL（例如“http:\/\/www.microsoft.com\/china”）。  
  
2.  确保将 <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A> 属性设置为 `true`（默认值）。  
  
3.  创建 <xref:System.Diagnostics.Process> 对象的新全局实例。  
  
4.  为 <xref:System.Windows.Forms.RichTextBox.LinkClicked> 事件编写事件处理程序，将所需的文本发送到浏览器。  
  
     在下面的示例中，<xref:System.Windows.Forms.RichTextBox.LinkClicked> 事件根据由 <xref:System.Windows.Forms.RichTextBox> 控件的 <xref:System.Windows.Forms.RichTextBox.Text%2A> 属性指定的 URL 打开 Internet Explorer 的一个实例。  此示例假定窗体具有 <xref:System.Windows.Forms.RichTextBox> 控件。  
  
    > [!IMPORTANT]
    >  在调用 <xref:System.Diagnostics.Process.Start%2A?displayProperty=fullName> 方法时，如果因特权不足而在部分信任的上下文中运行代码，则将遇到 <xref:System.Security.SecurityException> 异常。  有关更多信息，请参见 [代码访问安全性基础知识](../../../../docs/framework/misc/code-access-security-basics.md)。  
  
    ```vb  
    Public p As New System.Diagnostics.Process  
    Private Sub RichTextBox1_LinkClicked _  
       (ByVal sender As Object, ByVal e As _  
       System.Windows.Forms.LinkClickedEventArgs) _  
       Handles RichTextBox1.LinkClicked  
          ' Call Process.Start method to open a browser  
          ' with link text as URL.  
          p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText)  
    End Sub  
  
    ```  
  
    ```csharp  
    public System.Diagnostics.Process p = new System.Diagnostics.Process();  
  
    private void richTextBox1_LinkClicked(object sender,   
    System.Windows.Forms.LinkClickedEventArgs e)  
    {  
       // Call Process.Start method to open a browser  
       // with link text as URL.  
       p = System.Diagnostics.Process.Start("IExplore.exe", e.LinkText);  
    }  
  
    ```  
  
    ```cpp  
    public:  
       System::Diagnostics::Process ^ p;  
  
    private:  
       void richTextBox1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkClickedEventArgs ^  e)  
       {  
          // Call Process.Start method to open a browser  
          // with link text as URL.  
          p = System::Diagnostics::Process::Start("IExplore.exe",  
             e->LinkText);  
       }  
    ```  
  
     \([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]\) 必须初始化进程`p`，可以通过在窗体的构造函数中包含以下语句做到这一点：  
  
    ```cpp  
    p = gcnew System::Diagnostics::Process();  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.richTextBox1.LinkClicked += new   
       System.Windows.Forms.LinkClickedEventHandler  
       (this.richTextBox1_LinkClicked);  
  
    ```  
  
    ```cpp  
    this->richTextBox1->LinkClicked += gcnew  
       System::Windows::Forms::LinkClickedEventHandler  
       (this, &Form1::richTextBox1_LinkClicked);  
    ```  
  
     在使用完所创建的进程后立即停止它是很重要的。  请参考上面提供的代码，用于停止进程的代码可能类似于如下内容：  
  
    ```vb  
    Public Sub StopWebProcess()  
       p.Kill()  
    End Sub  
  
    ```  
  
    ```csharp  
    public void StopWebProcess()  
    {  
       p.Kill();  
    }  
  
    ```  
  
    ```cpp  
    public: void StopWebProcess()  
    {  
       p->Kill();  
    }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>   
 <xref:System.Windows.Forms.RichTextBox.LinkClicked>   
 <xref:System.Windows.Forms.RichTextBox>   
 [RichTextBox 控件](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)