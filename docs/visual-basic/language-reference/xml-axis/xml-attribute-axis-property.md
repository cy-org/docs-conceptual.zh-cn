---
title: "XML 特性轴属性 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlPropertyAttributeAxis
dev_langs:
- VB
helpviewer_keywords:
- attribute axis property [Visual Basic]
- Visual Basic code, accessing XML
- XML attribute axis property [Visual Basic]
- XML axis [Visual Basic], attribute
- XML [Visual Basic], accessing
ms.assetid: 7a4777e1-0618-4de9-9510-fb9ace2bf4db
caps.latest.revision: 23
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
ms.openlocfilehash: 94211f7c951976426ba17e73df214444a6c227b4
ms.lasthandoff: 03/13/2017

---
# <a name="xml-attribute-axis-property-visual-basic"></a>XML 特性轴属性 (Visual Basic)
提供对有关属性的值的访问<xref:System.Xml.Linq.XElement>对象或集合中的第一个元素<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
## <a name="syntax"></a>语法  
  
```  
  
      object.@attribute  
-or-  
object.@<attribute>  
```  
  
## <a name="parts"></a>部件  
 `object`  
 必需。 <xref:System.Xml.Linq.XElement>对象或集合的<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement>  
  
 .@  
 必需。 表示特性轴属性的开头。  
  
 <  
 可选。 表示属性的名称开头时`attribute`不是有效的标识符中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
 `attribute`  
 必需。 若要访问，窗体的属性名称 [`prefix`:]`name`。  
  
|部件|描述|  
|----------|-----------------|  
|`prefix`|可选。 该属性的 XML 命名空间前缀。 必须是使用 `Imports` 语句定义的全局 XML 命名空间。|  
|`name`|必需。 本地属性名称。 请参阅[声明的 XML 元素和属性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)。|  
  
 \>  
 可选。 表示属性的名称的结尾时`attribute`不是有效的标识符中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
## <a name="return-value"></a>返回值  
 一个字符串，包含的值`attribute`。 如果属性名称不存在，`Nothing`返回。  
  
## <a name="remarks"></a>备注  
 可以使用 XML 特性轴属性来访问属性的值按名称从<xref:System.Xml.Linq.XElement>对象或从集合中的第一个元素<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement> 可以按名称检索属性值，也可以将新属性添加到元素，通过指定新名称前面有 @ 标识符。  
  
 引用时使用 XML 属性使用 @ 标识符，该属性值返回作为字符串，并且不需要显式指定<xref:System.Xml.Linq.XAttribute.Value%2A>属性。</xref:System.Xml.Linq.XAttribute.Value%2A>  
  
 用于 XML 特性的命名规则与不同的命名规则[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]标识符。 若要访问 XML 特性都不是有效的 Visual Basic 标识符的名称，请将名称括在尖括号 (\<和&1;>)。  
  
## <a name="xml-namespaces"></a>XML 命名空间  
 特性轴属性中的名称可以使用通过使用全局声明的只有 XML 命名空间前缀`Imports`语句。 它不能使用在 XML 元素文本中局部声明的 XML 命名空间前缀。 有关详细信息，请参阅[Imports 语句 (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何获取名为的 XML 特性的值`type`从 XML 元素的命名集合`phone`。  
  
 [!code-vb[VbXMLSamples #&12;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-attribute-axis-property_1.vb)]  
  
 此代码显示以下文本：  
  
 `<phoneTypes>`  
  
 `<type>home</type>`  
  
 `<type>work</type>`  
  
 `</phoneTypes>`  
  
## <a name="example"></a>示例  
 下面的示例演示如何以声明方式的一部分，该 XML，并动态地通过将属性添加到的实例创建这两个 XML 元素的属性<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement> `type`属性以声明方式创建和`owne`r 特性动态创建。  
  
 [!code-vb[VbXMLSamples #&44;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-attribute-axis-property_2.vb)]  
  
 此代码显示以下文本：  
  
```  
<phone type="home" owner="Harris, Phyllis">206-555-0144</phone>  
```  
  
## <a name="example"></a>示例  
 下面的示例使用尖括号语法来获取名为 XML 属性的值`number-type`，它不在有效标识符[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
 [!code-vb[VbXMLSamples #&13;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-attribute-axis-property_3.vb)]  
  
 此代码显示以下文本：  
  
 `Phone type: work`  
  
## <a name="example"></a>示例  
 下面的示例声明 `ns` 作为 XML 命名空间前缀。 它然后使用该命名空间前缀创建 XML 文本和访问的第一个子节点的限定名"`ns:name`"。  
  
 [!code-vb[VbXMLSamples #&14;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-attribute-axis-property_4.vb)]  
  
 此代码显示以下文本：  
  
 `Phone type: home`  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Linq.XElement>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [已声明的 XML 元素和特性的名称](../../../visual-basic/programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
