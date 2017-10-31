---
title: "?: 运算符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- ?:_CSharpKeyword
- ?_CSharpKeyword
- :_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- '?: operator [C#]'
- conditional operator (?:) [C#]
ms.assetid: e83a17f1-7500-48ba-8bee-2fbc4c847af4
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 794ff53fe471ef23163503f59599b528df127e2e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="-operator-c-reference"></a>?: 运算符（C# 参考）
条件运算符 (`?:`) 根据 Boolean 表达式的值返回两个值之一。 下面是条件运算符的语法。  
  
```  
condition ? first_expression : second_expression;  
```  
  
## <a name="remarks"></a>备注  
 `condition` 的计算结果必须为 `true` 或 `false`。 如果 `condition` 为 `true`，则将计算 `first_expression` 并使其成为结果。 如果 `condition` 为 `false`，则将计算 `second_expression` 并使其成为结果。 只计算两个表达式之一。  
  
 `first_expression` 和 `second_expression` 的类型必须相同，或者必须存在从一种类型到另一种类型的隐式转换。  
  
 你可通过使用条件运算符表达可能更确切地要求 `if-else` 构造的计算。 例如，以下代码首先使用 `if` 语句，然后使用条件运算符将整数分类为正整数或负整数。  
  
```  
int input = Convert.ToInt32(Console.ReadLine());  
string classify;  
  
// if-else construction.  
if (input > 0)  
    classify = "positive";  
else  
    classify = "negative";  
  
// ?: conditional operator.  
classify = (input > 0) ? "positive" : "negative";  
```  
  
 条件运算符为右联运算符。 表达式 `a ? b : c ? d : e` 作为 `a ? b : (c ? d : e)` 而非 `(a ? b : c) ? d : e` 进行计算。  
  
 无法重载条件运算符。  
  
## <a name="example"></a>示例  
 [!code-cs[csRefOperators#41](../../../csharp/language-reference/operators/codesnippet/CSharp/conditional-operator_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 运算符](../../../csharp/language-reference/operators/index.md)   
 [if-else](../../../csharp/language-reference/keywords/if-else.md)   
 [?. 和 ? 运算符](../../../csharp/language-reference/operators/null-conditional-operators.md)   
 [??运算符](../../../csharp/language-reference/operators/null-conditional-operator.md)

