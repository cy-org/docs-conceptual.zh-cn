---
title: "如何：创建专用的字体集合 | Microsoft Docs"
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
  - "字体, 创建专用集合"
  - "专用字体集合, 创建"
ms.assetid: 6533d5e5-a8dc-4b76-9fc4-3bf75c8b9212
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：创建专用的字体集合
<xref:System.Drawing.Text.PrivateFontCollection> 类继承自 <xref:System.Drawing.Text.FontCollection> 抽象基类。  可使用 <xref:System.Drawing.Text.PrivateFontCollection> 对象维护应用程序专用的字体集。  专用的字体集合既可包括计算机上安装的系统字体，又可包括计算机上尚未安装的字体。  若要向专用的字体集内添加字体文件，请调用 <xref:System.Drawing.Text.PrivateFontCollection> 对象的 <xref:System.Drawing.Text.PrivateFontCollection.AddFontFile%2A> 方法。  
  
 <xref:System.Drawing.Text.PrivateFontCollection> 对象的 <xref:System.Drawing.Text.FontCollection.Families%2A> 属性包含一组 <xref:System.Drawing.FontFamily> 对象。  
  
 专用字体集合中字体系列的数量不必与已添加到字体集内的字体文件的数量相同。  例如，假定将 ArialBd.tff、Times.tff 和 TimesBd.tff 文件添加到一个集合内。  该字体集合内将有三个文件，但是只有两个系列，这是因为 Times.tff 和 TimesBd.tff 属于相同的系列。  
  
## 示例  
 下面的示例将以下三个字体文件添加到 <xref:System.Drawing.Text.PrivateFontCollection> 对象中：  
  
-   C:\\*systemroot*\\Fonts\\Arial.tff（Arial，常规）  
  
-   C:\\*systemroot*\\Fonts\\CourBI.tff（Courier New，加粗倾斜）  
  
-   C:\\*systemroot*\\Fonts\\TimesBd.tff（Times New Roman，加粗）  
  
 代码从 <xref:System.Drawing.Text.PrivateFontCollection> 对象的 <xref:System.Drawing.Text.FontCollection.Families%2A> 属性中检索 <xref:System.Drawing.FontFamily> 对象数组。  
  
 对于集合内的每个 <xref:System.Drawing.FontFamily> 对象，代码调用 <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> 方法以确定各种字形（常规、加粗、倾斜、加粗倾斜、下划线和删除线）是否可用。  传递给 <xref:System.Drawing.FontFamily.IsStyleAvailable%2A> 方法的参数为 <xref:System.Drawing.FontStyle> 枚举的成员。  
  
 如果给定的字体\/字形组合可用，则使用该字体\/字形构造 <xref:System.Drawing.Font> 对象。  传递给 <xref:System.Drawing.Font.%23ctor%2A> 构造函数的第一个参数是字体名称（不是用于 <xref:System.Drawing.Font.%23ctor%2A> 构造函数的其他变体的 <xref:System.Drawing.FontFamily> 对象）。  在构造 <xref:System.Drawing.Font> 对象之后，它将被传递给 <xref:System.Drawing.Graphics> 类的 <xref:System.Drawing.Graphics.DrawString%2A> 方法，以显示字体名称和字形名称。  
  
 下面的代码的输出类似于下面插图中所显示的输出。  
  
 ![字体文本](../../../../docs/framework/winforms/advanced/media/csfontstext7.png "csfontstext7")  
  
 Arial.tff（在下面的代码示例中已添加到专用字体集合中）是 Arial 常规字形的字体文件。  然而，请注意，该程序的输出显示了 Arial 字体系列的除了常规字形以外的几种可用字形。  这是因为 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可以从常规字形模拟加粗、倾斜和加粗倾斜字形。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 还可从常规字形生成下划线和删除线。  
  
 同样，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可从加粗字形或倾斜字形模拟加粗倾斜字形。  该程序的输出表明，即使 TimesBd.tff（Times New Roman，加粗）是字体集合内唯一的 Times 文件，Times 系列仍可使用加粗倾斜字形。  
  
 [!code-csharp[System.Drawing.FontsAndText#51](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.FontsAndText#51](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#51)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Text.PrivateFontCollection>   
 [使用字体和文本](../../../../docs/framework/winforms/advanced/using-fonts-and-text.md)