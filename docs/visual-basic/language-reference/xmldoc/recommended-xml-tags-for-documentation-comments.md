---
title: "建议的文档注释 (Visual Basic 中) 的 XML 标记 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.XmlDocComment
dev_langs:
- VB
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
caps.latest.revision: 14
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
ms.openlocfilehash: c6a47c12bc24864ef6ac9f80054becad98ec97f1
ms.lasthandoff: 03/13/2017

---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>建议的用于文档注释的 XML 标记 (Visual Basic)
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器可以处理你的代码与 XML 文件中的文档注释。 其他工具可用于 XML 文件处理成文档。  
  
 XML 注释可以在代码构造，如类型和类型成员。 对于分部类型只能有一个类型的一部分可以有 XML 注释，尽管没有对其成员的注释没有限制。  
  
> [!NOTE]
>  文档注释不能应用于命名空间。 原因是一个命名空间可以跨多个程序集，并不是所有程序集必须加载一次。  
  
 编译器会处理任何为有效的 XML 标记。 下列标记提供用户文档中的常用的功能。  
  
||||  
|---|---|---|  
|[\<c&1;>](../../../visual-basic/language-reference/xmldoc/c.md)|[\<代码&1;>](../../../visual-basic/language-reference/xmldoc/code.md)|[\<示例&1;>](../../../visual-basic/language-reference/xmldoc/example.md)|  
|[\<异常&1;>](../../../visual-basic/language-reference/xmldoc/exception.md) <sup>1</sup>|[\<包括&1;>](../../../visual-basic/language-reference/xmldoc/include.md) <sup>1</sup>|[\<list>](../../../visual-basic/language-reference/xmldoc/list.md)|  
|[\<para&1;>](../../../visual-basic/language-reference/xmldoc/para.md)|[\<param>](../../../visual-basic/language-reference/xmldoc/param.md) <sup>1</sup>|[\<paramref&1;>](../../../visual-basic/language-reference/xmldoc/paramref.md)|  
|[\<权限&1;>](../../../visual-basic/language-reference/xmldoc/permission.md) <sup>1</sup>|[\<备注&1;>](../../../visual-basic/language-reference/xmldoc/remarks.md)|[\<返回&1;>](../../../visual-basic/language-reference/xmldoc/returns.md)|  
|[\<see>](../../../visual-basic/language-reference/xmldoc/see.md) <sup>1</sup>|[\<seealso&1;>](../../../visual-basic/language-reference/xmldoc/seealso.md) <sup>1</sup>|[\<摘要&1;>](../../../visual-basic/language-reference/xmldoc/summary.md)|  
|[\<typeparam&1;>](../../../visual-basic/language-reference/xmldoc/typeparam.md) <sup>1</sup>|[\<值&1;>](../../../visual-basic/language-reference/xmldoc/value.md)||  
  
 (<sup>1</sup>编译器验证语法。)  
  
> [!NOTE]
>  如果要尖括号的文档注释文本中显示时，使用`<`和`>`。 例如，字符串`"<text in angle brackets>"`将显示为`<text in angle``brackets>`。  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)   
 [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
