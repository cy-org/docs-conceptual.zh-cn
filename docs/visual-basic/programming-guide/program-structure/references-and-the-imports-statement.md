---
title: "引用和 Imports 语句 (Visual Basic 中) |Microsoft 文档"
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
- assemblies [Visual Basic], namespaces
- references, assembly
- namespaces, assemblies
- referencing assemblies
- Imports statement, referencing assemblies
- assemblies [Visual Basic], references
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
caps.latest.revision: 12
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
ms.openlocfilehash: 283a27e7703b31a9aeed8f7e4104e89b7ff78525
ms.lasthandoff: 03/13/2017

---
# <a name="references-and-the-imports-statement-visual-basic"></a>引用和 Imports 语句 (Visual Basic)
您可以通过使外部对象提供到您的项目选择**添加引用**命令**项目**菜单。 中的引用都[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可以指向与类似的类型库但包含的详细信息的程序集。  
  
## <a name="the-imports-statement"></a>Imports 语句  
 程序集包含一个或多个命名空间。 在添加对程序集引用时，您还可以添加`Imports`控制的可见性的模块内的该程序集的命名空间的模块的语句。 `Imports`语句提供了使您可以使用仅需提供的唯一引用的命名空间部分的作用域上下文。  
  
 `Imports`语句具有以下语法︰  
  
 `Imports` [`|``Aliasname` =] `Namespace`  
  
 `Aliasname`是指可用于在代码内导入的命名空间是指一个短名称。 `Namespace`是通过在项目中，定义或通过以前的项目引用的命名空间可通过任何一个`Imports`语句。  
  
 模块可以包含任意数量的`Imports`语句。 它们必须出现在任何之后`Option`语句，如果存在，但在任何其他代码之前。  
  
> [!NOTE]
>  不要混淆项目引用与`Imports`语句或`Declare`语句。 项目引用使得外部对象，例如在程序集中，对象可用于[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]项目。 `Imports`语句用于简化对项目引用的访问，但不提供对这些对象的访问。 `Declare`语句用于声明对外部过程动态链接库 (DLL) 中的引用。  
  
## <a name="using-aliases-with-the-imports-statement"></a>Imports 语句中使用别名  
 `Imports`语句，从而更便于访问类方法通过消除需要显式键入引用的完全限定的名。 别名允许您将更友好的名称分配给只是一个命名空间的一部分。 例如，回车符/换行符将导致在多行上显示的文本单个块的序列是属于<xref:Microsoft.VisualBasic.ControlChars>中的模块<xref:Microsoft.VisualBasic?displayProperty=fullName>命名空间。</xref:Microsoft.VisualBasic?displayProperty=fullName> </xref:Microsoft.VisualBasic.ControlChars> 若要在不带别名程序中使用此常量，您需要键入以下代码︰  
  
 [!code-vb[VbVbalrApplication #&3;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_1.vb)]  
  
 `Imports`语句必须始终为紧接着的前几行`Option`模块中的语句。 下面的代码段演示如何导入并分配给别名<xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName>模块︰</xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName>  
  
 [!code-vb[VbVbalrApplication #&4;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_2.vb)]  
  
 将来对此命名空间的引用可以简短得多︰  
  
 [!code-vb[VbVbalrApplication #&5;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_3.vb)]  
  
 如果`Imports`语句不包括别名，可以在无需限定即可模块中使用的导入的命名空间中定义的元素。 如果指定的别名的名称，它必须用作限定符的名称包含在该命名空间内。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.ControlChars></xref:Microsoft.VisualBasic.ControlChars>   
 <xref:Microsoft.VisualBasic></xref:Microsoft.VisualBasic>   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [如何︰ 创建和使用程序集使用命令行](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
