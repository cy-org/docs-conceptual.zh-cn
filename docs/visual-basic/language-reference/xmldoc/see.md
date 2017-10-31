---
title: "&lt;see&gt; (Visual Basic) | Microsoft Docs"
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
  - "<see> XML 标记"
  - "see XML 标记"
ms.assetid: 7e18f60b-ef4a-4678-a797-5eb918635ca9
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;see&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定到另一成员的链接。  
  
## 语法  
  
```  
<see cref="member"/>  
```  
  
#### 参数  
 `member`  
 对可以通过当前编译环境进行调用的成员或字段的引用。  编译器检查给定的代码元素是否存在，并将 `member` 传递给输出 XML 中的元素名称。  `member` 必须位于双引号 \(" "\) 中。  
  
## 备注  
 使用 `<see>` 标记从文本内指定链接。  使用 [\<seealso\>](../../../visual-basic/language-reference/xmldoc/seealso.md) 指示希望在“请参见”一节中出现的文本。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 本示例使用 `UpdateRecord` 备注部分中的 `<see>` 标记来引用 `DoesRecordExist` 方法。  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/see_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)