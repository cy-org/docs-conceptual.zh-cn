---
title: "演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合 | Microsoft Docs"
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
  - "集合, 序列化"
  - "集合, 标准类型"
  - "DesiginerSerializationVisibilityAttribute 类"
  - "序列化, 集合"
  - "标准类型, 集合"
ms.assetid: 020c9df4-fdc5-4dae-815a-963ecae5668c
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合
有时您的自定义控件会将一个集合作为属性公开。  本演练演示如何使用 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> 类控制在设计时序列化集合的方式。  将 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> 值应用于您的集合属性可确保序列化属性。  
  
 若要将此主题中的代码作为单个清单进行复制，请参见 [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足够的权限，以便能够在安装 Visual Studio 的计算机上创建和运行 Windows 窗体应用程序项目。  
  
## 创建具有可序列化集合的控件  
 第一步是创建一个将可序列化集合作为属性的控件。  可以使用**“集合编辑器”**编辑此集合的内容，该编辑器可以从**“属性”**窗口访问。  
  
#### 创建具有可序列化集合的控件  
  
1.  创建一个名为 `SerializationDemoControlLib` 的 Windows 控件库项目。  有关更多信息，请参见 [Windows Control Library Template](http://msdn.microsoft.com/zh-cn/722f4e2d-1310-4ed5-8f33-593337ab66b4)。  
  
2.  将 `UserControl1` 重命名为 `SerializationDemoControl`。  有关更多信息，请参见 [How to: Rename Identifiers](http://msdn.microsoft.com/zh-cn/2430f732-2b70-4516-8cf6-a7bb71cc9724)。  
  
3.  在**“属性”**窗口中，将 <xref:System.Windows.Forms.Padding.All%2A?displayProperty=fullName> 属性的值设置为 `10`。  
  
4.  在 `SerializationDemoControl` 中放置一个 <xref:System.Windows.Forms.TextBox> 控件。  
  
5.  选择 <xref:System.Windows.Forms.TextBox> 控件。  在**“属性”**窗口中，设置下列属性。  
  
    |属性|更改为|  
    |--------|---------|  
    |**Multiline**|`true`|  
    |**Dock**|<xref:System.Windows.Forms.DockStyle>|  
    |**ScrollBars**|<xref:System.Windows.Forms.ScrollBars>|  
    |**ReadOnly**|`true`|  
  
6.  在**“代码编辑器”**中，在 `SerializationDemoControl` 内声明一个名为 `stringsValue` 的字符串数组字段。  
  
     [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#4)]
     [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#4)]
     [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#4)]  
  
7.  在 `SerializationDemoControl` 中定义 `Strings` 属性。  
  
> [!NOTE]
>  <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content> 值用于启用集合的序列化。  
  
 [!code-cpp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/cpp/form1.cpp#5)]
 [!code-csharp[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/CS/form1.cs#5)]
 [!code-vb[System.ComponentModel.DesignerSerializationVisibilityAttribute#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.DesignerSerializationVisibilityAttribute/VB/form1.vb#5)]  
  
1.  按 F5 生成该项目，然后在**“用户控件测试容器”**中运行控件。  
  
2.  在**“UserControl 测试容器”**的 <xref:System.Windows.Forms.PropertyGrid> 中查找 `Strings` 属性。  单击 `Strings` 属性，再单击省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮，以打开**“字符串集合编辑器”**。  
  
3.  在**“字符串集合编辑器”**中输入几个字符串。  在每个字符串的结尾按 Enter 键来分隔各字符串。  字符串输入完成后，单击**“确定”**。  
  
> [!NOTE]
>  您键入的字符串将出现在 `SerializationDemoControl` 的 <xref:System.Windows.Forms.TextBox> 中。  
  
## 序列化集合属性  
 若要测试控件的序列化行为，需要将其置于窗体中并使用**“集合编辑器”**更改集合的内容。  可以通过查看一个特殊的设计器文件来获知已序列化的集合的状态，**“Windows 窗体设计器”**会将代码发送至该文件中。  
  
#### 序列化集合  
  
1.  将 Windows 应用程序项目添加到解决方案。  将项目命名为 `SerializationDemoControlTest`。  
  
2.  在**“工具箱”**中找到名为**“SerializationDemoControlLib 组件”**的选项卡。  在此选项卡可找到 `SerializationDemoControl`。  有关更多信息，请参见[演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)。  
  
3.  将 `SerializationDemoControl` 置于窗体中。  
  
4.  在**“属性”**窗口中找到 `Strings` 属性。  单击 `Strings` 属性，再单击省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮，以打开**“字符串集合编辑器”**。  
  
5.  在**“字符串集合编辑器”**中键入几个字符串。  在每个字符串的结尾按 Enter 键来分隔各字符串。  字符串输入完成后，单击**“确定”**。  
  
> [!NOTE]
>  您键入的字符串将出现在 `SerializationDemoControl` 的 <xref:System.Windows.Forms.TextBox> 中。  
  
1.  在**“解决方案资源管理器”**中，单击**“显示所有文件”**按钮。  
  
2.  打开**“Form1”**节点。  此节点下面是一个名为**“Form1.Designer.cs”**或**“Form1.Designer.vb”**的文件。  **“Windows 窗体设计器”**将表示您的窗体及其子控件的设计时状态的代码发送至此文件。  在**“代码编辑器”**中打开此文件。  
  
3.  打开名为**“Windows 窗体设计器生成的代码”**的区域并找到标志为**“serializationDemoControl1”**的部分。  在此标签下是表示您的控件的已序列化状态的代码。  您在步骤 5 中键入的字符串会出现在对 `Strings` 属性的赋值中。  下面的代码示例演示类似于您在键入字符串“red”、“orange”和“yellow”后将看到的代码。  
  
4.  \[Visual Basic\]  
  
    ```  
    Me.serializationDemoControl1.Strings = New String() {"red", "orange", "yellow"}  
    ```  
  
5.  \[C\#\]  
  
    ```  
    this.serializationDemoControl1.Strings = new string[] {  
            "red",  
            "orange",  
            "yellow"};  
    ```  
  
6.  在**“代码编辑器”**中，将 `Strings` 属性上的 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute> 值更改为 <xref:System.ComponentModel.DesignerSerializationVisibility>。  
  
7.  \[Visual Basic\]  
  
    ```  
    <DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)> _  
    ```  
  
8.  \[C\#\]  
  
    ```  
    [DesignerSerializationVisibility(DesignerSerializationVisibility.Hidden)]  
    ```  
  
9. 重新生成解决方案并重复步骤 4 至 8。  
  
> [!NOTE]
>  在这种情况中，**“Windows 窗体设计器”**不向 `Strings` 属性发出赋值。  
  
## 后续步骤  
 了解了如何序列化标准类型的集合以后，可考虑将自定义控件更深入地集成到设计时环境中。  下列主题介绍如何增强自定义控件的设计时集成：  
  
-   [Design\-Time Architecture](../Topic/Design-Time%20Architecture.md)  
  
-   [Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)  
  
-   [Designer Serialization Overview](../Topic/Designer%20Serialization%20Overview.md)  
  
-   [演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)  
  
## 请参阅  
 <xref:System.ComponentModel.DesignerSerializationVisibilityAttribute>   
 [Designer Serialization Overview](../Topic/Designer%20Serialization%20Overview.md)   
 [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md)   
 [演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)