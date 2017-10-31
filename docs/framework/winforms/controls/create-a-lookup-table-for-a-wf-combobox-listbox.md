---
title: "如何：为 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件创建查找表 | Microsoft Docs"
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
  - "CheckedListBox 控件 [Windows 窗体], 创建查找表"
  - "组合框, 查找表"
  - "ComboBox 控件 [Windows 窗体], 查找表"
  - "列表框, 查找表"
  - "ListBox 控件 [Windows 窗体], 创建查找表"
  - "ListBox 控件 [Windows 窗体], 查找表"
  - "查找表"
  - "查找表, 为控件创建"
ms.assetid: 4ce35f12-1f4e-4317-92d1-af8686a8cfaa
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：为 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件创建查找表
有时，在 Windows 窗体上以用户友好格式显示数据，但存储数据时使用对程序而言更有意义的格式会很有帮助。  例如，食品订单窗体可能按列表框中的名称显示菜单项。  但是，记录订单的数据表将包含代表该食品的唯一 ID 号。  下表显示如何存储和显示食品订单窗体数据的示例。  
  
### OrderDetailsTable  
  
|OrderID|ItemID|Quantity|  
|-------------|------------|--------------|  
|4085|12|1|  
|4086|13|3|  
  
### ItemTable  
  
|ID|名称|  
|--------|--------|  
|12|Potato|  
|13|Chicken|  
  
 在此方案中，其中一张表 \(OrderDetailsTable\) 存储要显示和保存的实际信息。  但为了节省空间，它采用一种很隐秘的方式。  另一张表 \(OrdersTable\) 仅包含关于哪个 ID 号等同于哪个食品名称的表面信息，而不包含实际食品订单的信息。  
  
 ItemTable 通过三个属性连接到 <xref:System.Windows.Forms.ComboBox><xref:System.Windows.Forms.ListBox> 或 <xref:System.Windows.Forms.CheckedListBox> 控件。   `DataSource`  属性包含此表的名称。   `DisplayMember` 属性包含该表中你希望在控件中显示的数据列（食品名称）。   `ValueMember`  属性包含该表中具有存储信息的数据列（ID 号）。  
  
 OrderDetailsTable 通过其绑定集合连接到控件，其绑定集合可通过 <xref:System.Windows.Forms.Control.DataBindings%2A> 属性访问。  将绑定对象添加到集合时，请将控件属性连接到数据源 \(OrderDetailsTable\) 中的特定数据成员（ID 号）。  在控件中进行选择时，窗体输入将保存到此表。  
  
### 创建查找表的步骤  
  
1.  向窗体添加 <xref:System.Windows.Forms.ComboBox><xref:System.Windows.Forms.ListBox> 或 <xref:System.Windows.Forms.CheckedListBox> 控件。  
  
2.  连接到数据源。  
  
3.  在两张表之间建立数据关系。  参阅 [介绍 DataRelation 对象](../Topic/Introduction%20to%20DataRelation%20Objects.md)。  
  
4.  设置以下属性：  以下属性可在代码或设计器中设置。  
  
    |属性|设置|  
    |--------|--------|  
    |<xref:System.Windows.Forms.ListControl.DataSource%2A>|包含有关哪个 ID 号等同于哪一项的信息的表。  在前面的方案中，即为  `ItemTable`。|  
    |<xref:System.Windows.Forms.ListControl.DisplayMember%2A>|你想要在控件中显示的源数据表的列。  在前面的方案中，即为 `"Name"` （若要在代码中设置，请使用双引号）。|  
    |<xref:System.Windows.Forms.ListControl.ValueMember%2A>|包含所存储信息的源数据表的列。  在前面的方案中，即为 `"ID"` （若要在代码中设置，请使用双引号）。|  
  
5.  在过程中，调用 <xref:System.Windows.Forms.ControlBindingsCollection> 类的 <xref:System.Windows.Forms.ControlBindingsCollection.Add%2A> 方法，以将控件的 <xref:System.Windows.Forms.ListControl.SelectedValue%2A> 属性绑定到记录窗体输入的表。  你也可以在设计器而非代码中实现此操作，方法是在“属性”窗口中访问控件的 <xref:System.Windows.Forms.Control.DataBindings%2A> 属性。  在前面的方案中，即为 `OrderDetailsTable`，而列则为 `"ItemID"`。  
  
    ```vb  
    ListBox1.DataBindings.Add("SelectedValue", OrderDetailsTable, "ItemID")  
  
    ```  
  
    ```csharp  
    listBox1.DataBindings.Add("SelectedValue", OrderDetailsTable, "ItemID");  
  
    ```  
  
## 请参阅  
 [数据绑定和 Windows 窗体](../../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [ListBox 控件概述](../../../../docs/framework/winforms/controls/listbox-control-overview-windows-forms.md)   
 [ComboBox 控件概述](../../../../docs/framework/winforms/controls/combobox-control-overview-windows-forms.md)   
 [CheckedListBox 控件概述](../../../../docs/framework/winforms/controls/checkedlistbox-control-overview-windows-forms.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)