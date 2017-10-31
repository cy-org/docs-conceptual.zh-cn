---
title: "如何：标识可以为 null 的类型（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#], identifying
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
caps.latest.revision: 7
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
ms.openlocfilehash: c9e05bfe8be45e5b71a8db06ce4f2502c5397fd4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-identify-a-nullable-type-c-programming-guide"></a>如何：标识可以为 null 的类型（C# 编程指南）
可以使用 C# [typeof](../../../csharp/language-reference/keywords/typeof.md) 运算符创建表示可以为 null 的类型的 <xref:System.Type> 对象：  
  
```  
System.Type type = typeof(int?);  
```  
  
 还可以使用 <xref:System.Reflection> 命名空间的类和方法生成表示可以为 null 的类型的 <xref:System.Type> 对象。 但是，如果尝试使用 <xref:System.Object.GetType%2A> 方法或 `is` 运算符在运行时获取可以为 null 的变量的类型信息，则得到的结果是表示基础类型而不是可以为 null 的类型本身的 <xref:System.Type> 对象。  
  
 对可以为 null 的类型调用 `GetType` 会导致在将该类型隐式转换为 <xref:System.Object> 时执行装箱操作。 因此，<xref:System.Object.GetType%2A> 总是返回表示基础类型而不是可以为 null 的类型的 <xref:System.Type> 对象。  
  
```  
int? i = 5;  
Type t = i.GetType();  
Console.WriteLine(t.FullName); //"System.Int32"  
```  
  
 C# 的 [is](../../../csharp/language-reference/keywords/is.md) 运算符还可以作用于可以为 null 的基础类型。 因此，不能使用 `is` 确定变量是否是可以为 null 的类型。 以下示例演示 `is` 运算符将 Nullable\<int> 变量视为 int 变量。  
  
```  
static void Main(string[] args)  
{  
  int? i = 5;  
  if (i is int) // true  
    //…  
}  
```  
  
## <a name="example"></a>示例  
 使用下面的代码来确定 <xref:System.Type> 对象是否表示可以为 null 的类型。 请记住，如果从对 <xref:System.Object.GetType%2A> 的调用返回`Type` 对象，则此代码始终返回 false，如本主题前面所述。  
  
```  
if (type.IsGenericType && type.GetGenericTypeDefinition() == typeof(Nullable<>)) {…}  
```  
  
## <a name="see-also"></a>另请参阅  
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)   
 [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)

