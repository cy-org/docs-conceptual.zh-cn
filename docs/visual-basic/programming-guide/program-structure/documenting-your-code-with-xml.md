---
title: "使用 XML (Visual Basic 中) 将代码文档化 |Microsoft 文档"
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
- XML, documenting code
- XML comments, Visual Basic
- Visual Basic code, documenting with XML
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2ec4907ff96a0861f97de21bdf45662c558d0a95
ms.lasthandoff: 03/13/2017

---
# <a name="documenting-your-code-with-xml-visual-basic"></a>使用 XML 将代码文档化 (Visual Basic)
在[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，您可以记录使用 XML 将代码  
  
## <a name="xml-documentation-comments"></a>XML 文档注释  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供了一种简单的方法来自动创建项目的 XML 文档。 您可以自动生成的 XML 主干的类型和成员，，然后提供摘要、 描述性文档每个参数，并将其他备注。 与相应的安装程序，到 XML 文件与您的项目和.xml 扩展名同名自动发出 XML 文档。 有关详细信息，请参阅[/doc](../../../visual-basic/reference/command-line-compiler/doc.md)。  
  
 可以使用或其他操作以 XML 形式的 XML 文件。 此文件位于您的项目的输出.exe 或.dll 文件所在的目录中。  
  
 XML 文档开头`'''`。 这些注释的处理有一些限制︰  
  
-   文档必须是格式正确 XML。 如果 XML 的格式不正确，则会生成警告和文档文件将包含条注释，指出遇到错误。  
  
-   开发人员可以随意创建其自己的标记集。 没有一组建议的标记 （请参见本主题中的"相关章节"）。 建议的标记的一些具有特殊含义︰  
  
    -   \<Param&1;> 标记用来描述的参数。 如果使用，编译器将验证该参数存在并在文档中描述了所有参数。 如果验证失败，编译器会发出警告。  
  
    -   `cref`属性可以附加到任何标记，以提供对代码元素的引用。 编译器将验证存在此代码元素。 如果验证失败，编译器会发出警告。 编译器还将考虑所有`Imports`语句在查找中描述的类型时`cref`属性。  
  
    -   \<摘要&1;> IntelliSense 中将使用标记[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]以显示有关类型或成员的其他信息。  
  
## <a name="related-sections"></a>相关章节  
 有关创建带有文档注释的 XML 文件的详细信息，请参阅以下主题︰  
  
-   [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)  
  
-   [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)  
  
-   [处理 XML 文件](../../../visual-basic/programming-guide/program-structure/processing-the-xml-file.md)  
  
-   [如何：创建 XML 文档](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)  
  
-   [Visual Studio 中的 XML 工具](https://docs.microsoft.com/visualstudio/xml-tools/xml-tools-in-visual-studio)  
  
## <a name="see-also"></a>另请参阅  
 [使用 Visual Basic 开发应用程序](../../../visual-basic/developing-apps/index.md)   
 [Visual Basic 编程指南](../../../visual-basic/programming-guide/index.md)
