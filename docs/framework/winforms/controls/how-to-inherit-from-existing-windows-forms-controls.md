---
title: "如何：从现有 Windows 窗体控件继承 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 继承"
  - "继承, Windows 窗体自定义控件"
ms.assetid: 1e1fc8ea-c615-4cf0-a356-16d6df7444ab
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：从现有 Windows 窗体控件继承
如果要扩展现有控件的功能，可以通过继承创建一个由现有控件导出的控件。  当从一个现有控件继承时，就继承了该控件的所有功能和可视属性。  例如，如果您正在创建一个从 <xref:System.Windows.Forms.Button> 继承的控件，则新控件的外观和操作方式与标准的 <xref:System.Windows.Forms.Button> 控件完全一样。  您然后还可通过实现自定义方法和属性，扩展或修改新控件的功能。  在某些控件中，还可以通过重写继承控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法更改其可视外观。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建继承控件  
  
1.  创建一个新的**“Windows 窗体应用程序”**项目。  
  
2.  从**“项目”**菜单中选择**“添加新项”**。  
  
     将显示**“添加新项”**对话框。  
  
3.  在**“添加新项”**对话框中双击**“自定义控件”**。  
  
     一个新的自定义控件被添加到项目中。  
  
4.  如果使用的是 Visual Basic，则在**“解决方案资源管理器”**的顶部单击**“显示所有文件”**。  展开 CustomControl1.vb，然后在代码编辑器中打开 CustomControl1.Designer.vb。  
  
5.  如果使用的是 C\#，则在代码编辑器中打开 CustomControl1.cs。  
  
6.  查找继承自 <xref:System.Windows.Forms.Control> 的类声明。  
  
7.  将基类更改为要从中继承的控件。  
  
     例如，如果要从 <xref:System.Windows.Forms.Button> 继承，请将类声明更改为以下内容：  
  
    ```vb  
    Partial Class CustomControl1  
        Inherits System.Windows.Forms.Button  
    ```  
  
    ```csharp  
    public partial class CustomControl1 : System.Windows.Forms.Button  
    ```  
  
8.  如果使用的是 Visual Basic，请保存并关闭 CustomControl1.Designer.vb。  在代码编辑器中打开 CustomControl1.vb。  
  
9. 实现将合并到控件中的任合自定义方法或属性。  
  
10. 如果要修改控件的图形外观，则重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
    > [!NOTE]
    >  重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 将禁止修改所有控件的外观。  那些由 Windows 完成其所有绘图的控件（例如 <xref:System.Windows.Forms.TextBox>）从不调用它们的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，因此将永远不会使用自定义代码。  请参见您要修改的特定控件的帮助文档，查看 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法是否可用。  有关所有 Windows 窗体控件的列表，请参见 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)。  如果某个控件未将 <xref:System.Windows.Forms.Control.OnPaint%2A> 作为成员方法列出，则您无法通过重写此方法改变其外观。  有关自定义绘制的更多信息，请参见 [自定义控件的绘制和呈现](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md)。  
  
    ```vb  
    Protected Overrides Sub OnPaint(ByVal e As _  
       System.Windows.Forms.PaintEventArgs)  
       MyBase.OnPaint(e)  
       ' Insert code to do custom painting.   
       ' If you want to completely change the appearance of your control,  
       ' do not call MyBase.OnPaint(e).  
    End Sub  
  
    ```  
  
    ```csharp  
    protected override void OnPaint(PaintEventArgs pe)  
    {  
       base.OnPaint(pe);  
       // Insert code to do custom painting.  
       // If you want to completely change the appearance of your control,  
       // do not call base.OnPaint(pe).  
    }  
    ```  
  
11. 保存并测试控件。  
  
## 请参阅  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [如何：从 Control 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [如何：从 UserControl 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [如何：创作 Windows 窗体的控件](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [演练：使用 Visual Basic 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [演练：使用 Visual C\# 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)