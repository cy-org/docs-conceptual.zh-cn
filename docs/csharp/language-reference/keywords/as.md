---
title: "as（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- as_CSharpKeyword
- as
dev_langs:
- CSharp
helpviewer_keywords:
- type conversion [C#], as keyword
- as keyword [C#]
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
caps.latest.revision: 24
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
ms.openlocfilehash: 7a55c696ac295eee8d5d35ed56038f3c4a90b215
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="as-c-reference"></a>as（C# 参考）
可以使用 `as` 运算符在符合的引用类型或[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)之间执行某些类型的转换。 以下代码显示一个示例。  
  
 [!code-cs[csrefKeywordsOperator#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_1.cs)]  
  
## <a name="remarks"></a>备注  
 `as` 运算符类似于转换运算。 但是，如果无法进行转换，则 `as` 会返回 `null`，而不是引发异常。 请看下面的示例：  
  
```  
expression as type  
```  
  
 该代码等效于以下表达式，但 `expression` 变量仅进行一次计算。  
  
```  
expression is type ? (type)expression : (type)null  
```  
  
 请注意，`as` 运算符仅执行引用转换、可以为 null 的转换和装箱转换。 `as` 运算符无法执行其他转换，例如用户定义的转换，应使用转换表达式执行此转换。  
  
## <a name="example"></a>示例  
 [!code-cs[csrefKeywordsOperator#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/as_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [?: 运算符](../../../csharp/language-reference/operators/conditional-operator.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)

