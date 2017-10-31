---
title: "如何：使用设计器将数据绑定到 Windows 窗体的 DataGridView 控件 | Microsoft Docs"
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
  - "数据源, 绑定到 Windows 窗体控件"
  - "DataGridView 控件 [Windows 窗体], 数据绑定"
  - "Windows 窗体控件, 绑定到数据源"
ms.assetid: f4f46009-cec2-441b-8668-6b5af057558b
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 如何：使用设计器将数据绑定到 Windows 窗体的 DataGridView 控件
您可以使用设计器将 <xref:System.Windows.Forms.DataGridView> 控件连接到多种不同的数据源变体，包括数据库、业务对象或 Web 服务。  当您使用设计器将控件绑定到数据源时，控件会自动绑定到一个表示数据源的 <xref:System.Windows.Forms.BindingSource> 组件。  另外，控件中会自动生成若干列，以匹配由数据源提供的架构信息。  
  
 列生成之后，您可以根据需要对其进行修改。  例如，您可以移去或隐藏自己不感兴趣的列使之无法显示，可以重新排列各列，也可以修改列的类型。  有关修改列的更多信息，请查阅“请参见”部分中列出的主题。  
  
 还可以将多个 <xref:System.Windows.Forms.DataGridView> 控件绑定到相关表中以创建主\/从关系。  在此配置中，一个控件显示父表，另一个控件仅显示子表中与父表中当前行相关的那些行。  有关更多信息，请参见 [如何：在 Windows 窗体应用程序中显示相关数据](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目的窗体需包含一个 <xref:System.Windows.Forms.DataGridView> 控件或两个控件以建立主\/从关系。  有关创建此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 将控件绑定到数据源  
  
1.  单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)。  
  
2.  单击**“选择数据源”**选项的下拉箭头。  
  
3.  如果您的项目还没有数据源，请单击**“添加项目数据源”**并按照向导提示的步骤操作。  
  
     有关更多信息，请参见 [数据源配置向导](../Topic/Data%20Source%20Configuration%20Wizard.md)。  新的数据源将显示在**“选择数据源”**下拉窗口中。  如果新的数据源只包含一个成员（例如，单个数据库表），控件将自动绑定到该成员。  否则，请继续下一步。  
  
4.  如果**“其他数据源”**和**“项目数据源”**节点尚未展开，请展开它们，然后为绑定控件选择数据源。  
  
5.  如果您的数据源包含多个成员（例如，如果您创建了一个包含多个表的 <xref:System.Data.DataSet?displayProperty=fullName>），请展开该数据源并选择要绑定到的特定成员。  
  
6.  若要创建主\/从关系，请在第二个 <xref:System.Windows.Forms.DataGridView> 控件的**“选择数据源”**下拉窗口中，展开为父表创建的 <xref:System.Windows.Forms.BindingSource>，然后从显示的列表中选择相关的子表。  
  
    > [!NOTE]
    >  如果项目已经有数据源，则还可以使用**“数据源”**窗口创建数据窗体。  有关更多信息，请参见[“数据源”窗口](../Topic/Data%20Sources%20Window.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.DataGridView.DataMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=fullName>   
 [如何：连接到数据库中的数据](../Topic/How%20to:%20Connect%20to%20Data%20in%20a%20Database.md)   
 [如何：使用设计器添加和移除 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [如何：使用设计器更改 Windows 窗体 DataGridView 控件中列的顺序](../../../../docs/framework/winforms/controls/change-the-order-of-columns-in-the-datagrid-using-the-designer.md)   
 [如何：使用设计器更改 Windows 窗体 DataGridView 列的类型](../../../../docs/framework/winforms/controls/change-the-type-of-a-wf-datagridview-column-using-the-designer.md)   
 [如何：使用设计器冻结 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/freeze-columns-in-the-datagrid-using-the-designer.md)   
 [如何：使用设计器隐藏 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/hide-columns-in-the-datagrid-using-the-designer.md)   
 [如何：使用设计器使 Windows 窗体 DataGridView 控件中的列成为只读](../../../../docs/framework/winforms/controls/make-columns-read-only-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [“数据源”窗口](../Topic/Data%20Sources%20Window.md)   
 [如何：在 Windows 窗体应用程序中显示相关数据](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)