---
title: "/doc |Microsoft 文档"
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
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
caps.latest.revision: 18
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
ms.openlocfilehash: 1054eb256eb7670ee0454b02fc094e0306c1218d
ms.lasthandoff: 03/13/2017

---
# <a name="doc"></a>/doc
将文档注释处理到一个 XML 文件中。  
  
## <a name="syntax"></a>语法  
  
```  
/doc[+ | -]  
' -or-  
/doc:file  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`+` &#124; `-`|可选。 指定 +，或只是`/doc`，使编译器生成文档信息，并将其放在一个 XML 文件。 指定`-`等同于未指定`/doc`，导致不创建任何文档信息。|  
|`file`|如果使用 `/doc:`，则是必需的。 指定输出 XML 文件中，填入编译源代码文件中的注释。 如果文件名包含空格，将名称括起来加上引号 ("")。|  
  
## <a name="remarks"></a>备注  
 `/doc`选项控制是否编译器生成包含文档注释的 XML 文件。 如果您使用`/doc:``file`语法中，`file`参数指定的 XML 文件的名称。 如果您使用`/doc`或`/doc+`，编译器将从可执行文件或该编译器创建的库中获取 XML 文件名称。 如果您使用`/doc-`或不指定`/doc`选项时，编译器不会创建一个 XML 文件。  
  
 在源代码文件中，文档注释之前可以放置以下定义︰  
  
-   用户定义类型，如[类](../../../visual-basic/language-reference/statements/class-statement.md)或[接口](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   成员，一个字段，例如[事件](../../../visual-basic/language-reference/statements/event-statement.md)，[属性](../../../visual-basic/language-reference/statements/property-statement.md)，[函数](../../../visual-basic/language-reference/statements/function-statement.md)，或[子例程](../../../visual-basic/language-reference/statements/sub-statement.md)。  
  
 若要使用生成的 XML 文件和[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense)功能，但可让你想要支持的程序集相同的 XML 文件的文件名。 请确保 XML 文件与程序集的相同目录中，以便当中引用的程序集[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]项目中，.xml 文件也可以找到。 XML 文档文件则不需要发挥作用的代码在一个项目或项目引用的项目中的 intellisense。  
  
 除非在编译时使用`/target:module`，XML 文件包含标记`<assembly></assembly>`。 这些标记指定包含编译输出文件的程序集清单的文件的名称。  
  
 请参阅[XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)从您的代码中的注释生成文档的方法。  
  
|在 Visual Studio 中设置 /doc 集成开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.中的值设置**生成 XML 文档文件**框。|  
  
## <a name="example"></a>示例  
 请参阅[使用 XML 编制文档您代码](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)有关的示例。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [使用 XML 记录代码](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
