---
title: "如何：向 Windows 窗体添加控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 添加"
  - "Windows 窗体控件, 添加到窗体"
ms.assetid: 2af86001-9d62-4154-87fb-66db2c3cd9fd
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：向 Windows 窗体添加控件
大多数窗体都是通过将控件添加到窗体表面来定义用户界面 \(UI\) 的方式进行设计的。  “控件”是窗体上的一个组件，用于显示信息或接受用户输入。  有关控件的更多信息，请参见 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在窗体上绘制控件  
  
1.  打开窗体。  有关更多信息，请参见 [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/zh-cn/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5)。  
  
2.  在**“工具箱”**中单击要添加到窗体的控件。  
  
3.  在该窗体上，单击希望控件左上角位于的位置，然后拖动到希望该控件右下角位于的位置。  
  
     控件按指定的位置和大小添加到窗体中。  
  
    > [!NOTE]
    >  每个控件都有定义的默认大小。  可按控件的默认大小将控件添加到窗体上，方法是将控件从**“工具箱”**拖动到窗体上。  
  
### 将控件拖动到窗体上  
  
1.  打开窗体。  有关更多信息，请参见 [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/zh-cn/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5)。  
  
2.  在**“工具箱”**中单击所需的控件并将其拖到窗体上。  
  
     控件以其默认大小添加到窗体上的指定位置。  
  
    > [!NOTE]
    >  可双击**“工具箱”**中的控件，将该控件按其默认大小添加到窗体的左上角。  
  
     也可在运行时动态地将控件添加到窗体中。  在下面的代码示例中，单击 <xref:System.Windows.Forms.Button> 控件时，会将一个 <xref:System.Windows.Forms.TextBox> 添加到窗体。  
  
    > [!NOTE]
    >  下面的过程要求存在带有**“按钮”**控件的窗体，该窗体上已放置 `Button1`。  
  
### 以编程方式向窗体添加控件  
  
1.  在窗体的类的内部，在处理按钮的 `Click` 事件的方法中，插入类似于以下内容的代码，以添加对控件变量的引用，设置控件的 `Location`，然后添加该控件。  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim MyText As New TextBox()  
       MyText.Location = New Point(25, 25)  
       Me.Controls.Add(MyText)  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
       TextBox myText = new TextBox();  
       myText.Location = new Point(25,25);  
       this.Controls.Add (myText);  
    }  
  
    ```  
  
    ```cpp  
    private:  
      System::Void button1_Click(System::Object ^  sender,  
        System::EventArgs ^  e)  
      {  
        TextBox ^ myText = gcnew TextBox();  
        myText->Location = Point(25,25);  
        this->Controls->Add(myText);  
      }  
    ```  
  
    > [!NOTE]
    >  还可以添加代码来初始化控件的其他属性。  
  
    > [!IMPORTANT]
    >  如果您引用了恶意的 `UserControl`，就可能会使本地计算机的安全受到来自网络的威胁。  只有发生以下情况时，这才是需要注意的问题：一个恶意的用户创建了一个破坏性的自定义控件，然后您又错误地将该控件添加到您的项目中。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [如何：调整 Windows 窗体上控件的大小](../../../../docs/framework/winforms/controls/how-to-resize-controls-on-windows-forms.md)   
 [如何：设置 Windows 窗体控件所显示的文本](../../../../docs/framework/winforms/controls/how-to-set-the-text-displayed-by-a-windows-forms-control.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)