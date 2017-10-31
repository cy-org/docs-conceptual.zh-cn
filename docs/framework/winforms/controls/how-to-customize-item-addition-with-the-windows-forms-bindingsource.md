---
title: "如何：使用 Windows 窗体 BindingSource 自定义项添加 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 创建新项"
  - "BindingSource 组件 [Windows 窗体], 自定义项添加"
  - "示例 [Windows 窗体], BindingSource 组件"
  - "BindingSource 组件 [Windows 窗体], 示例"
ms.assetid: 1aae11fc-6fb2-4cb9-b3d0-e0638fe77ef0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用 Windows 窗体 BindingSource 自定义项添加
使用 <xref:System.Windows.Forms.BindingSource> 组件将 Windows 窗体控件绑定到数据源时，可能会发现需要自定义新项目的创建。<xref:System.Windows.Forms.BindingSource> 组件通过提供 <xref:System.Windows.Forms.BindingSource.AddingNew> 事件（通常在绑定的控件需要创建新项目时引发）使这种情况简单明了。 事件处理程序可以提供所需的任何自定义行为（例如，在 Web 服务上调用方法或从类工厂中获取新对象）。  
  
> [!NOTE]
>  通过处理 <xref:System.Windows.Forms.BindingSource.AddingNew> 事件添加项时，无法取消该添加。  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件将 <xref:System.Windows.Forms.DataGridView> 控件绑定到类工厂。 用户单击 <xref:System.Windows.Forms.DataGridView> 控件的新行时，引发 <xref:System.Windows.Forms.BindingSource.AddingNew> 事件。 事件处理程序创建一个新 `DemoCustomer` 对象，该对象被分配至 <xref:System.ComponentModel.AddingNewEventArgs.NewObject%2A?displayProperty=fullName> 属性。 这将导致新 `DemoCustomer` 对象被添加到 <xref:System.Windows.Forms.BindingSource> 组件的列表中和显示在 <xref:System.Windows.Forms.DataGridView> 控件的新行中。  
  
 [!code-cpp[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnector.AddingNew#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnector.AddingNew/VB/form1.vb#1)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)