---
title: "如何：确保子表中的选定行保持在正确的位置 | Microsoft Docs"
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
  - "缓存 [.NET Framework], 子表位置"
  - "子表位置"
  - "子表行选择"
  - "当前子表位置"
  - "数据绑定 [.NET Framework], 行选择"
  - "主/详细信息视图 [Windows 窗体]"
  - "主-详细信息视图"
  - "父/子视图 [Windows 窗体]"
  - "重置子表位置"
  - "行位置 [Windows 窗体]"
ms.assetid: c5fa2562-43a4-46fa-a604-52d8526a87bd
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：确保子表中的选定行保持在正确的位置
通常当在 Windows 窗体中使用数据绑定时，将显示称为父\/子视图或母版\/详细视图中的数据。  这是指一个数据绑定方案，其中来自同一源的数据将显示在两个控件中。  更改一个控件中的选定内容会导致在第二个控件中显示的数据变动。  例如，第一个控件可能会包含一个客户列表，而第二个控件则可能包含与第一个控件中选定客户相关的订单列表。  
  
 开始使用.NET Framework 2.0 版本，当在父\/子视图中显示数据时，可能需要采取额外步骤来确保子表中当前所选的行不会重置为表的第一行。  为了执行此操作，必须缓存子表位置并在父表发生更改后将其重置。  父表某一行中的字段第一次更改时通常会发生子表重置。  
  
### 若要缓存当前子表位置  
  
1.  则声明一个整数变量，以存储子列表位置，并声明一个布尔变量，以存储是否缓存子表位置。  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#4](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#4](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#4)]  
  
2.  为绑定的 <xref:System.Windows.Forms.CurrencyManager> 处理 <xref:System.Windows.Forms.CurrencyManager.ListChanged> 事件并检查 <xref:System.ComponentModel.ListChangedType> 的 <xref:System.ComponentModel.ListChangedType>。  
  
3.  检查 <xref:System.Windows.Forms.CurrencyManager> 的当前位置。  如果它大于列表中第一个条目（通常为 0），则将其保存到一个变量。  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#2](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#2](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#2)]  
  
4.  为父货币管理器处理父列表的 <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged> 事件。  在处理程序中，设置布尔值，以指示其不是一个缓存方案。  如果发生了 <xref:System.Windows.Forms.BindingManagerBase.CurrentChanged>，则对父对象的更改是列表位置的更改，而不是项目值的更改。  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#5)]  
  
### 若要重置子表位置  
  
1.  为子绑定的 <xref:System.Windows.Forms.CurrencyManager>处理 <xref:System.Windows.Forms.BindingManagerBase.PositionChanged> 事件。  
  
2.  将子表位置重置到前述过程中保存的缓存位置。  
  
     [!code-csharp[System.Windows.Forms.CurrencyManagerReset#3](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.CurrencyManagerReset#3](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#3)]  
  
## 示例  
 以下示例演示了如何在子表的 <xref:System.Windows.Forms.CurrencyManager> 上保存当前位置，并在父表上的编辑完成后重置该位置。  此示例包含通过使用 <xref:System.Windows.Forms.BindingSource> 组件绑定到 <xref:System.Data.DataSet> 中的两个表的两个 <xref:System.Windows.Forms.DataGridView> 控件。  两个表之间建立了关系并将此关系添加到了 <xref:System.Data.DataSet>。  出于演示目的，子表中的位置最初设置为第三行。  
  
 [!code-csharp[System.Windows.Forms.CurrencyManagerReset#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.CurrencyManagerReset#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.CurrencyManagerReset/VB/Form1.vb#1)]  
  
 若要测试代码示例，请执行以下步骤：  
  
1.  运行示例。  
  
2.  请确保“缓存并重置位置”复选框处于选中状态。  
  
3.  单击“清除父字段”按钮会导致父表的某个字段发生更改。  请注意，子表中的所选行将不会更改。  
  
4.  关闭，然后再次运行该示例。  需要这样做的原因是重置行为仅在父行中第一次更改时发生。  
  
5.  清除“缓存并重置位置”复选框。  
  
6.  单击“清除父字段”按钮。  请注意，子表中的选定的行将更改为第一行。  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing、System.Windows.Forms 和 System.Xml 程序集的引用。  
  
 有关如何从 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 的命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md)或[在命令行上使用 csc.exe 生成](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 [如何：确保绑定到同一数据源的多个控件保持同步](../../../docs/framework/winforms/multiple-controls-bound-to-data-source-synchronized.md)   
 [BindingSource 组件](../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)