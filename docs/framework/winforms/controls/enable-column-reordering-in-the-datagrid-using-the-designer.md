---
title: "如何：使用设计器在 Windows 窗体的 DataGridView 控件中启用列重新排序 | Microsoft Docs"
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
  - "列 [Windows 窗体], 重新排序"
  - "数据 [Windows 窗体], 显示"
  - "DataGridView 控件 [Windows 窗体], 列顺序"
  - "Windows 窗体, 列"
ms.assetid: d82bd69c-6799-4439-a32c-91139c5901d1
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用设计器在 Windows 窗体的 DataGridView 控件中启用列重新排序
当用户查看显示在 Windows 窗体的 <xref:System.Windows.Forms.DataGridView> 控件中的数据时，有时希望对特定列中的值进行比较。  如果列广泛地分散在控件中，这样做可能不太方便，尤其是在用户为了查看所有感兴趣的列而必须前后水平滚动时。  通过允许您的用户对列进行重新排序，可以使比较列值的任务更加轻松。  当您启用列重新排序时，用户可以用鼠标拖动列标题，将某个列移动到一个新的位置。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，项目中应有一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 启用列重新排序  
  
-   单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“启用列重新排序”**。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=fullName>   
 [如何：使用设计器冻结 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/freeze-columns-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)