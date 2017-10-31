---
title: "如何：使用设计器将 Windows 窗体控件绑定到类型 | Microsoft Docs"
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
  - "BindingSource 组件 [Windows 窗体], 绑定到类型"
  - "控件 [Windows 窗体], 绑定到类型"
  - "类型 [Windows 窗体], 将控件绑定到"
ms.assetid: 5ab984b5-c2d0-4638-a572-1c84013e8746
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用设计器将 Windows 窗体控件绑定到类型
在生成与数据交互的控件时，有时需要将控件绑定到类型，而不是对象。  您通常需要在设计时将控件绑定到类型，数据在设计时有可能不可用，但您仍希望数据绑定控件显示来自类型公共接口的数据。  下面的过程演示如何创建绑定到类型的新 <xref:System.Windows.Forms.BindingSource>，接着演示如何将类型的属性之一绑定到 <xref:System.Windows.Forms.TextBox> 的 <xref:System.Windows.Forms.TextBox.Text%2A> 属性。  
  
### 将 BindingSource 绑定到类型  
  
1.  创建 Windows 窗体项目。  
  
     有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在**“设计”**视图中，将一个 <xref:System.Windows.Forms.BindingSource> 组件拖动到窗体上。  
  
3.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.BindingSource.DataSource%2A> 属性的箭头。  
  
4.  在**“数据源 UI 类型编辑器”**中，单击**“添加项目数据源”**。  
  
5.  在**“选择数据源类型”**页上，选择**“对象”**，然后单击**“下一步”**。  
  
6.  选择要绑定到的类型：  
  
    -   如果希望绑定到的类型在当前项目中，或者包含该类型的程序集已经作为引用添加，请展开节点以找到所需的类型，然后选择该类型。  
  
         \- 或 \-  
  
    -   如果希望绑定到的类型在另外一个程序集中，不在当前的引用列表中，请单击**“添加引用”**，然后单击**“项目”**选项卡。  选择包含所需业务对象的项目并单击**“确定”**。  此项目将显示在程序集列表中，因此您可以展开节点以找到所需的类型，然后选择该类型。  
  
        > [!NOTE]
        >  如果希望绑定到框架或 Microsoft 程序集中的类型，请清除**“隐藏以 Microsoft 或 System 开头的程序集”**复选框。  
  
7.  单击**“下一步”**，然后单击**“完成”**。  
  
### 将控件绑定到 BindingSource  
  
1.  将一个 <xref:System.Windows.Forms.TextBox> 添加到窗体中。  
  
2.  在**“属性”**窗口中，展开**“\(DataBindings\)”**节点。  
  
3.  单击 <xref:System.Windows.Forms.TextBox.Text%2A> 属性旁边的箭头。  
  
4.  在**“数据源 UI 类型编辑器”**中，展开之前添加的 <xref:System.Windows.Forms.BindingSource> 的节点，并选择希望绑定到 <xref:System.Windows.Forms.TextBox> 的 <xref:System.Windows.Forms.TextBox.Text%2A> 属性的绑定类型的属性。  
  
## 请参阅  
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)   
 [在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)