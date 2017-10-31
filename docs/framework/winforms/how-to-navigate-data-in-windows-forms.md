---
title: "如何：在 Windows 窗体中导航数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "CurrencyManager 类, 导航 Windows 窗体数据"
  - "光标, 数据源"
  - "数据 [Windows 窗体], 导航"
  - "数据源, Windows 窗体"
  - "Windows 窗体, 导航"
ms.assetid: 97360f7b-b181-4084-966a-4c62518f735b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 Windows 窗体中导航数据
在 Windows 应用程序中，在数据源中的记录中进行导航的最简单方式是将 <xref:System.Windows.Forms.BindingSource> 组件绑定到数据源，然后将控件绑定到 <xref:System.Windows.Forms.BindingSource>。  然后，可以对 <xref:System.Windows.Forms.BindingSource> 使用内置的导航方法，如 <xref:System.Windows.Forms.BindingSource.MoveNext%2A>、<xref:System.Windows.Forms.BindingSource.MoveLast%2A>、<xref:System.Windows.Forms.BindingSource.MovePrevious%2A> 和 <xref:System.Windows.Forms.BindingSource.MoveFirst%2A>。  使用这些方法将相应地调整 <xref:System.Windows.Forms.BindingSource> 的 <xref:System.Windows.Forms.BindingSource.Position%2A> 和 <xref:System.Windows.Forms.BindingSource.Current%2A> 属性。  还可以通过设置 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性来查找项并将它设置为当前项。  
  
### 递增在数据源中的位置  
  
1.  将绑定数据的 <xref:System.Windows.Forms.BindingSource> 的 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性设置为要转到的记录位置。  下面的示例阐释在单击 `nextButton` 时，使用 <xref:System.Windows.Forms.BindingSource> 的 <xref:System.Windows.Forms.BindingSource.MoveNext%2A> 方法递增 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性。  <xref:System.Windows.Forms.BindingSource> 与数据集 `Northwind` 的 `Customers` 表相关联。  
  
    > [!NOTE]
    >  将 <xref:System.Windows.Forms.BindingSource.Position%2A> 属性设置为第一条或最后一条记录以外的值不会导致错误，因为 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 将不允许将位置设置为列表范围之外的值。  如果在应用程序中知道是否已越过第一条或最后一条记录非常重要，可包括测试是否将超过数据元素计数的逻辑。  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.NavigatingData#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#4)]  
  
### 检查是否已越过结尾或开始位置  
  
1.  为 <xref:System.Windows.Forms.BindingSource.PositionChanged> 事件创建一个事件处理程序。  在该处理程序中，可以测试所建议的位置值是否已超过实际数据元素计数。  
  
     下面的示例阐释可以如何测试是否已到达了最后一个数据元素。  在该示例中，如果到了最后一个元素，则窗体上的**“下一页”**按钮处于禁用状态。  
  
    > [!NOTE]
    >  请注意，如果在代码中对导航的列表进行了更改，则应重新启用**“下一页”**按钮，以便用户可以浏览新列表的整个长度。  另外请注意，需要将要使用的特定 <xref:System.Windows.Forms.BindingSource> 的上述 <xref:System.Windows.Forms.BindingSource.PositionChanged> 事件与其事件处理方法相关联。  下面是处理 <xref:System.Windows.Forms.BindingSource.PositionChanged> 事件的一个方法示例：  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.NavigatingData#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#3)]  
  
### 查找项并将其设置为当前项  
  
1.  查找要设置为当前项的记录。  如果数据源实现 <xref:System.ComponentModel.IBindingList>，则此查找操作可以通过使用 <xref:System.Windows.Forms.BindingSource> 的 <xref:System.Windows.Forms.BindingSource.Find%2A> 方法来完成。  实现 <xref:System.ComponentModel.IBindingList> 的数据源的一些示例有 <xref:System.ComponentModel.BindingList%601> 和 <xref:System.Data.DataView>。  
  
     [!code-csharp[System.Windows.Forms.NavigatingData#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.NavigatingData#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.NavigatingData/VB/Form1.vb#2)]  
  
## 请参阅  
 [Windows 窗体支持的数据源](../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)   
 [Windows 窗体数据绑定中的更改通知](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)