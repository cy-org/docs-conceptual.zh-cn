---
title: "命名空间概述 (LINQ to XML) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: b8eb31fa-4b26-4acf-8050-6e705687f458
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cec2efd31c96af17ad717abaa8f4359210e99a78
ms.lasthandoff: 03/13/2017

---
# <a name="namespaces-overview-linq-to-xml"></a>命名空间概述 (LINQ to XML)
本主题介绍命名空间、<xref:System.Xml.Linq.XName>类和<xref:System.Xml.Linq.XNamespace>类。</xref:System.Xml.Linq.XNamespace> </xref:System.Xml.Linq.XName>  
  
## <a name="xml-names"></a>XML 名称  
 XML 名称常常是导致 XML 编程复杂性的原因。 XML 名称由 XML 命名空间（也称为 XML 命名空间 URI）和本地名称组成。 XML 命名空间类似于基于 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 的程序中的命名空间。 它能够唯一限定元素和属性的名称。 这有助于避免 XML 文档各个部分之间的名称冲突。 声明 XML 命名空间后，您可以选择只须在该命名空间中是唯一的本地名称。  
  
 XML 名称的另一个方面是 XML*命名空间前缀*。 XML 名称的复杂性大都是由 XML 前缀引起的。 这些前缀可用来创建 XML 命名空间的快捷方式，从而使 XML 文档更加简洁易懂。 但是，XML 前缀仅在其上下文中才有意义，这就增加了复杂性。 例如，XML 前缀 `aw` 可以与 XML 树的一部分中的一个 XML 命名空间关联，也可以与该 XML 树的另一部分中的另一个 XML 命名空间关联。  
  
 如果通过 Visual Basic 和 XML 文本使用 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]，则在命名空间中处理文档时必须使用命名空间前缀。  
  
 在[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]，表示 XML 名称的类是<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName> XML 名称在整个频繁出现[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]API 中，任何时候只要需要 XML 名称，您将发现<xref:System.Xml.Linq.XName>参数。</xref:System.Xml.Linq.XName> 但是，很少会直接使用<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName> <xref:System.Xml.Linq.XName>包含一个从字符串的隐式转换。</xref:System.Xml.Linq.XName>  
  
 有关详细信息，请参阅<xref:System.Xml.Linq.XNamespace>和<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XNamespace>  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 命名空间 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)
