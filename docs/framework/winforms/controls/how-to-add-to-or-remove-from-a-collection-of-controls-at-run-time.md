---
title: "如何：在运行时在控件集合中进行添加或移除 | Microsoft Docs"
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
  - "集合, 添加项"
  - "控件 [Windows 窗体], 使用集合添加"
  - "控件 [Windows 窗体], 使用集合移除"
  - "控件集合"
  - "运行时, 添加控件"
  - "运行时, 移除控件"
ms.assetid: 771bf895-3d5f-469b-a324-3528f343657e
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在运行时在控件集合中进行添加或移除
应用程序开发中的常规任务在窗体上的任何容器控件上添加控件或移除控件（如 <xref:System.Windows.Forms.Panel> 或 <xref:System.Windows.Forms.GroupBox> 控件，甚至窗体自身）。  在设计时，可以直接将控件拖到面板或分组框上。  在运行时，这些控件维护一个 `Controls` 集合，该集合记录在其中放置了哪些控件。  
  
> [!NOTE]
>  下面的代码示例适用于在其中维护一个控件集合的任何控件。  
  
### 以编程方式向集合添加控件  
  
1.  创建要添加的控件实例。  
  
2.  设置新控件的属性。  
  
3.  将控件添加到父控件的 `Controls` 集合。  
  
     下面的代码示例演示如何创建 <xref:System.Windows.Forms.Button> 控件的实例。  该示例需要一个具有 <xref:System.Windows.Forms.Panel> 控件的窗体，并且要创建的按钮的事件处理方法 `NewPanelButton_Click` 已存在。  
  
    ```vb  
    Public NewPanelButton As New Button()  
  
    Public Sub AddNewControl()  
       ' The Add method will accept as a parameter any object that derives  
       ' from the Control class. In this case, it is a Button control.  
       Panel1.Controls.Add(NewPanelButton)  
       ' The event handler indicated for the Click event in the code   
       ' below is used as an example. Substite the appropriate event  
       ' handler for your application.  
       AddHandler NewPanelButton.Click, AddressOf NewPanelButton_Click  
    End Sub  
  
    ```  
  
    ```csharp  
    public Button newPanelButton = new Button();  
  
    public void addNewControl()  
    {   
       // The Add method will accept as a parameter any object that derives  
       // from the Control class. In this case, it is a Button control.  
       panel1.Controls.Add(newPanelButton);  
       // The event handler indicated for the Click event in the code   
       // below is used as an example. Substite the appropriate event  
       // handler for your application.  
       this.newPanelButton.Click += new System.EventHandler(this. NewPanelButton_Click);  
    }  
    ```  
  
### 以编程方式从集合移除控件  
  
1.  从事件中移除事件处理程序。  在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中使用 [RemoveHandler 语句](../../../../ocs/visual-basic/language-reference/statements/removehandler-statement.md) 关键字；在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中则使用 [\-\= 运算符](../Topic/-=%20Operator%20\(C%23%20Reference\)2.md)。  
  
2.  使用 `Remove` 方法，从该面板的 `Controls` 集合中删除所需的控件。  
  
3.  调用 <xref:System.Windows.Forms.Control.Dispose%2A> 方法，释放该控件使用的所有资源。  
  
    ```vb  
    Public Sub RemoveControl()  
    ' NOTE: The code below uses the instance of   
    ' the button (NewPanelButton) from the previous example.  
       If Panel1.Controls.Contains(NewPanelButton) Then  
          RemoveHandler NewPanelButton.Click, AddressOf _   
             NewPanelButton_Click  
          Panel1.Controls.Remove(NewPanelButton)  
          NewPanelButton.Dispose()  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void removeControl(object sender, System.EventArgs e)  
    {  
    // NOTE: The code below uses the instance of   
    // the button (newPanelButton) from the previous example.  
       if(panel1.Controls.Contains(newPanelButton))  
       {  
          this.newPanelButton.Click -= new System.EventHandler(this.   
             NewPanelButton_Click);  
          panel1.Controls.Remove(newPanelButton);  
          newPanelButton.Dispose();  
       }  
    }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.Panel>   
 [Panel 控件](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)