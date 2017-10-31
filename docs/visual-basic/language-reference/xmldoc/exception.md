---
title: "&lt;exception&gt; (Visual Basic) | Microsoft Docs"
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
  - "<exception> XML 标记"
  - "exception XML 标记"
ms.assetid: c0517549-171e-4dae-ab88-a9c1700b6eee
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;exception&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定可引发哪些异常。  
  
## 语法  
  
```  
<exception cref="member">description</exception>  
```  
  
#### 参数  
 `member`  
 对可从当前编译环境中获取的异常的引用。  编译器检查到给定异常存在后，将 `member` 转换为输出 XML 中的规范化元素名称。  `member` 必须位于双引号 \(" "\) 中。  
  
 `description`  
 说明。  
  
## 备注  
 使用 `<exception>` 标记指定可引发哪些异常。  该标记应用于方法定义。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 此示例使用 `<exception>` 标记描述 `IntDivide` 函数可引发的异常。  
  
 [!code-vb[VbVbcnXmlDocComments#3](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/exception_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)