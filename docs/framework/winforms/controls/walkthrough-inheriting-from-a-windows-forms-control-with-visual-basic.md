---
title: "演练：使用 Visual Basic 从 Windows 窗体控件继承 | Microsoft Docs"
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
  - "继承, 控件"
  - "继承, 自定义控件"
  - "继承, 演练"
  - "Windows 窗体控件, 继承"
ms.assetid: fb58d7c8-b702-4478-ad31-b00cae118882
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 演练：使用 Visual Basic 从 Windows 窗体控件继承
使用 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 可通过继承来创建功能强大的自定义控件。  通过继承，可以创建不仅保留了标准 Windows 窗体控件的所有内在功能，而且还包含自定义功能的控件。  在本演练中，将创建一个名为 `ValueButton` 的简单继承控件。  此按钮将继承标准 Windows 窗体 <xref:System.Windows.Forms.Button> 控件的功能，并将公开一个名为 `ButtonValue` 的自定义属性。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 创建新项目时，应指定其名称以便设置根命名空间、程序集名称和项目名称，并确保默认组件位于正确的命名空间中。  
  
#### 创建 ValueButtonLib 控件库和 ValueButton 控件  
  
1.  在**“文件”**菜单上，指向**“新建”**，然后单击**“项目”**打开**“新建项目”**对话框。  
  
2.  在 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 项目列表中，选择**“Windows 窗体控件库”**项目模板，然后在**“名称”**框中键入 `ValueButtonLib`。  
  
     默认情况下，项目名称 `ValueButtonLib` 也被分配到根命名空间中。  根命名空间用于限定程序集中的组件名。  例如，如果两个程序集提供名为 `ValueButton` 的组件，则可以使用 `ValueButtonLib.ValueButton` 指定 `ValueButton` 组件。  有关更多信息，请参见 [Visual Basic 中的命名空间](../Topic/Namespaces%20in%20Visual%20Basic.md)。  
  
3.  在**“解决方案资源管理器”**中，右击**“UserControl1.vb”**，然后从快捷菜单中选择**“重命名”**。  将文件名更改为`“ValueButton.vb”`。  系统询问是否重命名对代码元素“UserControl1”的所有引用时，单击**“是”**按钮。  
  
4.  在**“解决方案资源管理器”**中，单击**“显示所有文件”**按钮。  
  
5.  打开**“ValueButton.vb”**节点显示设计器生成的代码文件**“ValueButton.Designer.vb”**。  在**“代码编辑器”**中打开此文件。  
  
6.  找到 `Class` 语句 `Partial Public Class ValueButton`，将该控件要继承的类型从 <xref:System.Windows.Forms.UserControl> 更改为 <xref:System.Windows.Forms.Button>。  这允许您所继承的控件继承 <xref:System.Windows.Forms.Button> 控件的所有功能。  
  
7.  找到 `InitializeComponent` 方法并删除分配 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 属性的行。  <xref:System.Windows.Forms.Button> 控件中没有此属性。  
  
8.  在**“文件”**菜单中，选择**“全部保存”**以保存项目。  
  
     注意，可视化设计器不再可用。  由于 <xref:System.Windows.Forms.Button> 控件自行绘制，因此您无法在设计器中修改其外观。  除非在代码中进行修改，否则它的可视化表示形式将与它所继承的类（即 <xref:System.Windows.Forms.Button>）的可视化表示形式完全一样。  
  
> [!NOTE]
>  但您仍然可以向设计器图面添加不含 UI 元素的组件。  
  
## 将属性添加到继承的控件中  
 继承的 Windows 窗体控件的可能用途之一是创建与标准 Windows 窗体控件的外观和行为相同、但公开自定义属性的控件。  在本节中，将向控件中添加名为 `ButtonValue` 的属性。  
  
#### 添加 Value 属性  
  
1.  在**解决方案资源管理器**中，右击**“ValueButton.vb”**，然后从快捷菜单中单击**“查看代码”**。  
  
