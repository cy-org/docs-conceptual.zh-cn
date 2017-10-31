---
title: "如何：更改 Windows 窗体 LinkLabel 控件的外观 | Microsoft Docs"
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
  - "LinkLabel 控件 [Windows 窗体], 更改链接的外观"
  - "LinkLabel 控件 [Windows 窗体], 示例"
  - "LinkLabel 属性"
  - "链接, 更改外观"
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：更改 Windows 窗体 LinkLabel 控件的外观
可以更改 <xref:System.Windows.Forms.LinkLabel> 控件显示的文本以适应各种用途。  例如，一种常见的做法是将文本设置为以特定颜色并加下划线显示，以指示该文本可以单击。  用户单击文本后，该颜色会变为其他颜色。  若要控制此行为，可以设置五个不同的属性，分别是 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>、<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>、<xref:System.Windows.Forms.LinkLabel.LinkColor%2A>、<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 和 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 属性。  
  
### 更改 LinkLabel 控件的外观  
  
1.  将 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A> 和 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 属性设置为所需的颜色。  
  
     此操作可以通过编程方式实现，也可以在设计时通过**“属性”**窗口实现。  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2.  将 <xref:System.Windows.Forms.LinkLabel.Text%2A> 属性设置为相应的标题。  
  
     此操作可以通过编程方式实现，也可以在设计时通过**“属性”**窗口实现。  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3.  设置 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 属性，以确定将标题的哪一部分作为链接。  
  
     <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 值是用包含两个数字的 <xref:System.Windows.Forms.LinkArea> 表示的，这两个数字分别表示起始字符位置和字符个数。  此操作可以通过编程方式实现，也可以在设计时通过**“属性”**窗口实现。  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4.  将 <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> 属性设置为 <xref:System.Windows.Forms.LinkBehavior>、<xref:System.Windows.Forms.LinkBehavior> 或 <xref:System.Windows.Forms.LinkBehavior>。  
  
     如果将它设置为 <xref:System.Windows.Forms.LinkBehavior>，则仅当指针停留在 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> 所确定的标题部分时，这一部分才会有下划线。  
  
5.  在 <xref:System.Windows.Forms.LinkLabel.LinkClicked> 事件处理程序中，将 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> 属性设置为 `true`。  
  
     访问了某个链接后，常见的做法是以某种方式更改该链接的外观，通常是更改颜色。  文本将更改为由 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> 属性指定的颜色。  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>   
 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>   
 <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>   
 <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>   
 [LinkLabel 控件概述](../../../../docs/framework/winforms/controls/linklabel-control-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 LinkLabel 控件链接到对象或网页](../../../../docs/framework/winforms/controls/link-to-an-object-or-web-page-with-wf-linklabel-control.md)   
 [LinkLabel 控件](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)