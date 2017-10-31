---
title: "演练：在 Windows 窗体中执行拖放操作 | Microsoft Docs"
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
  - "拖放, Windows 窗体"
  - "Windows 窗体, 拖放操作"
ms.assetid: eb66f6bf-4a7d-4c2d-b276-40fefb2d3b6c
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 演练：在 Windows 窗体中执行拖放操作
要在基于 Windows 的应用程序中执行拖放操作，必须处理一系列事件，特别是 <xref:System.Windows.Forms.Control.DragEnter>、<xref:System.Windows.Forms.Control.DragLeave> 和 <xref:System.Windows.Forms.Control.DragDrop> 事件。  通过使用这些事件的事件参数中的可用信息，可以轻松地实现拖放操作。  
  
## 拖动数据  
 所有拖放操作都从拖动开始。  实现在拖动开始时收集数据的功能在 <xref:System.Windows.Forms.Control.DoDragDrop%2A> 方法中实现。  
  
 在下面的示例中，使用 <xref:System.Windows.Forms.Control.MouseDown> 事件启动拖动操作，因为该事件最直观（大部分拖放操作都从按下鼠标按钮开始）。  但是，请记住，任何事件都可用于启动拖放过程。  
  
> [!NOTE]
>  某些控件具有自定义的、拖动特定的事件。  例如，<xref:System.Windows.Forms.ListView> 和 <xref:System.Windows.Forms.TreeView> 控件有 <xref:System.Windows.Forms.TreeView.ItemDrag> 事件。  
  
#### 启动拖动操作  
  
1.  在拖动起始控件的 <xref:System.Windows.Forms.Control.MouseDown>事件，请使用 `DoDragDrop` 方法设置要拖动的数据，并拖动将具有的允许效果。  有关更多信息，请参见 <xref:System.Windows.Forms.DragEventArgs.Data%2A> 和 <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A>。  
  
     下面的示例显示如何启动拖动操作。  拖动起始控件是 <xref:System.Windows.Forms.Button> 控件，被拖动的数据是表示 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性的字符串，允许的效果是复制或移动。  
  
    ```vb  
    Private Sub Button1_MouseDown(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles Button1.MouseDown  
       Button1.DoDragDrop(Button1.Text, DragDropEffects.Copy Or DragDropEffects.Move)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_MouseDown(object sender,   
    System.Windows.Forms.MouseEventArgs e)  
    {  
       button1.DoDragDrop(button1.Text, DragDropEffects.Copy |   
          DragDropEffects.Move);  
    }  
  
    ```  
  
    > [!NOTE]
    >  任何数据都可用作 `DoDragDrop` 方法中的参数；在上面的示例中，使用 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性（而不是对值进行硬编码或从数据集检索数据），因为该属性与拖动起始位置（<xref:System.Windows.Forms.Button> 控件）相关。  当将拖放操作合并到基于 Windows 的应用程序中时，请牢记这一点。  
  
 拖动操作生效后，可以处理 <xref:System.Windows.Forms.Control.QueryContinueDrag> 事件，该事件“要求系统权限”才能继续该拖动操作。  当处理此方法时，调用影响拖动操作的方法（例如，当光标悬停在 <xref:System.Windows.Forms.TreeView> 控件上时，展开该控件中的 <xref:System.Windows.Forms.TreeNode>）也正是时候。  
  
## 放置数据  
 开始从 Windows 窗体或控件上的某个位置拖动数据后，将很自然地要将其放置在某处。  当光标经过为放置数据而进行了正确配置的窗体或控件区域时，会发生改变。  可以通过设置 <xref:System.Windows.Forms.Control.AllowDrop%2A> 属性并处理 <xref:System.Windows.Forms.Control.DragEnter> 和 <xref:System.Windows.Forms.Control.DragDrop> 事件，使 Windows 窗体或控件内的任何区域接受放置的数据。  
  
#### 执行放置  
  
1.  将 <xref:System.Windows.Forms.Control.AllowDrop%2A> 属性设置为 true。  
  
2.  在将要发生放置操作的控件的 `DragEnter` 事件中，确保正在拖动的数据是可接受的类型（在本例中为 <xref:System.Windows.Forms.Control.Text%2A>）。  代码随后将发生放置操作时产生的效果设置为 <xref:System.Windows.Forms.DragDropEffects> 枚举中的值。  有关更多信息，请参见 <xref:System.Windows.Forms.DragEventArgs.Effect%2A>。  
  
    ```vb  
    Private Sub TextBox1_DragEnter(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragEnter  
       If (e.Data.GetDataPresent(DataFormats.Text)) Then  
         e.Effect = DragDropEffects.Copy  
       Else  
         e.Effect = DragDropEffects.None  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_DragEnter(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       if (e.Data.GetDataPresent(DataFormats.Text))   
          e.Effect = DragDropEffects.Copy;  
       else  
          e.Effect = DragDropEffects.None;  
    }  
  
    ```  
  
    > [!NOTE]
    >  您可以定义自己的 <xref:System.Windows.Forms.DataFormats>，方法是将自己的对象指定为 <xref:System.Windows.Forms.DataObject.SetData%2A> 方法的 <xref:System.Object> 参数。  在进行该操作时，请确保指定的对象可序列化。  有关更多信息，请参见 [ISerializable 接口](frlrfSystemRuntimeSerializationISerializableClassTopic)。  
  
3.  在将要发生放置操作的控件的 <xref:System.Windows.Forms.Control.DragDrop> 事件中，使用 <xref:System.Windows.Forms.DataObject.GetData%2A> 方法检索正在拖动的数据。  有关更多信息，请参见 [DtaObject.Data 属性](frlrfSystemSecurityCryptographyXmlDataObjectClassDataTopic)。  
  
     在下面的示例中，<xref:System.Windows.Forms.TextBox> 控件是要拖动到的控件（发生放置操作的位置）。  代码将 <xref:System.Windows.Forms.TextBox> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性设置为等于正在拖动的数据。  
  
    ```vb  
    Private Sub TextBox1_DragDrop(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragDrop  
       TextBox1.Text = e.Data.GetData(DataFormats.Text).ToString  
    End Sub  
  
    ```  
  
    ```csharp  
    private void textBox1_DragDrop(object sender,   
    System.Windows.Forms.DragEventArgs e)  
    {  
       textBox1.Text = e.Data.GetData(DataFormats.Text).ToString();  
    }  
  
    ```  
  
    > [!NOTE]
    >  另外，还可以使用 <xref:System.Windows.Forms.DragEventArgs.KeyState%2A> 属性，这样，将根据拖放操作过程中按下的键，产生相应的效果（例如，标准操作是在按 Ctrl 键时复制拖动的数据）。  
  
## 请参阅  
 [如何：将数据添加到剪贴板](../../../../docs/framework/winforms/advanced/how-to-add-data-to-the-clipboard.md)   
 [如何：从剪贴板检索数据](../../../../docs/framework/winforms/advanced/how-to-retrieve-data-from-the-clipboard.md)   
 [拖放操作和剪贴板支持](../../../../docs/framework/winforms/advanced/drag-and-drop-operations-and-clipboard-support.md)