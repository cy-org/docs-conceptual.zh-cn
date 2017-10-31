---
title: "如何：访问绑定到 Windows 窗体 DataGridView 行的对象 | Microsoft Docs"
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
  - "数据网格, 访问绑定对象"
  - "DataGridView 控件 [Windows 窗体], 访问绑定到行的对象"
  - "对象绑定, 访问绑定对象"
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 如何：访问绑定到 Windows 窗体 DataGridView 行的对象
有时，显示业务对象集合中存储的信息表很有用。  将 <xref:System.Windows.Forms.DataGridView> 控件绑定到此类集合时，每个公共属性都将在它自己的列中显示，除非该属性已用 <xref:System.ComponentModel.BrowsableAttribute> 标记为不可浏览。  例如，`Customer` 对象的集合将具有“姓名”和“地址”等列。  
  
 如果这些对象包含你希望访问的附加信息和代码，则可以通过行对象来进行访问。  在下面的代码示例中，用户可以选择多行并单击一个按钮将发票发送给每个对应客户。  
  
### 访问行绑定对象  
  
-   使用 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## 示例  
 完整的代码示例包括一个简单的 `Customer` 实现，并将 <xref:System.Windows.Forms.DataGridView> 绑定到一个包含几个 `Customer` 对象的 <xref:System.Collections.ArrayList>。  因为在 <xref:System.Windows.Forms.Form.Load?displayProperty=fullName> 事件处理程序之外无法访问客户集合，所以 <xref:System.Windows.Forms.Button?displayProperty=fullName> 的 <xref:System.Windows.Forms.Control.Click> 事件处理程序必须通过行访问 `Customer` 对象。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 的命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewRow>   
 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=fullName>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [如何：将对象绑定到 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/how-to-bind-objects-to-windows-forms-datagridview-controls.md)