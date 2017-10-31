---
title: "如何：使用 Modifiers 和 GenerateMember 属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "Designer_GenerateMember"
  - "Designer_Modifiers"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "基窗体"
  - "窗体继承"
  - "GenerateMember 属性"
  - "继承, 窗体"
  - "继承的窗体"
  - "继承的窗体, Windows 窗体"
  - "Modifiers 属性"
  - "Windows 窗体, 继承"
ms.assetid: 3381a5e4-e1a3-44e2-a765-a0b758937b85
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用 Modifiers 和 GenerateMember 属性
将组件放置在 Windows 窗体上时，设计环境提供两个属性：`GenerateMember` 和 `Modifiers`。  `GenerateMember` 属性指定 Windows 窗体设计器何时为组件生成成员变量。  `Modifiers` 属性是指定给该成员变量的访问修饰符。  如果 `GenerateMember` 属性的值为 `false`，则 `Modifiers` 属性没有效果。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 指定组件是否是窗体成员  
  
1.  在 Windows 窗体设计器中打开窗体。  
  
2.  打开**“工具箱”**，将三个 <xref:System.Windows.Forms.Button> 控件放置在窗体上。  
  
3.  根据下表为每个 <xref:System.Windows.Forms.Button> 控件设置 `GenerateMember` 和 `Modifiers` 属性。  
  
    |按钮名称|GenerateMember 值|Modifiers 值|  
    |----------|----------------------|-----------------|  
    |`button1`|`true`|`private`|  
    |`button2`|`true`|`protected`|  
    |`button3`|`false`|无更改|  
  
4.  生成解决方案。  
  
5.  在**“解决方案资源管理器”**中，单击**“显示所有文件”**按钮。  
  
6.  打开**“Form1”**节点，并在**“代码编辑器”**中打开**“Form1.Designer.vb”**或**“Form1.Designer.cs”**文件。  此文件包含 Windows 窗体设计器发出的代码。  
  
7.  找到三个按钮的声明。  下面的代码示例显示了由 `GenerateMember` 和 `Modifiers` 属性指定的差异。  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.GenerateMember#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#3)]  
  
     [!code-csharp[System.Windows.Forms.GenerateMember#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.GenerateMember#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.GenerateMember/VB/Form1.vb#2)]  
  
> [!NOTE]
>  默认情况下，Windows 窗体设计器将 `private`（在 Visual Basic 中为 `Friend`）修饰符指定给容器控件（如 <xref:System.Windows.Forms.Panel>）。  如果基 <xref:System.Windows.Forms.UserControl> 或 <xref:System.Windows.Forms.Form> 具有容器控件，则将不会接受继承的控件和窗体中的新子级。  此解决方案用于将基容器控件的修饰符更改为 `protected` 或 `public`。  
  
## 请参阅  
 <xref:System.Windows.Forms.Button>   
 [Windows 窗体可视化继承](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)   
 [演练：演示可视化继承](../../../../docs/framework/winforms/advanced/walkthrough-demonstrating-visual-inheritance.md)   
 [如何：继承 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)