---
title: "引用类型（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.referencetypes
dev_langs:
- CSharp
helpviewer_keywords:
- reference types [C#]
- C# language, reference types
- types [C#], reference types
ms.assetid: 801cf030-6e2d-4a0d-9daf-1431b0c31f47
caps.latest.revision: 15
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
ms.openlocfilehash: ed7b9c8ed4aa1136c09049c8ffd6c68beeeb2a48
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="reference-types-c-reference"></a>引用类型（C# 参考）
C# 中有两种类型：引用类型和值类型。 引用类型的变量存储对其数据（对象）的引用，而值类型的变量直接包含其数据。 对于引用类型，两种变量可引用同一对象；因此，对一个变量执行的操作会影响另一个变量所引用的对象。 对于值类型，每个变量都具有其自己的数据副本，对一个变量执行的操作不会影响另一个变量（ref 和 out 参数变量除外，请参阅 [ref](../../../csharp/language-reference/keywords/ref.md) 和 [out 参数修饰符](../../../csharp/language-reference/keywords/out-parameter-modifier.md)）。  
  
 下列关键字用于声明引用类型：  
  
-   [类](../../../csharp/language-reference/keywords/class.md)  
  
-   [接口](../../../csharp/language-reference/keywords/interface.md)  
  
-   [委托](../../../csharp/language-reference/keywords/delegate.md)  
  
 C# 也提供了下列内置引用类型：  
  
-   [动态](../../../csharp/language-reference/keywords/dynamic.md)  
  
-   [对象](../../../csharp/language-reference/keywords/object.md)  
  
-   [字符串](../../../csharp/language-reference/keywords/string.md)  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [类型](../../../csharp/language-reference/keywords/types.md)   
 [值类型](../../../csharp/language-reference/keywords/value-types.md)

