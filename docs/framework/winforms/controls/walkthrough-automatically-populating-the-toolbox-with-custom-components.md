---
title: "演练：使用自定义组件自动填充工具箱 | Microsoft Docs"
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
  - "自定义组件, 添加到工具箱"
  - "IToolboxService 接口"
  - "工具箱 [Windows 窗体], 填充"
ms.assetid: 2fa1e3e8-6b9f-42b2-97c0-2be57444dba4
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 演练：使用自定义组件自动填充工具箱
如果组件是由当前打开的解决方案中的项目定义的，那么无需任何操作，这些组件就会自动出现在**“工具箱”**中。  还可以通过使用 [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/bd07835f-18a8-433e-bccc-7141f65263bb) 用自定义组件手动填充**“工具箱”**，但**“工具箱”**在考虑解决方案的生成输出结果中的各项时需具有以下全部特点：  
  
-   实现 <xref:System.ComponentModel.IComponent>；  
  
-   没有将 <xref:System.ComponentModel.ToolboxItemAttribute> 设置为 `false`；  
  
-   没有将 <xref:System.ComponentModel.DesignTimeVisibleAttribute> 设置为 `false`。  
  
> [!NOTE]
>  **“工具箱”**不会遵循引用链，因此它将不显示并非由解决方案中的项目生成的各项。  
  
 本演练演示在构建了自定义组件之后，它如何自动出现在**“工具箱”**中。  本演练涉及以下任务：  
  
-   创建 Windows 窗体项目。  
  
-   创建自定义组件。  
  
-   创建自定义组件的实例。  
  
-   卸载和重新加载自定义组件。  
  
 完成后，将会看到**“工具箱”**中填充了所创建的组件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建一个名为 `ToolboxExample` 的基于 Windows 的应用程序项目。  
  
     有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  向项目添加新的组件。  将其命名为 `DemoComponent`。  
  
     有关更多信息，请参见[NIB:How to: Add New Project Items](http://msdn.microsoft.com/zh-cn/63d3e16b-de6e-4bb5-a0e3-ecec762201ce)。  
  
3.  生成项目。  
  
4.  在**“工具”**菜单上单击**“选项”**项。  单击**“Windows 窗体设计器”**项下面的**“常规”**，并确保**“AutoToolboxPopulate”**选项设置为**“True”**。  
  
## 创建自定义组件的实例  
 下一步是窗体上创建自定义组件的实例。  因为**“工具箱”**会自动解释新组件，所以这和创建任何其他组件或控件一样简单。  
  
#### 创建自定义组件的实例  
  
1.  在**“窗体设计器”**中打开该项目的窗体。  
  
2.  在**“工具箱”**中，单击名为**“ToolboxExample 组件”**的新选项卡。  
  
     单击该选项卡后将会看到**“DemoComponent”**。  
  
    > [!NOTE]
    >  由于性能的原因，**“工具箱”**的自动填充区域中的组件不显示自定义位图，并且不支持 <xref:System.Drawing.ToolboxBitmapAttribute>。  若要在**“工具箱”**中显示自定义组件的图标，请使用**“选择工具箱项”**对话框加载您的组件。  
  
3.  将组件拖到窗体上。  
  
     这样将创建该组件的一个实例，并将其添加到**“组件栏”**。  
  
## 卸载并重新加载自定义组件  
 **“工具箱”**考虑每个加载项目中的组件，当卸载项目时，它将移除对该项目组件的引用。  
  
#### 试验卸载和重新加载组件对工具箱的影响  
  
1.  从解决方案卸载该项目。  
  
     有关卸载项目的更多信息，请参见 [NIB:How to: Unload and Reload Projects](http://msdn.microsoft.com/zh-cn/abc0155b-8fcb-4ffc-95b6-698518a7100b)。  如果提示保存，选择**“是”**。  
  
2.  将新的**“Windows 应用程序”**项目添加到解决方案。  在**“设计器”**中打开窗体。  
  
     前个项目中的**“ToolboxExample 组件”**选项卡现在不见了。  
  
3.  重新加载 `ToolboxExample` 项目。  
  
     现在重新出现**“ToolboxExample 组件”**选项卡。  
  
## 后续步骤  
 本演练演示了**“工具箱”**会考虑项目的组件，但**“工具箱”**同时也会考虑控件。  可以通过添加和移除解决方案中的控件项目来试验自定义控件。  
  
## 请参阅  
 [General, Windows Forms Designer, Options Dialog Box](http://msdn.microsoft.com/zh-cn/8dd170af-72f0-4212-b04b-034ceee92834)   
 [How to: Manipulate Toolbox Tabs](http://msdn.microsoft.com/zh-cn/21285050-cadd-455a-b1f5-a2289a89c4db)   
 [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/bd07835f-18a8-433e-bccc-7141f65263bb)   
 [将控件放在 Windows 窗体上](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)