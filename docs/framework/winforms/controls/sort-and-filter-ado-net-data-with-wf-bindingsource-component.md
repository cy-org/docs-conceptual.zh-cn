---
title: "如何：使用 Windows 窗体 BindingSource 组件对 ADO.NET 数据进行排序和筛选 | Microsoft Docs"
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
  - "ADO.NET [Windows 窗体]"
  - "BindingSource 组件 [Windows 窗体], 对数据进行排序和筛选"
  - "数据 [Windows 窗体], 筛选"
  - "数据 [Windows 窗体], 排序"
  - "数据排序, ADO.NET"
  - "筛选 [Windows 窗体], ADO.NET"
  - "对数据进行排序"
ms.assetid: 6c206daf-d706-4602-9dbe-435343052063
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 Windows 窗体 BindingSource 组件对 ADO.NET 数据进行排序和筛选
您可以通过 <xref:System.Windows.Forms.BindingSource.Sort%2A> 和 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性公开 <xref:System.Windows.Forms.BindingSource> 控件的排序和筛选功能。  当基础数据源为 <xref:System.ComponentModel.IBindingList> 时可以应用简单排序，当数据源为 <xref:System.ComponentModel.IBindingListView> 时可以应用筛选和高级排序。  <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性需要标准 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 语法：在表示数据源中数据列名的字符串之后加上 `ASC` 或 `DESC`，以指示该列表应按升序排序，还是应按降序排序。  通过用逗号分隔符隔开每一列，可以设置高级排序或多列排序。  <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性获取字符串表达式。  
  
> [!NOTE]
>  将敏感信息（如密码）存储在连接字符串中可能会影响您的应用程序的安全性。  若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。  有关更多信息，请参见[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)。  
  
### 使用 BindingSource 筛选数据  
  
-   将 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性设置为所需的表达式。  
  
     在下面的代码示例中，表达式就是在列名之后加上该列所需的值。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#11)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#11)]  
  
### 使用 BindingSource 进行数据排序  
  
1.  将 <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性设置为后面要跟有 `ASC` 或 `DESC` 的所需列名称，以指示是按升序还是降序排序。  
  
2.  用逗号分隔多个列。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#12)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#12)]  
  
## 示例  
 下面的代码示例将 Northwind 示例数据库的 Customers 表中的数据加载到 <xref:System.Windows.Forms.DataGridView> 控件中，然后对显示的数据进行筛选和排序。  
  
 [!code-csharp[System.Windows.Forms.DataConnectorFilterAndSort#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorFilterAndSort#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorFilterAndSort/VB/form1.vb#1)]  
  
## 编译代码  
 若要运行本示例，请将代码粘贴到一个窗体中，让该窗体包含一个名为 `BindingSource1` 的 <xref:System.Windows.Forms.BindingSource> 及一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView>。  处理该窗体的 <xref:System.Windows.Forms.Form.Load> 事件，然后调用加载事件处理方法中的 `InitializeSortedFilteredBindingSource`。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingSource.Sort%2A>   
 <xref:System.Windows.Forms.BindingSource.Filter%2A>   
 [如何：安装示例数据库](../Topic/How%20to:%20Install%20Sample%20Databases.md)   
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)