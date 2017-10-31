---
title: "Imports 语句 （.NET Namespace 和类型） |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Imports
- imports
dev_langs:
- VB
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
caps.latest.revision: 40
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
ms.openlocfilehash: 393f3e9a264817d8658585267c954d973290530a
ms.lasthandoff: 03/13/2017

---
# <a name="imports-statement-net-namespace-and-type"></a>Imports 语句（.NET 命名空间和类型）
使类型引用而无需命名空间限定的名称。  
  
## <a name="syntax"></a>语法  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`aliasname`|可选。 *导入别名*或名称时所依据的代码可以指`namespace`而不是完全限定字符串。 请参阅[声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`namespace`|必需。 正在导入的命名空间完全限定的名称。 可以将命名空间的字符串嵌套到任意级别。|  
|`element`|可选。 命名空间中声明的编程元素的名称。 可以是任何容器元素。|  
  
## <a name="remarks"></a>备注  
 `Imports`语句使给定的命名空间直接引用中包含的类型。  
  
 你可以提供单个命名空间名称或嵌套的命名空间的字符串。 每个嵌套的命名空间从下一步的更高级别命名空间由句点分隔 (`.`)，如下面的示例所示。  
  
 `Imports System.Collections.Generic`  
  
 每个源文件可以包含任意数量的`Imports`语句。 这些必须遵循的任何选项声明，如`Option Strict`语句，并且它们必须先完成任何编程元素声明，如`Module`或`Class`语句。  
  
 您可以使用`Imports`只能在文件级别。 这意味着导入的声明上下文必须是源文件，且不能为命名空间、 类、 结构、 模块、 接口、 过程或块。  
  
 请注意，`Imports`语句不会将其他项目和程序集的元素提供给您的项目。 导入才会对引用的设置的位置。 它只会删除需要限定已可供您的项目的名称。 详细信息，请参阅"导入包含元素"中[对声明的元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
> [!NOTE]
>  您可以定义隐式`Imports`语句通过使用[，项目设计器 (Visual Basic 中) 引用页](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)。 有关详细信息，请参阅[如何︰ 添加或删除已导入命名空间 (Visual Basic 中)](http://msdn.microsoft.com/library/44cebec3-0ea0-47c2-8406-4edeab6a997e)。  
  
## <a name="import-aliases"></a>导入别名  
 *导入别名*定义命名空间或类型的别名。 当您需要使用一个或多个命名空间中声明同名的项时，导入别名非常有用。 有关详细信息和示例，请参阅"限定元素名称"[对声明的元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
 不应声明某一成员在模块级别与同名`aliasname`。 如果这样做，Visual Basic 编译器将使用`aliasname`只能用于声明的成员，而不再将其识别为导入别名。  
  
 虽然声明导入别名使用的语法类似的用于导入 XML 命名空间前缀，则结果将不同。 导入别名可以用作在代码中，表达式，而 XML 命名空间前缀可以用作只能在 XML 文本或 XML 轴属性中前缀为限定的元素或属性名称。  
  
### <a name="element-names"></a>元素名称  
 如果您提供`element`，它必须表示*容器元素*，也就是说，可以包含其他元素的编程元素。 容器元素包括类、 结构、 模块、 接口和枚举。  
  
 所提供的元素的作用域`Imports`语句取决于是否指定`element`。 如果只指定`namespace`，所有具有唯一名为该命名空间的成员和该命名空间内的容器元素的成员，是无需限定即可。 如果同时指定了`namespace`和`element`，仅该元素的成员是无需限定即可。  
  
## <a name="example"></a>示例  
 下面的示例返回在 C:\ 目录中的所有文件夹使用<xref:System.IO.DirectoryInfo>类。</xref:System.IO.DirectoryInfo>  
  
 没有代码`Imports`语句的文件的顶部。 因此， `DirectoryInfo`， <xref:System.Text.StringBuilder>，和<xref:Microsoft.VisualBasic.ControlChars.CrLf>是所有完全限定的命名空间名称的引用。</xref:Microsoft.VisualBasic.ControlChars.CrLf> </xref:System.Text.StringBuilder>  
  
 [!code-vb[VbVbalrStatements #&152;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_1.vb)]  
  
## <a name="example"></a>示例  
 下面的示例包含`Imports`被引用的命名空间的语句。 因此，类型不需要是完全限定的命名空间。  
  
 [!code-vb[VbVbalrStatements #&153;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_2.vb)]  
  
 [!code-vb[VbVbalrStatements #&154;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_3.vb)]  
  
## <a name="example"></a>示例  
 下面的示例包含`Imports`语句创建别名的被引用的命名空间。 类型的别名进行限定。  
  
 [!code-vb[VbVbalrStatements #&155;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_4.vb)]  
  
 [!code-vb[VbVbalrStatements #&156;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_5.vb)]  
  
## <a name="example"></a>示例  
 下面的示例包含`Imports`语句创建别名的引用的类型。 使用别名以指定的类型。  
  
 [!code-vb[VbVbalrStatements #&157;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_6.vb)]  
  
 [!code-vb[VbVbalrStatements #&158;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_7.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句 (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
