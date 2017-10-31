---
title: "如何：用 Windows 窗体创建多窗格用户界面 | Microsoft Docs"
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
  - "ListView 控件 [Windows 窗体], 示例"
  - "Panel 控件 [Windows 窗体], 示例"
  - "RichTextBox 控件 [Windows 窗体], 示例"
  - "SplitContainer 控件 [Windows 窗体], 示例"
  - "Splitter 控件 [Windows 窗体], 示例"
  - "TreeView 控件 [Windows 窗体], 示例"
ms.assetid: e79f6bcc-3740-4d1e-b46a-c5594d9b7327
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 如何：用 Windows 窗体创建多窗格用户界面
在下面的过程中，将创建一个类似于在 Microsoft Outlook 中使用的多窗格用户界面，该界面中包含**“文件夹列表”**、**“邮件”**窗格和**“预览”**窗格。  这种排列主要是通过在窗体上停靠控件实现的。  
  
 在停靠控件时，可以确定控件要紧靠父容器的哪个边缘。  这样，如果将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>，控件的右边缘将停靠在它的父控件的右边缘。  此外，控件停靠边缘的大小将调整为与它的容器控件的大小匹配。  有关 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性工作方式的更多信息，请参见 [如何：在 Windows 窗体上停靠控件](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)。  
  
 该过程的重点是在窗体上排列 <xref:System.Windows.Forms.SplitContainer> 和其他控件，而不是添加功能以使得应用程序类似于 Microsoft Outlook。  
  
 若要创建该用户界面，请将所有控件放到 <xref:System.Windows.Forms.SplitContainer> 控件（其左侧面板中包含 <xref:System.Windows.Forms.TreeView> 控件）中。  <xref:System.Windows.Forms.SplitContainer> 控件的右侧面板中包含另一个 <xref:System.Windows.Forms.SplitContainer> 控件，其中 <xref:System.Windows.Forms.ListView> 控件在 <xref:System.Windows.Forms.RichTextBox> 控件上方。  这些 <xref:System.Windows.Forms.SplitContainer> 控件支持在窗体上分别调整其他控件的大小。  可以改编此过程中的方法，制作出您自己的自定义用户界面。  
  
### 以编程方式创建 Outlook 样式的用户界面  
  
1.  在窗体内，声明组成用户界面的每个控件。  本示例使用 <xref:System.Windows.Forms.TreeView>、<xref:System.Windows.Forms.ListView>、<xref:System.Windows.Forms.SplitContainer> 和 <xref:System.Windows.Forms.RichTextBox> 控件来创建类似于 Microsoft Outlook 的用户界面。  
  
    ```vb  
    Private WithEvents treeView1 As System.Windows.Forms.TreeView  
    Private WithEvents listView1 As System.Windows.Forms.ListView  
    Private WithEvents richTextBox1 As System.Windows.Forms.RichTextBox  
    Private WithEvents splitContainer1 As _  
        System.Windows.Forms.SplitContainer  
    Private WithEvents splitContainer2 As _  
        System.Windows.Forms.SplitContainer  
  
    ```  
  
    ```csharp  
    private System.Windows.Forms.TreeView treeView1;  
    private System.Windows.Forms.ListView listView1;  
    private System.Windows.Forms.RichTextBox richTextBox1;  
    private System.Windows.Forms. SplitContainer splitContainer2;  
    private System.Windows.Forms. SplitContainer splitContainer1;  
  
    ```  
  
