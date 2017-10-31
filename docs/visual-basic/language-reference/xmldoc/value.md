---
title: "&lt;value&gt; (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "<value> XML 标记"
  - "值 XML 标记"
ms.assetid: 0b84b02e-9e6d-41b5-a926-0d5dc76dacb5
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;value&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定属性的说明。  
  
## 语法  
  
```  
<value>property-description</value>  
```  
  
#### 参数  
 `property-description`  
 属性的说明。  
  
## 备注  
 使用 `<value>` 标记说明属性。  请注意，当在 Visual Studio 开发环境中通过代码向导添加属性时，它将会为新属性添加 [\<summary\>](../../../visual-basic/language-reference/xmldoc/summary.md) 标记。  然后，应该手动添加 `<value>` 标记以描述该属性所表示的值。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 本示例使用 `<value>` 标记描述 `Counter` 属性所存储的值。  
  
 [!code-vb[VbVbcnXmlDocComments#1](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/value_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)