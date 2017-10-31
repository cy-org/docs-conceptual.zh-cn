---
title: "XML 文本和 XML 1.0 规范 (Visual Basic 中) |Microsoft 文档"
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
- XML literals [Visual Basic], XML 1.0 specification
ms.assetid: 46f046e5-293c-41a3-b893-4e5f6e32e78a
caps.latest.revision: 13
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
ms.openlocfilehash: f6e52a99625d5e6f0ed7db439e1e633c3b0bb0a7
ms.lasthandoff: 03/13/2017

---
# <a name="xml-literals-and-the-xml-10-specification-visual-basic"></a>XML 文本和 XML 1.0 规范 (Visual Basic)
中的 XML 文本语法[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]支持大部分可扩展标记语言 (XML) 1.0 规范。 有关 XML 1.0 规范的详细信息，请参阅[可扩展标记语言 (XML) 1.0](http://go.microsoft.com/fwlink/?LinkId=73927) W3C 网站上。  
  
## <a name="what-visual-basic-does-not-support"></a>Visual Basic 不支持的新增功能  
  
-   XML 文本不能包含文档类型定义 (DTD)。  
  
-   XML 文档文本必须以 XML 文档声明开头。  
  
-   XML 文本不能包含在同一行超过 65535 个字符。  
  
-   XML 命名空间前缀、 元素名称和特性名称不能包含超过 1024 个字符。  
  
## <a name="extra-features-that-visual-basic-supports"></a>Visual Basic 支持的额外功能  
  
-   允许文档和元素的文本中的嵌入式的表达式语法不是有效的 XML。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 文档文本](../../../../visual-basic/language-reference/xml-literals/xml-document-literal.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
