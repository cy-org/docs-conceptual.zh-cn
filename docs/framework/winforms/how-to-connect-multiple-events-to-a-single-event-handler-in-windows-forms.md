---
title: "如何：将多个事件连接到 Windows 窗体中的单个事件处理程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "事件处理程序 [Windows 窗体], 将事件连接到"
  - "事件 [Windows 窗体], 将多个事件连接到单个事件处理程序"
  - "菜单项, 多播事件处理方法"
  - "菜单, 多个菜单项的事件处理方法"
  - "Windows 窗体控件, 事件"
ms.assetid: 5a20749a-41b5-4acc-8eb1-9e5040b0a2c4
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：将多个事件连接到 Windows 窗体中的单个事件处理程序
在应用程序设计中，可能需要将单个事件处理程序用于多个事件或让多个事件执行同一过程。  例如，如果菜单命令与窗体上的按钮公开的功能相同，则让它们引发同一事件常常可以节省很多时间。  可按下面的方法达到此目的：在 C\# 中使用“属性”窗口的“事件”视图；或在 Visual Basic 代码编辑器中使用 `Handles`  关键字以及**“类名”**和**“方法名称”**下拉框。  
  
### 在 Visual Basic 中将多个事件连接到单个事件处理程序  
  
1.  右击窗体并选择**“查看代码”**。  
  
2.  从**“类名”**下拉框中，选择需要事件处理程序处理的某个控件。  
  
3.  从**“方法名称”**下拉框中，选择需要事件处理程序处理的某个事件。  
  
4.  代码编辑器插入适当的事件处理程序并在方法中放置插入点。  在下面的示例中，就是 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Click> 事件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
5.  在 `Handles` 子句中添加其他要处理的事件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click, Button2.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
6.  将适当的代码添加到该事件处理程序中。  
  
### 在 C\# 中将多个事件连接到单个事件处理程序  
  
1.  选择要将事件处理程序连接到的控件。  
  
2.  在“属性”窗口中，单击**“事件”**按钮 \(![事件按钮](../../../docs/framework/winforms/media/vxeventsbutton-propertieswindow.png "vxEventsButton\_PropertiesWindow")\)。  
  
3.  单击要处理的事件的名称。  
  
4.  在事件名称旁边的值区域中，单击下拉按钮显示现有事件处理程序列表，这些事件处理程序与要处理的事件的方法签名匹配。  
  
5.  从该列表中选择适当的事件处理程序。  
  
     代码将添加到该窗体中，以便将该事件绑定到现有事件处理程序。  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [事件处理程序概述](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)