---
title: "如何：克隆打印机 | Microsoft Docs"
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
  - "克隆打印队列"
  - "克隆打印机"
  - "打印队列"
  - "打印队列, 克隆"
  - "打印机, 克隆"
ms.assetid: dd6997c9-fe04-40f8-88a6-92e3ac0889eb
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：克隆打印机
大多数公司有时可能会购买多台同一型号的打印机。  通常，这些打印机都使用大致相同的配置设置安装。  安装每台打印机会很耗时并且容易出错。  使用随 [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)]一起公开的 <xref:System.Printing.IndexedProperties?displayProperty=fullName> 命名空间和 <xref:System.Printing.PrintServer.InstallPrintQueue%2A> 类，可以快速安装任意数量的从现有打印队列克隆的附加打印队列。  
  
## 示例  
 下面的示例将从现有的打印队列克隆出第二个打印队列。  第二个打印队列仅在名称、位置、端口和共享状态方面与第一个打印队列有所不同。  此操作的主要步骤如下所示。  
  
1.  为要克隆的现有打印机创建一个 <xref:System.Printing.PrintQueue> 对象。  
  
2.  从 <xref:System.Printing.PrintQueue> 的 <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> 创建 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>。  此字典中每项的 <xref:System.Collections.DictionaryEntry.Value%2A> 属性是从 <xref:System.Printing.IndexedProperties.PrintProperty> 派生的类型之一的对象。  可通过两种方式设置此字典中项的值。  
  
    -   使用字典的 **Remove** 和 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.Add%2A> 方法移除项，然后使用所需的值重新添加此项。  
  
    -   使用字典的 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.SetProperty%2A> 方法。  
  
     下面的示例演示了这两种方式。  
  
3.  创建一个 <xref:System.Printing.IndexedProperties.PrintBooleanProperty> 对象，将其 <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> 设置为“IsShared”并将其 <xref:System.Printing.IndexedProperties.PrintBooleanProperty.Value%2A> 设置为 `true`。  
  
4.  将 <xref:System.Printing.IndexedProperties.PrintBooleanProperty> 对象用作 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> 的“IsShared”项的值。  
  
5.  创建一个 <xref:System.Printing.IndexedProperties.PrintStringProperty> 对象，将其 <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> 设置为“ShareName”并将其 <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> 设置为相应的 <xref:System.String>。  
  
6.  将 <xref:System.Printing.IndexedProperties.PrintStringProperty> 对象用作 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> 的“ShareName”项的值。  
  
7.  再创建一个 <xref:System.Printing.IndexedProperties.PrintStringProperty> 对象，将其 <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> 设置为“Location”并将其 <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> 设置为相应的 <xref:System.String>。  
  
8.  将第二个 <xref:System.Printing.IndexedProperties.PrintStringProperty> 对象用作 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> 的“Location”项的值。  
  
9. 创建 <xref:System.String> 的数组。  其中各项是服务器的端口名称。  
  
10. 使用 <xref:System.Printing.PrintServer.InstallPrintQueue%2A> 安装包含新值的新打印机。  
  
 下面演示了一个示例。  
  
 [!code-csharp[ClonePrinter#ClonePrinter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClonePrinter/CSharp/Program.cs#cloneprinter)]
 [!code-vb[ClonePrinter#ClonePrinter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClonePrinter/visualbasic/program.vb#cloneprinter)]  
  
## 请参阅  
 <xref:System.Printing.IndexedProperties>   
 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Collections.DictionaryEntry>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)