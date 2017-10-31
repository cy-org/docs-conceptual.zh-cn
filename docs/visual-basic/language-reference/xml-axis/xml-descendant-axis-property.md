---
title: "XML 子代轴属性 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyDescendantsAxis
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML descendant axis property [Visual Basic]
- descendant axis property [Visual Baisc]
- XML axis [Visual Basic], descendant
- XML [Visual Basic], accessing
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
caps.latest.revision: 14
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
ms.openlocfilehash: 434dc90c643381bdc27b2da54a7418e39bf15e98
ms.lasthandoff: 03/13/2017

---
# <a name="xml-descendant-axis-property-visual-basic"></a>XML 后代轴属性 (Visual Basic)
提供对以下的后代的访问︰<xref:System.Xml.Linq.XElement>对象，<xref:System.Xml.Linq.XDocument>对象、 一套<xref:System.Xml.Linq.XElement>对象或一套<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
## <a name="syntax"></a>语法  
  
```  
  
object...<descendant>  
```  
  
## <a name="parts"></a>部件  
 `object`  
 必需。 <xref:System.Xml.Linq.XElement>对象，<xref:System.Xml.Linq.XDocument>对象、 一套<xref:System.Xml.Linq.XElement>对象或一套<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
 ...<  
 必需。 表示子代轴属性的开头。  
  
 `descendant`  
 必需。 若要访问，窗体的子代节点的名称 [`prefix``:`]`name`。  
  
|部件|说明|  
|----------|-----------------|  
|`prefix`|可选。 子代节点的 XML 命名空间前缀。 必须通过定义一个全局 XML 命名空间`Imports`语句。|  
|`name`|必需。 子代节点的本地名称。 请参阅[声明的 XML 元素和属性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
  
 \>  
 必需。 表示子代轴属性的结尾。  
  
## <a name="return-value"></a>返回值  
 一套<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
## <a name="remarks"></a>备注  
 可以使用 XML 后代轴属性按名称从访问子代节点<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>对象，或从大量的<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 使用 XML`Value`属性来访问返回的集合中的第一个后代节点的值。 有关详细信息，请参阅[XML 值属性](../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将子代轴属性转换为对调用<xref:System.Xml.Linq.XContainer.Descendants%2A>方法。</xref:System.Xml.Linq.XContainer.Descendants%2A>  
  
## <a name="xml-namespaces"></a>XML 命名空间  
 子代轴属性中的名称可以使用只有 XML 命名空间使用全局声明`Imports`语句。 它不能使用在 XML 元素文本中局部声明的 XML 命名空间。 有关详细信息，请参阅[Imports 语句 (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何访问名为的第一个后代节点的值`name`和名为的所有子代节点的值`phone`从`contacts`对象。  
  
 [!code-vb[VbXMLSamples #&25;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_1.vb)]  
  
 此代码显示以下文本：  
  
 `Name: Patrick Hines`  
  
 `Home Phone = 206-555-0144`  
  
## <a name="example"></a>示例  
 下面的示例声明 `ns` 作为 XML 命名空间前缀。 它然后使用该命名空间前缀创建 XML 文本和访问具有限定名的第一个子节点的值`ns:name`。  
  
 [!code-vb[VbXMLSamples #&26;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-descendant-axis-property_2.vb)]  
  
 此代码显示以下文本：  
  
 `Name: Patrick Hines`  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
