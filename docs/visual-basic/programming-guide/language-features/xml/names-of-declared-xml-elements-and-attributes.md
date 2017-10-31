---
title: "声明的 XML 元素和特性 (Visual Basic 中) 的名称 |Microsoft 文档"
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
- declarations [XML in Visual Basic]
- element names [XML in Visual Basic]
- names in XML literals
- attribute names [XML in Visual Basic]
- XML literals [Visual Basic], element names
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
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
ms.openlocfilehash: ed8ecf69170acf9745a4038975e7e3421722d52d
ms.lasthandoff: 03/13/2017

---
# <a name="names-of-declared-xml-elements-and-attributes-visual-basic"></a>已声明的 XML 元素和特性的名称 (Visual Basic)
本主题提供了[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]命名 XML 元素和属性在 XML 文本中的准则。  在 XML 文本中，可以指定本地名称或限定的名。 限定的名称由 XML 命名空间前缀、 冒号和本地名称组成。 有关 XML 命名空间前缀的详细信息，请参阅[XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## <a name="rules"></a>规则  
 本地名称为元素或属性中的[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]必须遵守以下规则。  
  
-   它可以开始使用命名空间。 它必须以字母字符或下划线开头 (`_`)。  
  
-   它必须包含仅字母字符、 十进制数字、 下划线、 句点 （.） 和连字符 （-）。  
  
-   它不得超过 1024 个字符长。  
  
-   出现在名称中的冒号指示命名空间划分。 因此，您可以使用冒号只能用于指定特定名称的 XML 命名空间。  
  
 此外，您应该遵守以下准则。  
  
-   XML 1.0 规范保留字符串的区分大小写"xml"开头的所有名称。 因此，不要使用这类名称用作元素和属性名称。  
  
### <a name="name-length-guidelines"></a>名称长度原则  
 在实践中，名称应尽可能短时仍然能够清楚地标识该元素的特性。 这可以提高您的代码的可读性并降低行长度和源文件大小。  
  
 但是，您的名称不应为太短，它不会不充分描述的元素或您的代码如何使用它。 这是代码的重要的可读性。 如果其他人正试图了解它，或者如果您自己正在寻求通过它您撰写后很长时间，相应的元素名称可以节省时间。  
  
## <a name="case-sensitivity-in-names"></a>在名称中的区分大小写  
 XML 元素名称是区分大小写。 这意味着当[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器在比较两个不同的只有字母大小写的名称，会将其解释为不同的名称。 例如，但它可解释`ABC`和`abc`为引用不同的元素。  
  
## <a name="xml-namespaces"></a>XML 命名空间  
 在创建一个 XML 元素文本时，可以指定元素名称的 XML 命名空间前缀。 有关详细信息，请参阅[XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)
