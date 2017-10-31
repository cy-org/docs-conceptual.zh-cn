---
title: "如何：访问 XML 子元素 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "子轴属性 [Visual Basic]"
  - "XML [Visual Basic], 访问"
  - "XML 轴 [Visual Basic], 子控件"
  - "XML 子轴属性 [Visual Basic]"
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 如何：访问 XML 子元素 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本示例演示如何使用子轴属性来访问某个 XML 元素中具有指定名称的所有 XML 子元素。  具体而言，它使用 <xref:System.Xml.Linq.XElement.Value%2A> 属性来获取 `name` 子轴属性返回的集合中的第一个元素的值。  `name` 子轴属性获取 `contact` 对象中所有名为 `phone` 的子元素。  本示例还使用 `phone` 子轴属性来访问 `contact` 对象中包含的所有名为 `phone` 的子元素。  
  
## 示例  
 [!code-vb[VbXMLSamples#10](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-access-xml-child-elements_1.vb)]  
  
## 编译代码  
 此示例需要：  
  
-   对 <xref:System.Xml.Linq> 命名空间的引用。  
  
## 请参阅  
 <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=fullName>   
 [XML 子轴属性](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)   
 [XML 值属性](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)