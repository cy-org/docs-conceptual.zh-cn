---
title: "如何︰ 使用泛型类 (Visual Basic 中) |Microsoft 文档"
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
- type parameters, defining
- data type arguments, defining
- arguments [Visual Basic], data types
- Of keyword, using
- generic parameters
- data type parameters
- generics [Visual Basic], about generics
- data types [Visual Basic], as parameters
- data types [Visual Basic], as arguments
- parameters, type
- types [Visual Basic], generic
- parameters, generic
- generics [Visual Basic], creating generic types
- data type arguments
- parameters, data type
- data type parameters, defining
- type arguments, defining
- arguments [Visual Basic], type
ms.assetid: 242dd2a6-86c4-4ce7-83f2-f2661803f752
caps.latest.revision: 24
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: eeb55be1c368e9ca80ab94de814a5e2ba9bc9f1f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-a-generic-class-visual-basic"></a>如何：使用泛型类 (Visual Basic)
采用 *类型参数* 的类称为 *泛型类*。 如果使用一个泛型类，则可以通过为每个形参提供 *类型实参* ，从该类生成 *构造类* 。 随后可以声明构造类类型的一个变量，可以创建构造类的实例并将它分配给该变量。  
  
 除了类之外，你还可以定义和使用泛型结构、接口、过程和委托。  
  
 下面的过程采用在 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] 中定义的一个泛型类，并且通过它创建一个实例。  
  
### <a name="to-use-a-class-that-takes-a-type-parameter"></a>使用采用类型参数的类  
  
1.  在开始您的源文件时，包括[Imports 语句 （.NET Namespace 和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)要导入<xref:System.Collections.Generic?displayProperty=fullName>命名空间。</xref:System.Collections.Generic?displayProperty=fullName> 这使您可以引用的<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>类，而不必完全限定它以将其与其他队列类，如<xref:System.Collections.Queue?displayProperty=fullName>。</xref:System.Collections.Queue?displayProperty=fullName>区分开来</xref:System.Collections.Generic.Queue%601?displayProperty=fullName>  
  
2.  以正常方式创建对象，但是紧接在类名之后添加 `(Of` `type``)` 。  
  
     下面的示例使用同一个类 (<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>) 创建保存不同的数据类型的项的两个队列对象。</xref:System.Collections.Generic.Queue%601?displayProperty=fullName> 它将项添加到每个队列末尾，然后从每个队列的前面删除并显示项。  
  
     [!code-vb[VbVbalrDataTypes #&9;](../../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/how-to-use-a-generic-class_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/12a7a7h3)   
 [Of](../../../../visual-basic/language-reference/statements/of-clause.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [如何：定义可对不同数据类型提供相同功能的类](../../../../visual-basic/programming-guide/language-features/data-types/how-to-define-a-class-that-can-provide-identical-functionality.md)   
 [迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)
