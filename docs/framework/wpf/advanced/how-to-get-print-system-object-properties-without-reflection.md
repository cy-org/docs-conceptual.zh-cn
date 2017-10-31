---
title: "如何：在不使用反射的情况下获得打印系统对象属性 | Microsoft Docs"
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
  - "PrintSystemObject, 获取属性"
ms.assetid: 43560f28-183d-41c1-b9d1-de7c2552273e
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：在不使用反射的情况下获得打印系统对象属性
使用反射列举对象的属性（以及这些属性的类型）会降低应用程序性能。  <xref:System.Printing.IndexedProperties> 命名空间提供一种使用反射获取此信息的方法。  
  
## 示例  
 执行如下步骤可以实现上述目的：  
  
1.  创建类型的实例。  在下面的示例中，类型为 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)]附带的 <xref:System.Printing.PrintQueue> 类型，但几近相同的代码也适用于您从 <xref:System.Printing.PrintSystemObject> 派生的类型。  
  
2.  通过该类型的 <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> 创建 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>。  此字典中每项的 <xref:System.Collections.DictionaryEntry.Value%2A> 属性是从 <xref:System.Printing.IndexedProperties.PrintProperty> 派生的类型之一的对象。  
  
3.  枚举字典的成员。  对于每个成员，请执行下列操作。  
  
4.  将每项的值向上转换为 <xref:System.Printing.IndexedProperties.PrintProperty>，并使用它来创建一个 <xref:System.Printing.IndexedProperties.PrintProperty> 对象。  
  
5.  获取每个 <xref:System.Printing.IndexedProperties.PrintProperty> 对象的 <xref:System.Printing.IndexedProperties.PrintProperty.Value%2A> 的类型。  
  
 [!code-csharp[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/CSharp/Program.cs#showpropertytypeswithoutreflection)]
 [!code-vb[GetPrintObjectPropertyTypesWithoutReflection#ShowPropertyTypesWithoutReflection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/GetPrintObjectPropertyTypesWithoutReflection/visualbasic/program.vb#showpropertytypeswithoutreflection)]  
  
## 请参阅  
 <xref:System.Printing.IndexedProperties.PrintProperty>   
 <xref:System.Printing.PrintSystemObject>   
 <xref:System.Printing.IndexedProperties>   
 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>   
 <xref:System.Printing.LocalPrintServer>   
 <xref:System.Printing.PrintQueue>   
 <xref:System.Collections.DictionaryEntry>   
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)   
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)