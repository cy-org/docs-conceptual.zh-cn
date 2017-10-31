---
title: "演练：使用 Visual C# 从 Windows 窗体控件继承 | Microsoft Docs"
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
ms.assetid: 09476da0-8d4c-4a4c-b969-649519dfb438
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 演练：使用 Visual C# 从 Windows 窗体控件继承
使用 [!INCLUDE[csprcslong](../../../../includes/csprcslong-md.md)] 可以通过继承创建功能强大的自定义控件。  通过继承，可以创建不仅保留了标准 Windows 窗体控件的所有内在功能，而且还包含自定义功能的控件。  在本演练中，将创建一个名为 `ValueButton` 的简单继承控件。  此按钮将继承标准 Windows 窗体 <xref:System.Windows.Forms.Button> 控件的功能，并将公开一个名为 `ButtonValue` 的自定义属性。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 创建新项目时，应指定其名称以便设置根命名空间、程序集名称和项目名称，并确保默认组件位于正确的命名空间中。  
  
#### 创建 ValueButtonLib 控件库和 ValueButton 控件  
  
1.  在**“文件”**菜单上，指向**“新建”**，然后单击**“项目”**打开**“新建项目”**对话框。  
  
2.  在 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 项目列表中，选择**“Windows 窗体控件库”**项目模板，然后在**“名称”**框中键入 `ValueButtonLib`。  
  
     默认情况下，项目名称 `ValueButtonLib` 也被分配到根命名空间中。  根命名空间用于限定程序集中的组件名。  例如，如果两个程序集提供名为 `ValueButton` 的组件，则可以使用 `ValueButtonLib.ValueButton` 指定 `ValueButton` 组件。  有关更多信息，请参见[命名空间](../Topic/Namespaces%20\(C%23%20Programming%20Guide\).md)。  
  
3.  在**“解决方案资源管理器”**中右击**“UserControl1.cs”**，再从快捷菜单中选择**“重命名”**。  将文件名更改为 `ValueButton.cs`。  系统询问是否重命名对代码元素“`UserControl1`”的所有引用时，单击**“是”**按钮。  
  
4.  在**“解决方案资源管理器”**中右击**“ValueButton.cs”**，再选择**“查看代码”**。  
  
5.  找到 `class` 语句行 `public partial class ValueButton`，并将此控件继承的类型从 <xref:System.Windows.Forms.UserControl> 更改为 <xref:System.Windows.Forms.Button>。  这允许您所继承的控件继承 <xref:System.Windows.Forms.Button> 控件的所有功能。  
  
6.  在**“解决方案资源管理器”**中打开**“ValueButton.cs”**节点，以显示设计器生成的代码文件**“ValueButton.Designer.cs”**。  在**“代码编辑器”**中打开此文件。  
  
7.  找到 `InitializeComponent` 方法并删除分配 <xref:System.Windows.Forms.ContainerControl.AutoScaleMode%2A> 属性的行。  <xref:System.Windows.Forms.Button> 控件中没有此属性。  
  
8.  在**“文件”**菜单中，选择**“全部保存”**以保存项目。  
  
    > [!NOTE]
    >  可视化设计器不再可用。  由于 <xref:System.Windows.Forms.Button> 控件自行绘制，因此您无法在设计器中修改其外观。  除非在代码中进行修改，否则它的可视化表示形式将与它所继承的类（即 <xref:System.Windows.Forms.Button>）的可视化表示形式完全一样。  但您仍然可以向设计器图面添加不含 UI 元素的组件。  
  
## 将属性添加到继承的控件中  
 继承的 Windows 窗体控件的可能用途之一是创建与标准 Windows 窗体控件的外观相同、但公开自定义属性的控件。  在本节中，将向控件中添加名为 `ButtonValue` 的属性。  
  
#### 添加 Value 属性  
  
1.  在**“解决方案资源管理器”**中，右击**“ValueButton.cs”**，然后从快捷菜单中单击**“查看代码”**。  
  
