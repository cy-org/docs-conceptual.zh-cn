---
title: "如何：访问 XML 后代元素 (Visual Basic) | Microsoft Docs"
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
  - "子代轴属性 [Visual Basic]"
  - "XML [Visual Basic], 访问"
  - "XML 轴 [Visual Basic], 降序"
  - "XML 子代轴属性 [Visual Basic]"
ms.assetid: aabfa258-4112-4e7e-bab9-403f96072ef7
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：访问 XML 后代元素 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本示例演示如何使用子代轴属性来访问具有指定名称并且包含在 XML 元素之下的所有 XML 元素。  具体而言，该示例使用 `Value` 属性获取 `name` 子代轴属性所返回的集合中的第一个元素的值。  `name` 子代轴属性获取 `contacts` 对象所含的所有名为 `name` 的元素。  本示例还使用 `phone` 子代轴属性来访问 `contacts` 对象所含的所有名为 `phone` 的子代。  
  
## 示例  
 [!code-vb[VbXMLSamples#31](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-access-xml-descendant-elements_1.vb)]  
  
## 编译代码  
 此示例需要：  
  
-   对 <xref:System.Xml.Linq> 命名空间的引用。  
  
## 请参阅  
 <xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=fullName>   
 [XML 后代轴属性](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [XML 值属性](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)   
 [在 Visual Basic 中访问 XML](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)