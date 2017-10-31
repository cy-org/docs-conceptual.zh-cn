---
title: "Namespace 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Namespace"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "声明, 命名空间"
  - "声明命名空间, 语法"
  - "Namespace 语句"
  - "命名空间, 声明"
  - "命名空间, 嵌套"
  - "命名空间, 根"
  - "根命名空间"
ms.assetid: a31fbd95-9ace-4c3d-bbb1-51222a2272b2
caps.latest.revision: 39
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 39
---
# Namespace 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明命名空间的名称，并使跟在声明后面的源代码将在该命名空间中进行编译。  
  
## 语法  
  
```  
Namespace [Global.] { name | name.name }  
    [ componenttypes ]  
End Namespace  
```  
  
## 部件  
 Global  
 可选。  可以定义命名空间在项目的根命名空间之外。  请参见 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)。  
  
 `name`  
 必选。  标识命名空间的唯一名称。  必须是有效的 Visual Basic 标识符。  有关更多信息，请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
 `componenttypes`  
 可选。  组成命名空间的元素。  其中包括，但是，并不限于，枚举、结构、接口、类、模块、委托和其他命名空间。  
  
 `End Namespace`  
 终止 `Namespace` 块。  
  
## 备注  
 命名空间用作组织系统。  它们提供一种方法，用于对向其他程序和应用程序公开的编程元素进行分类和呈现。  请注意命名空间不是 *类型* 上来讲，类或结构是 \- 您不能声明编程元素具有命名空间的数据类型。  
  
 在 `Namespace` 语句后声明的所有编程元素均属于该命名空间。  Visual Basic 不断地将元素编译到最后一个声明的命名空间中，直到它遇到 `End Namespace` 语句或另一个 `Namespace` 语句。  
  
 如果已定义某个命名空间，则即使在项目之外，也可以向该命名空间添加编程元素。  为此，使用一个 `Namespace` 语句处理 Visual Basic 生成元素添加到该命名空间。  
  
 只能在文件或命名空间级别使用 `Namespace` 语句。  这意味着命名空间的声明上下文必须是源文件或另一个命名空间，而不能是类、结构、模块、接口或过程。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 可以在一个命名空间中声明另一个命名空间。  对于可以声明的嵌套级别并无严格的限制，但请记住，当其他代码访问在最内部的命名空间中声明的元素时，它必须使用一个包含嵌套层次结构中的所有命名空间名称的限定字符串。  
  
## 访问级别  
 命名空间视为，就好像它们具有一个 `Public` 访问级别。  命名空间可从以下位置访问：同一项目中任何位置的代码、引用该项目的其他项目以及从该项目生成的任何程序集。  
  
 在命名空间级别声明的编程元素（在命名空间中有意义，但在任何其他元素内部无意义）可以具有 `Public` 或 `Friend` 访问级别。  如果未指定此类元素的访问级别，则默认为 `Friend`。  可以在命名空间级别声明的元素包括类、结构、模块、接口、枚举和委托。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
## 根命名空间  
 项目中的所有命名空间名称均基于根命名空间。  Visual Studio 将您的项目名称指定为项目中所有代码的默认根命名空间。  例如，如果项目名为 `Payroll`，则它的编程元素均属于 `Payroll` 命名空间。  如果声明 `Namespace funding`，则该命名空间的全名为 `Payroll.funding`。  
  
 如果想在 `Namespace` 语句中指定现有的命名空间（如在泛型列表类示例中那样），则可以将根命名空间设置为空值。  为此，请在**“项目”**菜单中单击**“项目属性”**，然后清除**“根命名空间”**条目，使此框为空。  如果在泛型列表类示例中不这样做，Visual Basic 编译器会将 `System.Collections.Generic` 用作 `Payroll` 项目中的新命名空间，全名为 `Payroll.System.Collections.Generic`。  
  
 另外，也可以使用 `Global` 关键字来引用在项目外定义的命名空间的元素。  这样可使您将项目名称留用作根命名空间。  这会减少无意中将您的编程元素与现有命名空间的编程元素混在一起的机率。  有关更多信息，请参见中 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)的 “在完全限定名称的全局关键字”一节。  
  
 `Global` 关键字还可用于 Namespace 语句。  这使您可以定义命名空间在项目的根命名空间之外。  有关更多信息，请参见中 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)的 “Namespace 语句的全局关键字”一节。  
  
 **疑难解答。**根命名空间可能导致命名空间名称发生意外的串联。  如果引用在项目外定义的命名空间，Visual Basic 编译器可将它们解释为根命名空间中的嵌套命名空间。  在这种情况下，编译器无法识别已在外部命名空间中定义的任何类型。  若要避免此问题，设置根命名空间为一个 null 值 \(如 “根命名空间所述，”或使用 `Global` 关键字对外部命名空间的访问元素。  
  
## 特性和修饰符  
 无法将特性应用于命名空间。  特性向程序集的元数据提供信息，这对于源分类器（如命名空间）并无意义。  
  
 无法将任何访问或过程修饰符或任何其他修饰符应用于命名空间。  由于命名空间并非类型，因此这些修饰符对于它并无意义。  
  
## 示例  
 下面的示例声明两个命名空间，其中一个嵌套在另一个中。  
  
 [!code-vb[VbVbalrStatements#43](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_1.vb)]  
  
## 示例  
 下面的示例在一行上声明多个嵌套命名空间，其效果与上一个示例等同。  
  
 [!code-vb[VbVbalrStatements#41](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_2.vb)]  
  
## 示例  
 下面的示例访问在前面的示例中定义的类。  
  
 [!code-vb[VbVbalrStatements#42](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/namespace-statement_3.vb)]  
  
## 示例  
 下面的示例定义一个新的泛型列表类的主干，并将它添加到 <xref:System.Collections.Generic?displayProperty=fullName> 命名空间中。  
  
```vb  
Namespace System.Collections.Generic  
    Class specialSortedList(Of T)  
        Inherits List(Of T)  
        ' Insert code to define the special generic list class.  
    End Class  
End Namespace  
```  
  
## 请参阅  
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)