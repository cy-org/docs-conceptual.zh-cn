---
title: "Windows 窗体 DataGridView 控件中的默认功能 | Microsoft Docs"
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
  - "数据网格, DataGridView 控件中的默认功能"
  - "DataGridView 控件 [Windows 窗体], 默认功能"
ms.assetid: 4405f697-cad1-4839-9bcd-8ddb09d9f00e
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Windows 窗体 DataGridView 控件中的默认功能
Windows 窗体控件 <xref:System.Windows.Forms.DataGridView> 为用户提供大量的默认功能。  
  
## 默认功能  
 默认情况下，<xref:System.Windows.Forms.DataGridView> 控件具有下列特点：  
  
-   自动显示垂直滚动表时保持可见的列标头和行标头。  
  
-   拥有行标头，其中包含当前行的选中指示符。  
  
-   在第一个单元格中拥有选择矩形。  
  
-   拥有列，当用户双击列分隔符时可自动调整大小。  
  
-   通过应用程序的 `Main` 方法调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 方法时，自动支持 Windows XP 和 Windows Server 2003 系列中的视觉样式。  
  
 此外，默认情况下可以编辑 <xref:System.Windows.Forms.DataGridView> 控件的内容：  
  
-   用户在某个单元格中双击或按 F2 时，此控件将自动使该单元格自动进入编辑模式，并在用户键入时自动更新单元格的内容。  
  
-   如果用户滚动至网格的结尾，将会看到用于添加新记录的行。  用户单击此行时，会向 <xref:System.Windows.Forms.DataGridView> 控件添加使用默认值的新行。  用户按 Esc 时，此新行将消失。  
  
-   如果用户单击行标头，将会选中整行。  
  
 通过设置 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 属性将其绑定到数据源时，该控件可以：  
  
-   将数据源列的名称自动用作列标头文本。  
  
-   用数据源的内容进行填充。  <xref:System.Windows.Forms.DataGridView> 列是为数据源中的每个列自动创建的。  
  
-   为表中的每个可见行创建一行。  
  
-   用户单击列标头时，将根据基础数据自动对行进行排序。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)