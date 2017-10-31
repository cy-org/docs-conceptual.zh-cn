---
title: "如何：使用设计器添加和移除 Windows 窗体 DataGridView 控件中的列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.DataGridViewAddColumnDialog"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DataGridView 控件 [Windows 窗体], 添加列"
  - "DataGridView 控件 [Windows 窗体], 移除列"
ms.assetid: 9e709f35-0a8c-4e7e-b4c4-bacb7a834077
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：使用设计器添加和移除 Windows 窗体 DataGridView 控件中的列
要显示数据，Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件必须包含列。  如果您计划手动填充控件，则必须自己添加列。  否则，可以将控件绑定到数据源，从而自动生成并填充列。  如果数据源包含的列多于您要显示的，可移除不需要的列。  
  
 下面的过程要求有一个带窗体的**“Windows 应用程序”**项目，且窗体中要包括一个 <xref:System.Windows.Forms.DataGridView> 控件。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 使用设计器添加列  
  
1.  单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“添加列”**。  
  
2.  在**“添加列”**对话框中，选择**“数据绑定列”**选项并从数据源中选择一列，或者选择**“未绑定的列”**选项并使用提供的字段来定义列。  
  
3.  单击**“添加”**按钮添加列，使其在现有列尚未填入控件显示区域的情况下出现在设计器中。  
  
    > [!NOTE]
    >  可在**“编辑列”**对话框中修改列属性，该对话框可通过控件的智能标记来访问。  
  
### 使用设计器移除列  
  
1.  从控件的智能标记中选择**“编辑列”**。  
  
2.  从**“选定的列”**列表中选择一列。  
  
3.  单击**“移除”**按钮删除该列，使其从设计器中消失。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)