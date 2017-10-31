---
title: "如何：使用设计器在 Windows 窗体 ListView 控件中启用平铺视图 | Microsoft Docs"
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
  - "ListView 控件 [Windows 窗体], 平铺视图"
  - "平铺视图功能"
  - "平铺, Windows 窗体, 控件"
ms.assetid: 12f0816a-52b8-41ee-a6d9-ded3a8a5817a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用设计器在 Windows 窗体 ListView 控件中启用平铺视图
通过 <xref:System.Windows.Forms.ListView> 控件的平铺视图功能可以在图形信息和文本信息之间提供视觉上的平衡。  为平铺视图中的某项显示的文本信息与为详细信息视图定义的列信息相同。  在 <xref:System.Windows.Forms.ListView> 控件中，平铺视图与分组或插入标记功能一同运行。  
  
 平铺视图使用 32 x 32 的图标和若干行文本，如下图所示。  
  
 ![ListView 控件中的平铺视图](../../../../docs/framework/winforms/controls/media/listviewtile.gif "ListViewTile")  
  
 使用平铺视图属性和方法可以指定要为每项显示的列字段，并可以对平铺视图窗口中所有项的大小和外观进行整体控制。  为了清楚起见，平铺视图中的第一行文本总是该项的名称；该名称无法更改。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.ListView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  平铺视图仅在应用程序调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法时在 [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] 上可用。  在以前的操作系统上，与平铺视图相关的任何代码均无效，<xref:System.Windows.Forms.ListView> 控件以大图标视图的形式显示。  有关更多信息，请参见 <xref:System.Windows.Forms.ListView.View%2A?displayProperty=fullName>。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中设置平铺视图  
  
1.  选择窗体上的 <xref:System.Windows.Forms.ListView> 控件。  
  
2.  在**“属性”**窗口中，选择 <xref:System.Windows.Forms.ListView.View%2A> 属性，然后选择**“平铺”**。  
  
## 请参阅  
 <xref:System.Windows.Forms.ListView.TileSize%2A>   
 [Windows XP Features and Windows Forms Controls](http://msdn.microsoft.com/zh-cn/bc7fab94-fce9-4bf1-a8ad-a5837c91c3c0)   
 [ListView 控件概述](../../../../docs/framework/winforms/controls/listview-control-overview-windows-forms.md)