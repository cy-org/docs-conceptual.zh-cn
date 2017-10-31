---
title: "如何：创建具有访问键和文本换行的控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "访问键, 控件"
  - "控件, 访问键"
  - "控件, 文本换行"
  - "键, 控件"
  - "文本换行"
  - "使文本换行"
ms.assetid: 205099d9-2551-4302-a25e-a15af9f67e04
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：创建具有访问键和文本换行的控件
本示例演示如何创建一个具有[访问键](GTMT)并支持文本换行的控件。  本示例使用 <xref:System.Windows.Controls.Label> 控件来演示这些概念。  
  
## 示例  
 **为标签添加文本换行**  
  
 <xref:System.Windows.Controls.Label> 控件不支持文本换行。  如果您需要一个多次换行的标签，可以嵌套一个支持文本换行的元素，并将该元素放在标签内。  下面的示例演示如何使用 <xref:System.Windows.Controls.TextBlock> 创建一个进行多次文本换行的标签。  
  
 <!-- TODO: review snippet reference [!code-xml[Label#5](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Label/XAML/Pane1.xaml#5)]  -->
 <!-- TODO: review snippet reference [!code-xml[Label#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Label/CS/Pane1.xaml#5)]  -->  
  
 **为标签添加访问键和文本换行**  
  
 如果您需要一个具有访问键（助记键）的 <xref:System.Windows.Controls.Label>，则可以使用 <xref:System.Windows.Controls.Label> 中的 <xref:System.Windows.Controls.AccessText> 元素。  
  
 <xref:System.Windows.Controls.Label>、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.RadioButton>、<xref:System.Windows.Controls.CheckBox>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.TabItem>、<xref:System.Windows.Controls.Expander> 和 <xref:System.Windows.Controls.GroupBox> 等控件具有默认的控件模板。  这些模板包含一个 <xref:System.Windows.Controls.ContentPresenter>。  您可以为 <xref:System.Windows.Controls.ContentPresenter> 设置的属性之一是 <xref:System.Windows.Controls.ContentPresenter.RecognizesAccessKey%2A>\="true"，您可以使用该属性为控件指定访问键。  
  
 下面的示例演示如何创建一个具有访问键并支持文本换行的 <xref:System.Windows.Controls.Label>。  为了实现文本换行，本示例设置了 <xref:System.Windows.Controls.AccessText.TextWrapping%2A> 属性并使用下划线字符指定访问键。  （紧跟下划线字符后面的字符就是访问键。）  
  
 <!-- TODO: review snippet reference [!code-xml[Label#4](../../../../samples/snippets/xaml/VS_Snippets_Wpf/Label/XAML/Pane1.xaml#4)]  -->
 <!-- TODO: review snippet reference [!code-xml[Label#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Label/CS/Pane1.xaml#4)]  -->  
  
## 请参阅  
 [How to: Set the Target Property of a Label](http://msdn.microsoft.com/zh-cn/b24c6977-ebcb-4855-a9bb-3fd4435af8f8)