2.  找到 `class` 语句。  紧接在 `{` 后面键入下列代码：  
  
     \[C\#\]  
  
    ```  
    // Creates the private variable that will store the value of your   
    // property.  
    private int varValue;  
    // Declares the property.  
    public int ButtonValue  
    {  
       // Sets the method for retrieving the value of your property.  
       get  
       {  
          return varValue;  
       }  
       // Sets the method for setting the value of your property.  
       set  
       {  
          varValue = value;  
       }  
    }  
    ```  
  
     此代码设置存储和检索 `ButtonValue` 属性的方法。  `get` 语句将返回的值设置为存储在私有变量 `varValue` 中的值，而 `set` 语句通过使用 `value` 关键字设置该私有变量的值。  
  
3.  在**“文件”**菜单中，选择**“全部保存”**以保存项目。  
  
## 测试控件  
 控件不是独立的项目，它们必须寄宿在某个容器中。  为了测试控件，必须提供一个测试项目，以使控件在其中运行。  您还必须通过生成（编译）该控件使测试项目能够访问它。  在本节中，将生成控件并在 Windows 窗体中测试它。  
  
#### 生成控件  
  
1.  在**“生成”**菜单上，单击**“生成解决方案”**。  
  
     生成应该成功，没有任何编译器错误或警告。  
  
#### 创建测试项目  
  
1.  在**“文件”**菜单上，指向**“添加”**，然后单击**“新建项目”**打开**“添加新项目”**对话框。  
  
2.  在**“Visual C\#”**节点下选择**“Windows”**节点，再单击**“Windows 窗体应用程序”**。  
  
3.  在**“名称”**框中键入 `Test`。  
  
4.  在**“解决方案资源管理器”**中，右击测试项目的**“引用”**节点，然后从快捷菜单上选择**“添加引用”**以显示**“添加引用”**对话框。  
  
5.  单击标记为**“项目”**的选项卡。  **“项目名称”**下将列出 `ValueButtonLib` 项目。  双击该项目以将引用添加到测试项目。  
  
6.  在**“解决方案资源管理器”**中，右击**“测试”**并选择**“生成”**。  
  
#### 将控件添加到窗体  
  
1.  在**“解决方案资源管理器”**中，右击**“Form1.cs”**，然后从快捷菜单中选择**“视图设计器”**。  
  
2.  在**“工具箱”**中单击**“ValueButtonLib 组件”**。  双击**“ValueButton”**。  
  
     窗体上出现一个**“ValueButton”**。  
  
3.  右击**“ValueButton”**并从快捷菜单中选择**“属性”**。  
  
4.  在**“属性”**窗口中检查该控件的属性。  注意，除增加了一个 `ButtonValue` 属性外，它们与标准按钮公开的属性相同。  
  
5.  将 `ButtonValue` 属性设置为 `5`。  
  
6.  在**“工具箱”**的**“所有 Windows 窗体”**选项卡中，双击**“标签”**，将 <xref:System.Windows.Forms.Label> 控件添加到窗体中。  
  
7.  将标签重新定位到窗体的中央。  
  
8.  双击 `valueButton1`。  
  
     将响应 `valueButton1_Click` 事件而打开**“代码编辑器”**。  
  
9. 插入下面的代码行。  
  
     \[C\#\]  
  
    ```  
    label1.Text = valueButton1.ButtonValue.ToString();  
    ```  
  
10. 在**“解决方案资源管理器”**中，右击**“测试”**，然后从快捷菜单中选择**“设为启动项目”**。  
  
11. 从**“调试”**菜单中选择**“启动调试”**。  
  
     `Form1` 出现。  
  
12. 单击 `valueButton1`。  
  
     `label1` 中显示数字“5”，说明继承控件的 `ButtonValue` 属性已经通过 `valueButton1_Click` 方法传递到 `label1`。  这样，`ValueButton` 控件便继承了标准 Windows 窗体按钮的所有功能，但是公开了一个附加的自定义属性。  
  
## 请参阅  
 [使用组件编程](../Topic/Programming%20with%20Components.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)   
 [如何：在“选择工具箱项”对话框中显示控件](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [演练：使用 Visual C\# 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)