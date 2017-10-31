---
title: "在加载或分析 XML1 时保留空白"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dce6d2afc6c146c346dadeb9d7e4af6fcca1b987
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>在加载或分析 XML 时保留空白
本主题说明如何控制 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的空白行为。  
  
 一种常用情况是读取缩进的 XML，在内存中创建一个没有任何空白文本节点（即不保留空白）的 XML 树，对该 XML 执行某些操作，然后保存带缩进的 XML。 在序列化带格式的 XML 时，只保留 XML 树中有意义的空白。 这是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的默认行为。  
  
 另一个常见的情况是读取和修改已经有意缩进的 XML。 您可能不想以任何方式更改这种缩进。 若要在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中执行此操作，您要在加载或解析 XML 时保留空白，并在序列化 XML 时禁用格式设置。  
  
 本主题说明用于填充 XML 树的方法的空白行为。 有关序列化 XML 树时如何控制空白的信息，请参阅[在序列化时保留空白](../../../../csharp/programming-guide/concepts/linq/preserving-white-space-while-serializing.md)。  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>用于填充 XML 树的方法的行为  
 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 类中的以下方法用于填充 XML 树。 可以从文件、<xref:System.IO.TextReader>、<xref:System.Xml.XmlReader> 或字符串填充 XML 树：  
  
-   <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=nameWithType>  
  
-   <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=nameWithType>  
  
 如果方法不采用 <xref:System.Xml.Linq.LoadOptions> 作为参数，则该方法将不会保留无意义的空白。  
  
 在多数情况下，如果方法采用 <xref:System.Xml.Linq.LoadOptions> 作为参数，则您可以选择保留无意义的空白作为 XML 树中的文本节点。 但如果方法从 <xref:System.Xml.XmlReader> 中加载 XML，则 <xref:System.Xml.XmlReader> 将确定是否保留空白。 设置 <xref:System.Xml.Linq.LoadOptions.PreserveWhitespace> 不会有影响。  
  
 使用这些方法时，如果保留空白，则会将无意义的空白插入到 XML 树中作为 <xref:System.Xml.Linq.XText> 节点。 如果不保留空白，则不会插入文本节点。  
  
 您可以使用 <xref:System.Xml.XmlWriter> 创建一个 XML 树。 写入到 <xref:System.Xml.XmlWriter> 的节点会在树中进行填充。 但在使用此方法生成 XML 树时，不管节点是否为空白或是否为无意义的空白，都将保留所有节点。  
  
## <a name="see-also"></a>请参阅  
 [分析 XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)

