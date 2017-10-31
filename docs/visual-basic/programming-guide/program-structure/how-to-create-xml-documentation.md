---
title: "如何︰ 在 Visual Basic 中创建 XML 文档 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- XML comments
- XML documentation, creating
ms.assetid: 27b5b06c-09b9-496a-8245-f9542d846230
caps.latest.revision: 17
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 363a20c0fce05566b61e764d05932a9dfb779f90
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-xml-documentation-in-visual-basic"></a>如何：在 Visual Basic 中创建 XML 文档
此示例演示如何将 XML 文档注释添加到您的代码。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-xml-documentation-for-a-type-or-member"></a>若要创建的类型或成员的 XML 文档  
  
1.  在**代码编辑器**，将鼠标光标放置在上方你想要创建文档的类型或成员的行。  
  
2.  类型`'''`（三个单引号）。  
  
     在添加该类型或成员的 XML 主干**代码编辑器**。  
  
3.  添加相应的标记之间的描述性信息。  
  
    > [!NOTE]
    >  如果您添加的 XML 文档块内的其他行，每行必须以与`'''`。  
  
4.  添加新的 XML 文档注释中使用该类型或成员的附加代码。  
  
     IntelliSense 显示中的文本\<摘要&1;> 标记的类型或成员。  
  
5.  编译代码以生成包含文档注释的 XML 文件。 有关详细信息，请参阅[/doc](../../../visual-basic/reference/command-line-compiler/doc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 XML 将代码文档化](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)   
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)
