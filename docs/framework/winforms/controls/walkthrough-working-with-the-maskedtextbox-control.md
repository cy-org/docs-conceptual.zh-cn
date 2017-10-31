---
title: "演练：使用 MaskedTextBox 控件 | Microsoft Docs"
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
  - "input, 控制以确保有效性"
  - "MaskedTextBox 控件 [Windows 窗体], 验证"
  - "MaskedTextBox 控件 [Windows 窗体], 演练"
  - "文本, 控制输入"
  - "用户输入, 控制"
ms.assetid: df60565e-5447-4110-92a6-be1f6ff5faa3
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 演练：使用 MaskedTextBox 控件
本演练涉及以下任务：  
  
-   初始化 <xref:System.Windows.Forms.MaskedTextBox> 控件  
  
-   当字符不符合掩码时使用 <xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected> 事件处理程序向用户报警  
  
-   为 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 属性分配类型，并在用户尝试提交的值对类型无效时，使用 <xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted> 事件处理程序向用户报警  
  
## 创建项目和添加控件  
  
#### 向窗体添加 MaskedTextBox 控件  
  
1.  打开希望在其中放置 <xref:System.Windows.Forms.MaskedTextBox> 控件的窗体。  
  
2.  将 <xref:System.Windows.Forms.MaskedTextBox> 控件从**“工具箱”**中拖到窗体上。  
  
3.  右击控件并选择**“属性”**。  在**“属性”**窗口中，选择**“掩码”**属性，并单击属性名称旁边的**“...”**（省略号）按钮。  
  
4.  在**“输入掩码”**对话框中，选择**“短日期”**掩码，并单击**“确定”**。  
  
5.  在**“属性”**窗口中，将 <xref:System.Windows.Forms.MaskedTextBox.BeepOnError%2A> 属性设置为 `true`。  设置此属性后，每次用户尝试输入不符合掩码定义的字符时，就会听到短的提示音。  
  
 有关 Mask 属性支持的字符的摘要，请参见 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 属性的“备注”节。  
  
## 发生输入错误时向用户报警  
  
#### 为被拒绝的掩码输入添加气球状提示  
  
1.  返回到**“工具箱”**，向窗体添加 <xref:System.Windows.Forms.ToolTip>。  
  
2.  为在发生输入错误时会引发 <xref:System.Windows.Forms.ToolTip> 的 <xref:System.Windows.Forms.MaskedTextBox.MaskInputRejected> 事件创建事件处理程序。  气球状提示将持续五秒保持可见状态，或在用户单击它后消失。  
  
    ```csharp  
    public void Form1_Load(Object sender, EventArgs e)   
    {  
        ... // Other initialization code  
        maskedTextBox1.Mask = "00/00/0000";  
        maskedTextBox1.MaskInputRejected += new MaskInputRejectedEventHandler(maskedTextBox1_MaskInputRejected)  
    }  
  
    void maskedTextBox1_MaskInputRejected(object sender, MaskInputRejectedEventArgs e)  
    {  
        toolTip1.ToolTipTitle = "Invalid Input";  
        toolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", maskedTextBox1, maskedTextBox1.Location, 5000);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load  
        Me.ToolTip1.IsBalloon = True  
        Me.MaskedTextBox1.Mask = "00/00/0000"  
    End Sub  
  
    Private Sub MaskedTextBox1_MaskInputRejected(sender as Object, e as MaskInputRejectedEventArgs) Handles MaskedTextBox1.MaskInputRejected  
        ToolTip1.ToolTipTitle = "Invalid Input"  
        ToolTip1.Show("We're sorry, but only digits (0-9) are allowed in dates.", MaskedTextBox1, 5000)  
    End Sub  
  
    ```  
  
## 键入无效类型时向用户报警  
  
#### 为无效的数据类型添加气球状提示  
  
1.  在窗体的 <xref:System.Windows.Forms.Form.Load> 事件处理程序中，将表示 <xref:System.DateTime> 类型的 <xref:System.Type> 对象分配给 <xref:System.Windows.Forms.MaskedTextBox> 控件的 <xref:System.Windows.Forms.MaskedTextBox.ValidatingType%2A> 属性：  
  
    ```csharp  
    private void Form1_Load(Object sender, EventArgs e)  
    {  
        // Other code  
        maskedTextBox1.ValidatingType = typeof(System.DateTime);  
        maskedTextBox1.TypeValidationCompleted += new TypeValidationEventHandler(maskedTextBox1_TypeValidationCompleted);  
    }  
    ```  
  
    ```vb  
    Private Sub Form1_Load(sender as Object, e as EventArgs)  
        // Other code  
        MaskedTextBox1.ValidatingType = GetType(System.DateTime)  
    End Sub  
    ```  
  
2.  为 <xref:System.Windows.Forms.MaskedTextBox.TypeValidationCompleted> 事件添加事件处理程序：  
  
    ```csharp  
    public void maskedTextBox1_TypeValidationCompleted(object sender, TypeValidationEventArgs e)  
    {  
        if (!e.IsValidInput)  
        {  
           toolTip1.ToolTipTitle = "Invalid Date Value";  
           toolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000);  
           e.Cancel = true;  
        }  
    }  
    ```  
  
    ```vb  
    Public Sub MaskedTextBox1_TypeValidationCompleted(sender as Object, e as TypeValidationEventArgs)  
        If Not e.IsValidInput Then  
           ToolTip1.ToolTipTitle = "Invalid Date Value"  
           ToolTip1.Show("We're sorry, but the value you entered is not a valid date. Please change the value.", maskedTextBox1, 5000)  
           e.Cancel = True  
        End If  
    End Sub  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.MaskedTextBox>   
 [MaskedTextBox 控件](../../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md)