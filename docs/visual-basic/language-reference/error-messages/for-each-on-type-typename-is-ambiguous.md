---
title: "For Each 类型&lt;typename&gt;&quot; 不明确，因为该类型实现多个 System.Collections.Generic.IEnumerable (Of T) 实例化 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc32096
- bc32096
dev_langs:
- VB
helpviewer_keywords:
- BC32096
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
caps.latest.revision: 7
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
ms.openlocfilehash: 6177b48cdc3bc4085cecb6d73c164684ef1c0bc6
ms.lasthandoff: 03/13/2017

---
# <a name="39for-each39-on-type-39lttypenamegt39-is-ambiguous-because-the-type-implements-multiple-instantiations-of-39systemcollectionsgenericienumerableof-t39"></a>For Each 类型&lt;typename&gt;' 不明确，因为该类型实现多个实例化 System.Collections.Generic.IEnumerable (Of T)
一个`For Each`语句指定了多个迭代器变量<xref:System.Collections.IEnumerable.GetEnumerator%2A>方法。</xref:System.Collections.IEnumerable.GetEnumerator%2A>  
  
 迭代器变量必须实现的类型为<xref:System.Collections.IEnumerable?displayProperty=fullName>或<xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>接口之一`Collections`命名空间的[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]。</xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> </xref:System.Collections.IEnumerable?displayProperty=fullName> 它有可能实现多个构造的泛型接口，使用不同的类型参数对每个构造的类。 如果执行此类用于迭代器变量，该变量将包含多个<xref:System.Collections.IEnumerable.GetEnumerator%2A>方法。</xref:System.Collections.IEnumerable.GetEnumerator%2A> 在这种情况下，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不能选择要调用的方法。  
  
 **错误 ID:** BC32096  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   使用[DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md)或[TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md)接口定义的迭代器变量类型转换<xref:System.Collections.IEnumerable.GetEnumerator%2A>你想要使用的方法。</xref:System.Collections.IEnumerable.GetEnumerator%2A>  
  
## <a name="see-also"></a>另请参阅  
 [每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