2.  找到 `Public Class ValueButton` 语句。  在紧靠该语句下面键入下列代码：  
  
     \[Visual Basic\]  
  
    ```  
    ' Creates the private variable that will store the value of your   
    ' property.  
    Private varValue as integer  
    ' Declares the property.  
    Property ButtonValue() as Integer  
    ' Sets the method for retrieving the value of your property.  
       Get  
          Return varValue  
       End Get  
    ' Sets the method for setting the value of your property.  
       Set(ByVal Value as Integer)  
          varValue = Value  
       End Set  
    End Property  
    ```  
  
     此代码设置存储和检索 `ButtonValue` 属性的方法。  `Get` 语句将返回的值设置为存储在私有变量 `varValue` 中的值，而 `Set` 语句通过使用 `Value` 关键字设置该私有变量的值。  
  
3.  在**“文件”**菜单中，选择**“全部保存”**以保存项目。  
  
## 测试控件  
 控件不是独立的项目，它们必须寄宿在某个容器中。  为了测试控件，必须提供一个测试项目，以使控件在其中运行。  您还必须通过生成（编译）该控件使测试项目能够访问它。  在本节中，将生成控件并在 Windows 窗体中测试它。  
  
#### 生成控件  
  
1.  在**“生成”**菜单上，单击**“生成解决方案”**。  
  
     生成应该成功，没有任何编译器错误或警告。  
  
#### 创建测试项目  
  
1.  在**“文件”**菜单上，指向**“添加”**，然后单击**“新建项目”**打开**“添加新项目”**对话框。  
  
2.  选择 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 项目节点并单击**“Windows 窗体应用程序”**。  
  
3.  在**“名称”**框中键入 `Test`。  
  
4.  在**“解决方案资源管理器”**中，单击**“显示所有文件”**按钮。  
  
5.  在**“解决方案资源管理器”**中，右击测试项目的**“引用”**节点，然后从快捷菜单上选择**“添加引用”**以显示**“添加引用”**对话框。  
  
6.  单击**“项目”**选项卡。  
  
7.  单击标记为**“项目”**的选项卡。  **“项目名称”**下将列出 `ValueButtonLib` 项目。  双击该项目以将引用添加到测试项目。  
  
8.  在**“解决方案资源管理器”**中，右击**“测试”**并选择**“生成”**。  
  
#### 将控件添加到窗体  
  
1.  在**“解决方案资源管理器”**中，右击**“Form1.vb”**，并从快捷菜单中选择**“视图设计器”**。  
  
2.  在**“工具箱”**中单击**“ValueButtonLib 组件”**。  双击**“ValueButton”**。  
  
     窗体上出现一个**“ValueButton”**。  
  
3.  右击**“ValueButton”**并从快捷菜单中选择**“属性”**。  
  
4.  在**“属性”**窗口中检查该控件的属性。  注意，除增加了一个 `ButtonValue` 属性外，它们与标准按钮公开的属性相同。  
  
5.  将 `ButtonValue` 属性设置为 `5`。  
  
6.  在**“工具箱”**的**“所有 Windows 窗体”**选项卡上，双击**“Label”**向窗体添加一个 <xref:System.Windows.Forms.Label> 控件。  
  
7.  将标签重新定位到窗体的中央。  
  
8.  双击 `ValueButton1`。  
  
     将响应 `ValueButton1_Click` 事件而打开**“代码编辑器”**。  
  
9. 键入以下代码行。  
  
     \[Visual Basic\]  
  
    ```  
    Label1.Text = CStr(ValueButton1.ButtonValue)  
    ```  
  
10. 在**“解决方案资源管理器”**中，右击**“测试”**，然后从快捷菜单中选择**“设为启动项目”**。  
  
11. 从**“调试”**菜单中选择**“启动调试”**。  
  
     `Form1` 出现。  
  
12. 单击 `Valuebutton1`。  
  
     `Label1` 中显示数字“5”，表明继承的控件的 `ButtonValue` 属性通过 `ValueButton1_Click` 方法传递给了 `Label1`。  这样，`ValueButton` 控件便继承了标准 Windows 窗体按钮的所有功能，但是公开了一个附加的自定义属性。  
  
## 请参阅  
 [演练：使用 Visual Basic 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [如何：在“选择工具箱项”对话框中显示控件](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [NOT IN BUILD: Inheritance in Visual Basic](http://msdn.microsoft.com/zh-cn/e5e6e240-ed31-4657-820c-079b7c79313c)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)