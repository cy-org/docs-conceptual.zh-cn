---
title: "演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 管理大型数据集"
  - "DataGridView 控件 [Windows 窗体], 大型数据集"
  - "DataGridView 控件 [Windows 窗体], 虚拟模式"
  - "虚拟模式, 演练"
  - "演练 [Windows 窗体], DataGridView 控件"
ms.assetid: 74eb5276-5ab8-4ce0-8005-dae751d85f7c
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式
如果要在 <xref:System.Windows.Forms.DataGridView> 控件中显示非常大量的表格数据，可以将 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性设置为 `true`，并显式管理控件与其数据存储区的交互。  这样，您便可以在这种情况下精细调整该控件的性能。  
  
 <xref:System.Windows.Forms.DataGridView> 控件提供若干事件，您可以通过处理这些事件来与自定义数据存储区进行交互。  本演练引导您完成实现这些事件处理程序的过程。  为便于说明，本主题中的代码示例使用一个非常简单的数据源。  在生产设置中，通常仅将需要显示的行加载到缓存中，并处理 <xref:System.Windows.Forms.DataGridView> 事件以便与缓存进行交互和更新缓存。  有关更多信息，请参见 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
  
 若要以单个列表的形式复制本主题中的代码，请参见 [如何：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)。  
  
## 创建窗体  
  
#### 实现虚拟模式  
  
1.  创建一个从 <xref:System.Windows.Forms.Form> 派生并包含 <xref:System.Windows.Forms.DataGridView> 控件的类。  
  
     下面的代码包含一些简单的初始化操作。  它将声明一些将在后续步骤中使用的变量，提供 `Main` 方法，并在类的构造函数中提供一个简单的窗体布局。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#001)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#001)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#001](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#001)]  
    [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#002)]
    [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#002)]
    [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#002](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#002)]  
  
2.  为窗体的 <xref:System.Windows.Forms.Form.Load> 事件实现一个处理程序，该处理程序初始化 <xref:System.Windows.Forms.DataGridView> 控件并用示例值填充数据存储区。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#110)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#110)]  
  
3.  为 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 事件实现一个处理程序，从数据存储区或当前正在编辑的 `Customer` 对象中检索请求的单元格值。  
  
     只要 <xref:System.Windows.Forms.DataGridView> 控件需要绘制单元格，就会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#120)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#120)]  
  
4.  为 <xref:System.Windows.Forms.DataGridView.CellValuePushed> 事件实现一个处理程序，将编辑后的单元格值存储在代表已编辑的行的 `Customer` 对象中。  只要用户提交对单元格值的更改，就会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#130)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#130)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#130)]  
  
5.  为 <xref:System.Windows.Forms.DataGridView.NewRowNeeded> 事件实现一个处理程序，创建一个代表新建行的新 `Customer` 对象。  
  
     只要用户进入新的记录行，就会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#140)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#140)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#140)]  
  
6.  为 <xref:System.Windows.Forms.DataGridView.RowValidated> 事件实现一个处理程序，将新的或修改后的行保存到数据存储区中。  
  
     只要用户更改当前行，就会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#150)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#150)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#150)]  
  
7.  为 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 事件实现一个处理程序，指示当用户通过在编辑模式下按 Esc 两次或在非编辑模式下按 Esc 一次来指示行恢复时，是否发生 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 事件。  
  
     默认情况下，除非 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 事件处理程序中的 <xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=fullName> 属性设置为 `true`，否则，只要当前行中有任何单元格被修改，就会在恢复行时发生 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 事件。  如果提交范围是在运行时确定的，则此事件非常有用。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#160)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#160)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#160)]  
  
8.  为 <xref:System.Windows.Forms.DataGridView.CancelRowEdit> 事件实现一个处理程序，丢弃表示当前行的 `Customer` 对象的值。  
  
     当用户通过在编辑模式下按 Esc 两次或在非编辑模式下按 Esc 一次来指示行恢复时，会发生此事件。  如果当前行中没有任何单元格被修改，或者，<xref:System.Windows.Forms.QuestionEventArgs.Response%2A?displayProperty=fullName> 属性的值已在 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded> 事件处理程序中设置为 `false`，则不会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#170)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#170)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#170)]  
  
9. 为 <xref:System.Windows.Forms.DataGridView.UserDeletingRow> 事件实现一个处理程序，该事件将现有的 `Customer` 对象从数据存储区中删除，或丢弃表示新建行的未保存的 `Customer` 对象。  
  
     只要用户通过单击行标题再按 Delete 键来删除行，就会发生此事件。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#180)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#180)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#180)]  
  
10. 实现一个简单的 `Customers` 类来表示此代码示例使用的数据项。  
  
     [!code-cpp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CPP/virtualmode.cpp#200)]
     [!code-csharp[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/CS/virtualmode.cs#200)]
     [!code-vb[System.Windows.Forms.DataGridView.VirtualMode#200](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.VirtualMode/VB/virtualmode.vb#200)]  
  
## 测试应用程序  
 现在可以测试窗体，以确保其行为与预期相同。  
  
#### 测试窗体  
  
-   编译并运行应用程序。  
  
     您将看到填入了三个客户记录的 <xref:System.Windows.Forms.DataGridView> 控件。  您可以修改一行中的多个单元格的值，然后在编辑模式下按 Esc 两次或在非编辑模式下按 Esc 一次，将整行恢复为原始值。  当在控件中修改、添加或删除行时，数据存储区中的 `Customer` 对象也会相应地修改、添加或删除。  
  
## 后续步骤  
 此应用程序使您可以基本了解在 <xref:System.Windows.Forms.DataGridView> 控件中实现虚拟模式所必须处理的事件。  可以通过许多方法来改进这个简单的应用程序：  
  
-   实现用于缓存来自外部数据库的值的数据存储区。  此缓存应根据需要检索和丢弃值，以便仅仅包含必须显示的内容，从而确保只占用客户端计算机上的少量内存。  
  
-   根据实际要求精细调整数据存储区的性能。  例如，您可能要使用更大规模的缓存并将数据库查询的数目控制在最少，从而补偿慢速网络连接，而不是根据客户端计算机的内存限制进行调整。  
  
 有关缓存来自外部数据库的值的更多信息，请参见 [如何：在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 <xref:System.Windows.Forms.DataGridView.CellValueNeeded>   
 <xref:System.Windows.Forms.DataGridView.CellValuePushed>   
 <xref:System.Windows.Forms.DataGridView.NewRowNeeded>   
 <xref:System.Windows.Forms.DataGridView.RowValidated>   
 <xref:System.Windows.Forms.DataGridView.RowDirtyStateNeeded>   
 <xref:System.Windows.Forms.DataGridView.CancelRowEdit>   
 <xref:System.Windows.Forms.DataGridView.UserDeletingRow>   
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)   
 [如何：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/how-to-implement-virtual-mode-in-the-windows-forms-datagridview-control.md)