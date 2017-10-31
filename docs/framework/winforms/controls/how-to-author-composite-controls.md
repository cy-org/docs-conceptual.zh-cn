---
title: "如何：创作复合控件 | Microsoft Docs"
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
  - "复合控件, 创建"
  - "用户控件 [Windows 窗体], 创建"
  - "用户控件 [Windows 窗体], 继承来源"
  - "UserControl 类, 创建复合控件"
ms.assetid: 79c9cf05-5ab6-4a18-886d-88a64748b098
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：创作复合控件
复合控件有多种使用方式。  可以将它们作为 Windows 桌面应用程序项目的一部分创作，且只在该项目的窗体上使用它们。  您也可以在 Windows Control Library 项目中创作它们，将该项目编译成一个程序集，在其他项目中使用这些控件。  您甚至可以继承它们，并针对特殊目的使用可视化继承快速自定义它们。  
  
> [!NOTE]
>  如果需要创作在 Web 窗体上使用的复合控件，请参见[Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md)。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创作复合控件  
  
1.  打开名为 `DemoControlHost` 的**“Windows 应用程序”**新项目。  
  
2.  在**“项目”**菜单上，单击**“添加用户控件”**。  
  
3.  在**“添加新项”**对话框中，将类文件（.vb 或 .cs 文件）命名为您希望复合控件所具有的名字。  
  
4.  单击**“添加”**按钮创建复合控件的类文件。  
  
5.  将控件从**“工具箱”**添加到复合控件表面。  
  
6.  将代码置于事件过程中，处理由复合控件或其构成控件所引发的事件。  
  
7.  关闭复合控件的设计器，在看到提示时保存文件。  
  
8.  在**“生成”**菜单上，单击**“生成解决方案”**。  
  
     为使用户控件出现在**“工具箱”**中，必须生成该项目。  
  
9. 使用**“工具箱”**的**“DemoControlHost”**选项卡将控件实例添加到 `Form1`。  
  
### 创作控件类库  
  
1.  打开新的**“Windows 控件库”**项目。  
  
     默认情况下，该项目包含一个复合控件。  
  
2.  按上述步骤添加控件和代码。  
  
3.  选择不希望继承类更改的控件，并将这个控件的**“Modifiers”**属性设置为**“Private”**。  
  
4.  生成 DLL。  
  
### 从控件类库中的复合控件继承  
  
1.  在**“文件”**菜单上指向**“添加”**，然后选择**“新建项目”**，以便向解决方案中添加新的**“Windows 应用程序”**项目。  
  
2.  在**“解决方案资源管理器”**中，右击该新项目的**“引用”**文件夹并选择**“添加引用”**以打开**“添加引用”**对话框。  
  
3.  选择**“项目”**选项卡并双击您的控件库项目。  
  
4.  在**“生成”**菜单上，单击**“生成解决方案”**。  
  
5.  在**“解决方案资源管理器”**中，右击控件库项目并从快捷菜单中选择**“添加新项”**。  
  
6.  从**“添加新项”**对话框中选择**“继承的用户控件”**模板。  
  
7.  在**“继承选择器”**对话框中双击要继承的控件。  
  
     一个新的控件添加到项目中。  
  
8.  打开新控件的可视化设计器并添加其他构成控件。  
  
     您可以看到从 DLL 中的复合控件继承来的构成控件，还可以更改**“Modifiers”**属性为**“Public”**的控件的属性。  但不能更改**“Modifiers”**属性为**“Private”**的控件的属性。  
  
## 请参阅  
 [演练：使用 Visual Basic 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [演练：使用 Visual C\# 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)   
 [演练：使用 Visual Basic 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [演练：使用 Visual C\# 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)   
 [控件类型建议](../../../../docs/framework/winforms/controls/control-type-recommendations.md)   
 [如何：创作 Windows 窗体的控件](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)