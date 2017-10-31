---
title: "unchecked（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- unchecked_CSharpKeyword
- unchecked
dev_langs:
- CSharp
helpviewer_keywords:
- unchecked keyword [C#]
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5878a2412e6c85da85b1a3b8c2a8255b51e67137
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="unchecked-c-reference"></a>unchecked（C# 参考）
`unchecked` 关键字用于取消整型类型的算术运算和转换的溢出检查。  
  
 在未经检查的上下文中，如果表达式生成的值超出目标类型的范围，则不会标记溢出。 例如，由于以下示例中的计算在 `unchecked` 块或表达式中执行，因此将忽略计算结果对于整数而言过大的事实，并且向 `int1` 赋予值 -2,147,483,639。  
  
 [!code-cs[csrefKeywordsChecked#5](../../../csharp/language-reference/keywords/codesnippet/CSharp/unchecked_1.cs)]  
  
 如果删除 `unchecked` 环境，会发生编译错误。 由于表达式的所有项都是常量，因此可在编译时检测到溢出。  
  
 在编译时和运行时，默认不检查包含非常数项的表达式。 请参阅[启用检查](../../../csharp/language-reference/keywords/checked.md)，获取有关使用启用了检查的环境的信息。  
  
 由于检查溢出需要时间，因此在没有溢出风险的情况下使用取消检查的代码可能会提高性能。 但是，如果存在溢出的可能，则应使用启用了检查的环境。  
  
## <a name="example"></a>示例  
 此示例演示如何使用 `unchecked`关键字。  
  
 [!code-cs[csrefKeywordsChecked#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/unchecked_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [Checked 和 Unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)   
 [checked](../../../csharp/language-reference/keywords/checked.md)

