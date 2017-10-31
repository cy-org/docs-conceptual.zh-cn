---
title: "Add Content to a Text Box Using UI Automation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "adding content to text boxes"
  - "text boxes, adding content"
  - "UI Automation, adding content to text boxes"
ms.assetid: 8bdd1a73-1ecb-4a05-a891-a7827ebb767f
caps.latest.revision: 13
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 13
---
# Add Content to a Text Box Using UI Automation
> [!NOTE]
>  本文档的目标读者是欲使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]类的 .NET Framework 开发人员。  有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的最新信息，请参见 [Windows Automation API: UI Automation](http://go.microsoft.com/fwlink/?LinkID=156746)（Windows 自动化 API：UI 自动化）。  
  
 本主题包含代码示例，该代码示例演示如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]将文本插入单行文本框。  对于 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]不适用的多行和多格式文本控件，提供了另一种方法。  为了进行比较，该示例还演示如何使用 Win32 方法来达到相同的结果。  
  
## 示例  
 下面的示例将逐个通过目标应用程序中的一系列文本控件。  将对每个文本控件进行测试，以确定是否可以使用 <xref:System.Windows.Automation.AutomationElement.TryGetCurrentPattern%2A> 方法从中获取 <xref:System.Windows.Automation.ValuePattern> 对象。  如果文本控件确实支持 <xref:System.Windows.Automation.ValuePattern>，将使用 <xref:System.Windows.Automation.ValuePattern.SetValue%2A> 方法将用户定义的字符串插入文本控件。  否则，将使用 <xref:System.Windows.Forms.SendKeys.SendWait%2A?displayProperty=fullName> 方法。  
  
 [!code-csharp[InsertText#InsertText](../../../samples/snippets/csharp/VS_Snippets_Wpf/InsertText/CSharp/Window1.xaml.cs#inserttext)]
 [!code-vb[InsertText#InsertText](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InsertText/VisualBasic/Window1.xaml.vb#inserttext)]  
  
## 请参阅  
 [TextPattern Insert Text Sample](http://msdn.microsoft.com/zh-cn/67353f93-7ee2-42f2-ab76-5c078cf6ca16)