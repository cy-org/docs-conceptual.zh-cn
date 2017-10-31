---
title: "LINQ to XML 在 Visual Basic 中的概述 |Microsoft 文档"
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
helpviewer_keywords:
- LINQ to XML [Visual Basic], about LINQ to XML
- LINQ [Visual Basic], LINQ to XML
ms.assetid: 01c62a79-6d58-468e-84fb-039c05947701
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 508d4a97b0636f10607326eb35c4c5d8c7860873
ms.lasthandoff: 03/13/2017

---
# <a name="overview-of-linq-to-xml-in-visual-basic"></a>Visual Basic 中的 LINQ to XML 概述
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供了对支持[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]通过 XML 文本和 XML 轴属性。 这使您可以使用熟悉、 便利的语法，在中使用 XML 您[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]代码。 *XML 文本*使您能够在您的代码中直接包含 XML。 *XML 轴属性*使您能够访问子节点、 子代节点和属性的 XML 文本。 有关详细信息，请参阅[XML 文本概述](../../../../visual-basic/programming-guide/language-features/xml/xml-literals-overview.md)和[在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]内存中 XML 编程 API，专门用于充分利用[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]。 尽管可以调用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]Api 直接，只[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可用于声明 XML 文本和直接访问 XML 轴属性。  
  
> [!NOTE]
>  在 ASP.NET 页中的声明性代码中不支持 XML 文本和 XML 轴属性。 若要使用 Visual Basic XML 功能，请将代码放在 ASP.NET 应用程序中的代码隐藏页。  
  
 ![视频链接](../../../../visual-basic/programming-guide/language-features/xml/media/playvideo.gif "PlayVideo")相关的视频演示，请参阅[如何开始使用 LINQ to XML？](http://go.microsoft.com/fwlink/?LinkId=143034)和[如何实现创建 Excel 电子表格使用 LINQ to XML？](http://go.microsoft.com/fwlink/?LinkId=143536)。  
  
## <a name="creating-xml"></a>创建 XML  
 有两种方法来创建 XML 树的[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 您可以声明 XML 文本直接在代码中，也可以使用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]Api 以创建树。 这两个进程都使代码能够反映最终 XML 树的结构。 例如，下面的代码示例创建一个 XML 元素︰  
  
 [!code-vb[VbXmlSamples #&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_1.vb)]  
  
 有关详细信息，请参阅[在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)。  
  
## <a name="accessing-and-navigating-xml"></a>访问和导航 XML  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供用于访问和导航 XML 结构的 XML 轴属性。 这些属性，您可以通过指定的 XML 子元素名称来访问 XML 元素和属性。 或者，您可以显式调用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]用于导航和查找元素和属性的方法。 例如，下面的代码示例使用 XML 轴属性来引用的属性和 XML 元素的子元素。 此代码示例使用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询以检索子元素并输出为 XML 元素，从而有效地执行转换。  
  
 [!code-vb[VbXmlSamples #&8;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_2.vb)]  
  
 有关详细信息，请参阅[在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)。  
  
## <a name="xml-namespaces"></a>XML 命名空间  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使您能够通过使用指定为全局的 XML 命名空间别名`Imports`语句。 下面的示例演示如何使用`Imports`语句导入的 XML 命名空间︰  
  
 [!code-vb[VbXMLSamples #&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_3.vb)]  
  
 访问 XML 轴属性和声明的 XML 文档和元素的 XML 文本时，可以使用 XML 命名空间别名。  
  
 您可以检索<xref:System.Xml.Linq.XNamespace>对象使用的特定命名空间前缀[GetXmlNamespace 运算符](../../../../visual-basic/language-reference/operators/getxmlnamespace-operator.md)。</xref:System.Xml.Linq.XNamespace>  
  
 有关详细信息，请参阅[Imports 语句 (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
### <a name="using-xml-namespaces-in-xml-literals"></a>在 XML 文本中使用 XML 命名空间  
 下面的示例演示如何创建<xref:System.Xml.Linq.XElement>使用全局命名空间的对象`ns`:</xref:System.Xml.Linq.XElement>  
  
 [!code-vb[VbXMLSamples #&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_4.vb)]  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将转换成等效的代码，用于使用 XML 命名空间的 XML 表示法包含 XML 命名空间别名的 XML 文本`xmlns`属性。 在编译时上, 一节示例中的代码将产生与下面的示例实质上是相同的可执行代码︰  
  
 [!code-vb[VbXMLSamples #&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_5.vb)]  
  
### <a name="using-xml-namespaces-in-xml-axis-properties"></a>使用 XML 命名空间中 XML 轴属性  
 XML 文本声明的 XML 命名空间不可用于在 XML 轴属性中使用。 但是，全局命名空间可以用于 XML 轴属性。 使用冒号分隔 XML 命名空间前缀和本地元素名称。 下面是一个示例：  
  
 [!code-vb[VbXMLSamples #&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/overview-of-linq-to-xml_6.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)
