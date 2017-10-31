---
title: "如何：在 Windows 窗体上创建简单绑定控件 | Microsoft Docs"
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
  - "数据绑定, 简单的数据绑定"
  - "Windows 窗体控件, 数据绑定"
ms.assetid: 3bcaded8-0f1a-4cc0-8830-f59be253bf4e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 Windows 窗体上创建简单绑定控件
“简单绑定”使您得以在控件中显示单个数据元素，如来自数据集表的列值。  可将控件的任何属性简单绑定到数据值。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 简单绑定控件  
  
1.  连接到数据源。  有关更多信息，请参见[连接到数据源](../../../docs/framework/data/adonet/connecting-to-a-data-source.md)。  
  
2.  在窗体中，选择该控件并显示**“属性”**窗口。  
  
3.  展开 **\(DataBindings\)** 属性。  
  
     最常绑定的属性在 **\(DataBindings\)** 属性下显示。  例如，在大多数控件中，最经常绑定的是 **Text** 属性。  
  
4.  如果要绑定的属性不是一个经常绑定的属性，请在**“\(高级\)”**框中单击**“省略号”**按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)，以显示具有该控件的完整属性列表的**“格式设置和高级绑定”**对话框。  
  
5.  选择要绑定的属性，然后单击**“绑定”**下面的下拉箭头。  
  
     显示可用数据源的列表。  
  
6.  展开要绑定到的数据源，直到找到所需的单个数据元素。  例如，如果要绑定到数据集表中的某个列值，则请展开该数据集的名称，然后展开该表名以显示列名。  
  
7.  单击要绑定到的元素的名称。  
  
8.  如果正在处理**“格式设置和高级绑定”**对话框，请单击**“确定”**返回到**“属性”**窗口。  
  
9. 如果要绑定控件的其他属性，请重复步骤 3 到 7。  
  
    > [!NOTE]
    >  因为简单绑定控件仅显示单个数据元素，所以通常在具有简单绑定控件的 Windows 窗体中包含导航逻辑。  
  
## 请参阅  
 <xref:System.Windows.Forms.Binding>   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)