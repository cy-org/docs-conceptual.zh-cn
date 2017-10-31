---
title: "整型表（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- integral types, C#
- Visual C#, integral types
- types [C#], integral types
- ranges of integral types [C#]
ms.assetid: 62e86126-46ff-40b0-9028-e61d7558268c
caps.latest.revision: 9
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
ms.openlocfilehash: a2932d0b7c8e1b01a4965b29d90bdd5711ddb5dc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="integral-types-table-c-reference"></a>整型表（C# 参考）
下表显示整型类型的大小和范围，它们构成简单类型的子集。  
  
|类型|范围|大小|  
|----------|-----------|----------|  
|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|-128 到 127|8 位带符号整数|  
|[byte](../../../csharp/language-reference/keywords/byte.md)|0 到 255|无符号的 8 位整数|  
|[char](../../../csharp/language-reference/keywords/char.md)|U+0000 到 U+ffff|Unicode 16 位字符|  
|[short](../../../csharp/language-reference/keywords/short.md)|-32,768 到 32,767|有符号 16 位整数|  
|[ushort](../../../csharp/language-reference/keywords/ushort.md)|0 到 65,535|无符号 16 位整数|  
|[int](../../../csharp/language-reference/keywords/int.md)|-2,147,483,648 到 2,147,483,647|带符号的 32 位整数|  
|[uint](../../../csharp/language-reference/keywords/uint.md)|0 到 4,294,967,295|无符号的 32 位整数|  
|[long](../../../csharp/language-reference/keywords/long.md)|-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807|64 位带符号整数|  
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|0 到 18,446,744,073,709,551,615|无符号 64 位整数|  
  
 如果由整数文本所表示的值超出了 `ulong` 的范围，则将出现编译错误。  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [浮点型表](../../../csharp/language-reference/keywords/floating-point-types-table.md)   
 [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)   
 [设置数值结果表的格式](../../../csharp/language-reference/keywords/formatting-numeric-results-table.md)   
 [类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)

