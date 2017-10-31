---
title: "如何：在 Web 窗体应用程序中使用事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事件 [.NET Framework]，Web 窗体"
  - "Web 窗体控件，以及事件"
  - "事件处理程序 [.NET Framework]，Web 窗体"
  - "事件 [.NET Framework]，使用"
  - "Web 窗体，事件处理"
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# 如何：在 Web 窗体应用程序中使用事件
ASP.NET Web 窗体应用程序中的一种常见情况是使用控件填充网页，然后根据用户单击的控件执行特定操作。  例如，当用户在窗体中单击<xref:System.Web.UI.WebControls.Button?displayProperty=fullName>控件时，该控件会引发一个事件。  通过处理该事件，应用程序可以针对该按钮单击操作执行适当的应用程序逻辑。  
  
### 处理网页中的按钮单击事件  
  
1.  创建具有`OnClick`值的<xref:System.Web.UI.WebControls.Button>控件，该值设置为在下一步中定义的方法名称，的ASP.NET 网页 \(Web 窗体页\)。  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2.  定义与<xref:System.Web.UI.WebControls.Button.Click>事件委托签名匹配，并且具有为 `OnClick`值定义名称的事件处理程序。  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     <xref:System.Web.UI.WebControls.Button.Click> 事件将 <xref:System.EventHandler> 类用于委托类型，将 <xref:System.EventArgs> 类用于事件数据。  ASP.NET 页框架自动生成创建<xref:System.EventHandler>实例的代码，并将此委托实例添加到<xref:System.Web.UI.WebControls.Button>实例的<xref:System.Web.UI.WebControls.Button.Click>事件。  
  
3.  在步骤 2 中定义的事件处理程序方法添加代码以执行事件发生时所需的所有操作。  
  
## 请参阅  
 [事件](../../../docs/standard/events/index.md)