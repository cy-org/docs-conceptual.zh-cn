---
title: "&lt;list&gt; (Visual Basic) | Microsoft Docs"
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
  - "<description> XML 标记"
  - "<item> XML 标记"
  - "<list> XML 标记"
  - "<listheader> XML 标记"
  - "<term> XML 标记"
  - "description XML 标记"
  - "item XML 标记"
  - "list XML 标记"
  - "listheader XML 标记"
  - "term XML 标记"
ms.assetid: ec35fced-d58e-4520-a764-0691256e014b
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &lt;list&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

定义列表或表。  
  
## 语法  
  
```  
<list type="type">  
   <listheader>  
      <term>term</term>  
      <description>description</description>  
   </listheader>  
   <item>  
      <term>term</term>  
      <description>description</description>  
   </item>  
</list>  
```  
  
#### 参数  
 `type`  
 列表类型。  必须是表示项目符号列表的“项目符号”、表示编号列表的“编号”或表示两列表格的“表”。  
  
 `term`  
 仅在 `type` 为“table”时使用。要定义的术语，将在说明标记中定义。  
  
 `description`  
 当 `type` 为“bullet”或“number”时，`description` 是列表中的一项。当 `type` 为“table”时，`description` 是对 `term` 的定义。  
  
## 备注  
 `<listheader>` 块用于对表或定义列表的标题进行定义。  定义表时，只需提供标题的 `term` 一项。  
  
 列表中的每一项都用一个 `<item>` 块来描述。  创建定义列表时，`term` 和 `description` 都必须指定。  但是，对于表、项目符号列表或编号列表，只需提供 `description` 一项。  
  
 列表或表所拥有的 `<item>` 块数可以根据需要而定。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 本示例使用 `<list>` 标记定义备注部分中的项目符号列表。  
  
 [!code-vb[VbVbcnXmlDocComments#5](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/list_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)