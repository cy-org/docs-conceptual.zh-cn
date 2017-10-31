---
title: "如何：查找由 ControlTemplate 生成的元素 | Microsoft Docs"
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
  - "ControlTemplates [WPF], 查找元素"
  - "查找 ControlTemplate 元素"
ms.assetid: d7b25447-ceff-4bb4-9be5-fd7c40ef00af
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：查找由 ControlTemplate 生成的元素
下面的示例演示如何查找由 <xref:System.Windows.Controls.ControlTemplate> 生成的元素。  
  
## 示例  
 下面的示例演示一个用来为 <xref:System.Windows.Controls.Button> 类创建简单 <xref:System.Windows.Controls.ControlTemplate> 的样式：  
  
 [!code-xml[FindGeneratedItems#CT](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml#ct)]  
  
 若要在应用模板之后在模板中查找某个元素，可以调用 <xref:System.Windows.Controls.Control.Template%2A> 的 <xref:System.Windows.FrameworkTemplate.FindName%2A> 方法。  下面的示例创建一个消息框，该消息框显示控件模板中 <xref:System.Windows.Controls.Grid> 的实际宽度值：  
  
 [!code-csharp[FindGeneratedItems#CTFindElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FindGeneratedItems/CSharp/Window1.xaml.cs#ctfindelement)]
 [!code-vb[FindGeneratedItems#CTFindElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FindGeneratedItems/VisualBasic/Window1.xaml.vb#ctfindelement)]  
  
## 请参阅  
 [查找由 DataTemplate 生成的元素](../../../../docs/framework/wpf/data/how-to-find-datatemplate-generated-elements.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [WPF XAML 名称范围](../../../../docs/framework/wpf/advanced/wpf-xaml-namescopes.md)   
 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)