2.  创建定义用户界面的过程。  下面的代码设置属性，以使窗体类似于 Microsoft Outlook 的用户界面。  但是，通过使用其他控件或使它们停靠在不同的位置，一样可以轻松创建同样灵活的其他用户界面。  
  
    ```vb  
    Public Sub CreateOutlookUI()  
        ' Create an instance of each control being used.  
        Me.components = New System.ComponentModel.Container()  
        Me.treeView1 = New System.Windows.Forms.TreeView()  
        Me.listView1 = New System.Windows.Forms.ListView()  
        Me.richTextBox1 = New System.Windows.Forms.RichTextBox()  
        Me.splitContainer1 = New System.Windows.Forms.SplitContainer()  
        Me.splitContainer2= New System.Windows.Forms. SplitContainer()  
  
        ' Should you develop this into a working application,  
        ' use the AddHandler method to hook up event procedures here.  
  
        ' Set properties of TreeView control.  
        ' Use the With statement to avoid repetitive code.  
        With Me.treeView1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 0  
            .Nodes.Add("treeView")  
        End With  
  
    ' Set properties of ListView control.  
       With Me.listView1  
          .Dock = System.Windows.Forms.DockStyle.Top  
          .TabIndex = 2  
          .Items.Add("listView")  
       End With  
  
    ' Set properties of RichTextBox control.  
       With Me.richTextBox1  
          .Dock = System.Windows.Forms.DockStyle.Fill  
          .TabIndex = 3  
          .Text = "richTextBox1"  
       End With  
  
        ' Set properties of the first SplitContainer control.  
        With Me.splitContainer1  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 1  
            .SplitterWidth = 4  
            .SplitterDistance = 150  
            .Orientation = Orientation.Horizontal  
            .Panel1.Controls.Add(Me.listView1)  
            .Panel2.Controls.Add(Me.richTextBox1)  
    End With  
  
        ' Set properties of the second SplitContainer control.  
        With Me.splitContainer2  
            .Dock = System.Windows.Forms.DockStyle.Fill  
            .TabIndex = 4  
            .SplitterWidth = 4  
            .SplitterDistance = 100  
            .Panel1.Controls.Add(Me.treeView1)  
            .Panel2.Controls.Add(Me.SplitContainer1)  
    End With  
  
    ' Add the main SplitContainer control to the form.  
        Me.Controls.Add(Me.splitContainer2)  
        Me.Text = "Intricate UI Example"  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createOutlookUI()  
    {  
        // Create an instance of each control being used.  
        treeView1 = new System.Windows.Forms.TreeView();  
        listView1 = new System.Windows.Forms.ListView();  
        richTextBox1 = new System.Windows.Forms.RichTextBox();  
        splitContainer2 = new System.Windows.Forms.SplitContainer();  
        splitContainer1 = new System.Windows.Forms.SplitContainer();  
  
        // Insert code here to hook up event methods.  
  
        // Set properties of TreeView control.  
        treeView1.Dock = System.Windows.Forms.DockStyle.Fill;  
        treeView1.TabIndex = 0;  
        treeView1.Nodes.Add("treeView");  
  
        // Set properties of ListView control.  
        listView1.Dock = System.Windows.Forms.DockStyle.Top;  
        listView1.TabIndex = 2;  
        listView1.Items.Add("listView");  
  
        // Set properties of RichTextBox control.  
        richTextBox1.Dock = System.Windows.Forms.DockStyle.Fill;  
        richTextBox1.TabIndex = 3;  
        richTextBox1.Text = "richTextBox1";  
  
        // Set properties of first SplitContainer control.  
        splitContainer1.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 1;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 150;  
        splitContainer2.Orientation = Orientation.Horizontal;  
        splitContainer2.Panel1.Controls.Add(this.listView1);  
        splitContainer2.Panel1.Controls.Add(this.richTextBox1);  
  
        // Set properties of second SplitContainer control.  
        splitContainer2.Dock = System.Windows.Forms.DockStyle.Fill;  
        splitContainer2.TabIndex = 4;  
        splitContainer2.SplitterWidth = 4;  
        splitContainer2.SplitterDistance = 100;  
        splitContainer2.Panel1.Controls.Add(this.treeView1);  
        splitContainer2.Panel1.Controls.Add(this.splitContainer1);  
  
        // Add the main SplitContainer control to the form.  
        this.Controls.Add(this.splitContainer2);  
        this.Text = "Intricate UI Example";  
    }  
  
    ```  
  
3.  在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 中，添加对在 `New()` 过程中刚创建的过程的调用。  在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中，将这行代码添加到窗体类的构造函数。  
  
    ```vb  
    ' Add this to the New procedure.  
    CreateOutlookUI()  
  
    ```  
  
    ```csharp  
    // Add this to the form class's constructor.  
    createOutlookUI();  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [SplitContainer 控件](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)   
 [如何：使用设计器用 Windows 窗体创建多窗格用户界面](../../../../docs/framework/winforms/controls/create-a-multipane-user-interface-with-wf-using-the-designer.md)