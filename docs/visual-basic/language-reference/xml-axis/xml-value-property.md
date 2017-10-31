---
title: "XML 值属性 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.XmlPropertyExtensionValue"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Value 属性 [Visual Basic]"
  - "Visual Basic 代码, 访问 XML"
  - "XML 轴 [Visual Basic], Value"
  - "XML Value 属性 [Visual Basic]"
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# XML 值属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

提供对 <xref:System.Xml.Linq.XElement> 对象集合的第一个元素的值的访问。  
  
## 语法  
  
```  
  
object.Value  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`object`|必选。  <xref:System.Xml.Linq.XElement> 对象的集合。|  
  
## 返回值  
 包含集合第一个元素的值的`String`，如果集合为空则为 `Nothing`。  
  
## 备注  
 利用 <xref:System.Xml.Linq.XElement.Value%2A> 属性可以轻松访问 <xref:System.Xml.Linq.XElement> 对象集合中第一个元素的值。  此属性先检查集合是否包含至少一个对象。  如果集合为空，则该属性返回 `Nothing`。  否则，此属性返回集合中第一个元素的 <xref:System.Xml.Linq.XElement.Value%2A> 属性的值。  
  
> [!NOTE]
>  使用“@”标识符访问 XML 特性的值时，特性值是以 `String` 的形式返回的，您无需显式指定 <xref:System.Xml.Linq.XAttribute.Value%2A> 属性。  
  
 若要访问集合中的其他元素，可以使用 XML 扩展索引器属性。  有关更多信息，请参见 [扩展索引器属性](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)。  
  
## Inheritance  
 大多数用户无须实现 <xref:System.Collections.Generic.IEnumerable%601>，因此可以忽略这部分。  
  
 <xref:System.Xml.Linq.XElement.Value%2A> 属性是实现 `IEnumerable(Of XElement)` 的类型的扩展属性。  此扩展属性的绑定类似于扩展方法的绑定：如果类型实现其中一个接口，并定义具有名称“Value”的属性，则该属性优先于扩展属性。  换句话说，可以通过在实现 `IEnumerable(Of XElement)` 的类中定义一个新属性，重写此 <xref:System.Xml.Linq.XElement.Value%2A> 属性。  
  
## 示例  
 下面的示例演示如何使用 <xref:System.Xml.Linq.XElement.Value%2A> 属性访问 <xref:System.Xml.Linq.XElement> 对象集合中的第一个节点。  该示例使用子轴属性来获取 `contact` 对象中的名为 `phone` 的所有子节点的集合。  
  
 [!code-vb[VbXMLSamples#15](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_1.vb)]  
  
 这段代码将显示以下文本：  
  
 `Phone number: 206-555-0144`  
  
## 示例  
 下面的示例演示如何从 <xref:System.Xml.Linq.XAttribute> 对象集合中获取 XML 特性的值。  该示例使用特性轴属性显示所有 `phone` 元素的 `type` 特性的值。  
  
 [!code-vb[VbXMLSamples#16](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/xml-value-property_2.vb)]  
  
 这段代码将显示以下文本：  
  
 `home`  
  
 `work`  
  
## 请参阅  
 <xref:System.Xml.Linq.XElement>   
 <xref:System.Collections.Generic.IEnumerable%601>   
 [XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中创建 XML](../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [扩展索引器属性](../../../visual-basic/language-reference/xml-axis/extension-indexer-property.md)   
 [XML 子轴属性](../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [XML 特性轴属性](../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)