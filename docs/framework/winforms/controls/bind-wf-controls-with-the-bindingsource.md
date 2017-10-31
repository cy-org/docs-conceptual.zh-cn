---
title: "如何：使用设计器将 Windows 窗体控件与 BindingSource 组件进行绑定 | Microsoft Docs"
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
  - "BindingSource 组件 [Windows 窗体], 绑定控件"
  - "控件 [Windows 窗体], 绑定"
  - "数据绑定, BindingSource 组件"
ms.assetid: 391ae170-de5c-40f8-8233-91cb2ee4683a
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：使用设计器将 Windows 窗体控件与 BindingSource 组件进行绑定
将控件添加到窗体并确定应用程序的用户界面后，可以将控件绑定到数据源，这样用户就可以在运行时改变和保存与应用程序相关的数据。  
  
 将 <xref:System.Windows.Forms.BindingSource> 控件用作窗体上的控件和数据源之间的桥梁，能够最轻松地完成 Windows 窗体中一个控件或一系列控件的绑定。  
  
 可以将窗体上的一个或多个控件绑定到数据；在下面的过程中，将一个 <xref:System.Windows.Forms.TextBox> 控件绑定到一个数据源。  
  
 为了完成此过程，假定将绑定到派生自数据库的数据源。  有关从其他数据存储区创建数据源的更多信息，请参见 [数据源概述](../Topic/Add%20new%20data%20sources.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时绑定控件  
  
1.  将 <xref:System.Windows.Forms.TextBox> 控件拖到窗体上。  
  
2.  在**“属性”**窗口中：  
  
    1.  展开**“\(DataBindings\)”**节点。  
  
    2.  单击 <xref:System.Windows.Forms.TextBox.Text%2A> 属性旁边的箭头。  
  
         此时将打开**“DataSource”**UI 类型编辑器。  
  
         如果以前已经为项目或窗体配置了数据源，将显示此数据源。  
  
3.  单击**“添加项目数据源”**以连接到数据并创建一个数据源。  
  
4.  在**“数据源配置向导”**欢迎页上单击**“下一步”**。  
  
5.  在**“选择数据源类型”**页上选择**“数据库”**。  
  
6.  在**“选择您的数据连接”**页上，从可用连接列表中选择一个数据连接。  如果所需的数据连接不可用，请选择**“新建连接”**以创建新的数据连接。  
  
7.  选择**“是，保存连接”**，以保存应用程序配置文件中的连接字符串。  
  
8.  选择要放置到应用程序中的数据库对象。  在此例中，在表中选择一个希望显示 <xref:System.Windows.Forms.TextBox> 的字段。  
  
9. 如果愿意，可以替换默认的数据集名称。  
  
10. 单击**“完成”**。  
  
11. 在**“属性”**窗口中，再次单击 <xref:System.Windows.Forms.TextBox.Text%2A> 属性旁的箭头。  在**“DataSource”**UI 类型编辑器中，选择要将 <xref:System.Windows.Forms.TextBox> 绑定到的字段的名称。  
  
     **“DataSource”**UI 类型编辑器关闭，并且特定于该数据连接的数据集、<xref:System.Windows.Forms.BindingSource> 和表适配器将添加到窗体中。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.Windows.Forms.BindingNavigator>   
 [数据源概述](../Topic/Add%20new%20data%20sources.md)   
 [“数据源”窗口](../Topic/Data%20Sources%20Window.md)