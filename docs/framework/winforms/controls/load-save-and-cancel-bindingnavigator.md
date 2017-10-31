---
title: "如何：向 Windows 窗体 BindingNavigator 控件添加“加载”、“保存”和“取消”按钮 | Microsoft Docs"
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
  - "控件 [Windows 窗体]，操作"
  - "BindingNavigator 控件 [Windows 窗体]，添加按钮"
ms.assetid: faa33042-186e-4bb2-8798-17ceb987ec62
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：向 Windows 窗体 BindingNavigator 控件添加“加载”、“保存”和“取消”按钮
<xref:System.Windows.Forms.BindingNavigator> 控件是一个具有特殊用途的 <xref:System.Windows.Forms.ToolStrip> 控件，用于定位和操作窗体上绑定到数据的控件。  
  
 由于 <xref:System.Windows.Forms.BindingNavigator> 组件是一个 <xref:System.Windows.Forms.ToolStrip> 控件，因此可以轻松对其进行修改，加入供用户使用的附加或替代命令。  
  
 在下面的过程中，我们将 <xref:System.Windows.Forms.TextBox> 控件绑定到数据，并对 <xref:System.Windows.Forms.ToolStrip> 控件进行修改，在其中包括“加载”、“保存”和“取消”按钮。  
  
### 向 BindingNavigator 组件添加“加载”、“保存”和“取消”按钮  
  
1.  向窗体中添加一个 <xref:System.Windows.Forms.TextBox> 控件。  
  
2.  将其绑定到一个 <xref:System.Windows.Forms.BindingSource>，后者绑定到了一个数据源。  在此例中，<xref:System.Windows.Forms.BindingSource> 绑定到数据库。  
  
3.  生成数据集和表适配器后，向窗体中拖一个 <xref:System.Windows.Forms.BindingNavigator> 控件。  
  
4.  将 <xref:System.Windows.Forms.BindingNavigator> 控件的 <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> 属性设置为窗体上绑定到控件的 <xref:System.Windows.Forms.BindingSource>。  
  
5.  选择 <xref:System.Windows.Forms.BindingNavigator> 控件。  
  
6.  单击智能标记符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，**“BindingNavigator 任务”**对话框将出现，选择**“编辑项”**。  
  
     **“项集合编辑器”**出现。  
  
7.  在**“项集合编辑器”**中，完成下述操作：  
  
    1.  通过选择相应类型的 <xref:System.Windows.Forms.ToolStripItem> 并单击**“添加”**按钮来添加一个 <xref:System.Windows.Forms.ToolStripSeparator> 和三个 <xref:System.Windows.Forms.ToolStripButton> 项。  
  
    2.  将这些按钮的 <xref:System.Windows.Forms.ToolStripItem.Name%2A> 属性分别设置为“LoadButton”、“SaveButton”和“CancelButton”。  
  
    3.  将这些按钮的 <xref:System.Windows.Forms.ToolStripItem.Text%2A> 属性分别设置为“Load”、“Save”和“Cancel”。  
  
    4.  将每个按钮的 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 属性设置为“Text”。 ``  也可将此属性设置为“Image”或“ImageAndText”，并设置要显示在 <xref:System.Windows.Forms.ToolStripItem.Image%2A> 属性中的图像。 ``  ``  ``  ``  
  
    5.  单击**“确定”**关闭对话框。这些按钮将添加到 <xref:System.Windows.Forms.ToolStrip> 上。  
  
8.  右击窗体并选择**“查看代码”**。  
  
9. 在“代码编辑器”中，找到将数据加载到表适配器的代码行。  此代码是在第 2 步中设置数据绑定时生成的。  代码应类似于如下所示：`TableAdapterName.Fill(DataSetName.TableName)`。  此代码最有可能位于窗体的 <xref:System.Windows.Forms.Form.Load> 事件中。  
  
10. 为前面创建的**“加载”**<xref:System.Windows.Forms.ToolStripButton> `` 的 `` <xref:System.Windows.Forms.ToolStripItem.Click> 事件创建事件处理程序，并将此数据加载代码移入其中。  
  
     代码看起来应类似于以下形式：  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub LoadButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles LoadButton.Click  
        TableAdapterName.Fill(DataSetName.TableName)  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void LoadButton_Click(System.Object sender,   
        System.EventArgs e)  
    {  
        TableAdapterName.Fill(DataSetName.TableName);  
    }  
    ```  
  
11. 为前面创建的**“保存”**<xref:System.Windows.Forms.ToolStripButton> `` 的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件创建事件处理程序，并编写代码以更新该控件所绑定到的表中的数据。  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub SaveButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SaveButton.Click  
        TableAdapterName.Update(DataSetName.TableName)  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void SaveButton_Click(System.Object sender,   
        System.EventArgs e)  
    {  
        TableAdapterName.Update(DataSetName.TableName);  
    }  
    ```  
  
    > [!NOTE]
    >  在某些情况下，<xref:System.Windows.Forms.BindingNavigator> 组件会已有一个**“保存”**按钮，但 `` Windows 窗体设计器并没有生成代码。  如果这样，可将前面的代码加入该按钮的 <xref:System.Windows.Forms.ToolStripItem.Click> 事件处理程序中，而不是在 <xref:System.Windows.Forms.ToolStrip> 上创建全新的按钮。  不过，该按钮在默认情况下是禁用的，因此要使按钮正常工作，必须将其 <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> 属性设置为 `true`。  
  
12. 为前面创建的**“取消”**<xref:System.Windows.Forms.ToolStripButton> `` 的 `` <xref:System.Windows.Forms.ToolStripItem.Click> 事件创建事件处理程序，并编写代码以取消对所显示数据记录所做的任何更改。  
  
     \[Visual Basic\]  
  
    ```  
    Private Sub CancelButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CancelButton.Click  
        BindingSourceName.CancelEdit()  
    End Sub  
    ```  
  
     \[C\#\]  
  
    ```  
    private void CancelButton_Click(System.Object sender, System.EventArgs e)  
    {  
        BindingSourceName.CancelEdit();  
    }  
    ```  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.BindingSource.CancelEdit%2A> 方法按数据行起作用。  在定位到下一记录前，保存您在查看该单一记录时所做的任何更改。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.ToolStrip>   
 [BindingNavigator 控件](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)   
 [BindingSource 组件概述](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)