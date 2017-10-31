---
title: "类型 &quot;&lt;typename&gt;&quot; 未定义 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30002
- bc30002
dev_langs:
- VB
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
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
ms.openlocfilehash: 09aa7c535fd5e17ddcd0e743fb5ec17ebadd4f7d
ms.lasthandoff: 03/13/2017

---
# <a name="type-39lttypenamegt39-is-not-defined"></a>类型 '&lt;typename&gt;' 未定义
该语句进行了引用未定义的类型。 您可以如声明语句中定义类型`Enum`， `Structure`， `Class`，或`Interface`。  
  
 **错误 ID:** BC30002  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   确保类型定义和它的引用都使用相同的拼写。  
  
-   确保该类型定义为引用可访问。 例如，如果类型在另一个模块，并且已被声明为`Private`、 将该类型定义移到引用的模块或将其声明`Public`。  
  
-   请确保该类型的命名空间未在项目中重新定义。 如果是，使用`Global`关键字用于完全限定类型名称。 例如，如果一个项目定义命名空间名为`System`、<xref:System.Object?displayProperty=fullName>无法访问类型，除非它是使用完全限定`Global`关键字︰ `Global.System.Object`。</xref:System.Object?displayProperty=fullName>  
  
-   如果定义的类型，但未注册的对象库或在其中定义的类型库[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，请单击**添加引用**上**项目**菜单上，然后选择适当的对象库或类型库。  
  
-   确保该类型的程序集中的目标.NET Framework 配置文件的一部分。 有关详细信息，请参阅[疑难解答.NET Framework 目标错误](https://docs.microsoft.com/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors)。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [管理项目中的引用](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)
