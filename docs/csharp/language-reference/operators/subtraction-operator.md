---
title: "- 运算符（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- -_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- '- operator [C#]'
- subtraction operator (-) [C#]
ms.assetid: 4de7a4fa-c69d-48e6-aff1-3130af970b2d
caps.latest.revision: 19
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
ms.openlocfilehash: 7fabdab8593ff4d721b352b59a45f51721f53eb4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="--operator-c-reference"></a>- 运算符（C# 参考）
`-` 运算符既可作为一元运算符也可作为二元运算符。  
  
## <a name="remarks"></a>备注  
 为所有数值类型预定义了一元 `-` 运算符。 对数值类型进行一元 `-` 运算的结果是操作数的数值求反运算。  
  
 针对所有数值和枚举类型预定义二元 `-` 运算符，从第一个操作数中减去第一个操作数。  
  
 委托类型也提供二元 `-` 运算符，该运算符执行委托移除。  
  
 用户定义的类型可重载一元 `-` 运算符和二元 `-` 运算符。 有关详细信息，请参阅[运算符（C# 参考）](../../../csharp/language-reference/keywords/operator.md)。  
  
## <a name="example"></a>示例  
 [!code-cs[csRefOperators#40](../../../csharp/language-reference/operators/codesnippet/CSharp/subtraction-operator_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 运算符](../../../csharp/language-reference/operators/index.md)

