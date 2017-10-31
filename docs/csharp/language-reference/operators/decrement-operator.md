---
title: "-- 运算符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- --_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- -- operator [C#]
- decrement operator (--) [C#]
ms.assetid: 6b9cfe86-63c7-421f-9379-c9690fea8720
caps.latest.revision: 17
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
ms.openlocfilehash: 100e68f3b07164b0cfb398a32f47137f2726943f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="---operator-c-reference"></a>-- 运算符（C# 参考）
减量运算符 (`--`) 按 1 递减其操作数。 减量运算符可以在其操作数之前或之后出现：`--variable` 和 `variable--`。 第一种形式是前缀递减操作。 操作的结果是操作数递减“后”的值。 第二种形式是后缀递减操作。 操作的结果是操作数递减“前”的值。  
  
## <a name="remarks"></a>备注  
 数值和枚举类型具有预定义的减量运算符。  
  
 用户定义的类型可以重载 `--` 运算符（请参阅[运算符](../../../csharp/language-reference/keywords/operator.md)）。 对整数类型的操作通常可用于枚举。  
  
## <a name="example"></a>示例  
 [!code-cs[csRefOperators#8](../../../csharp/language-reference/operators/codesnippet/CSharp/decrement-operator_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 运算符](../../../csharp/language-reference/operators/index.md)

