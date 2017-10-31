---
title: "when（C# 参考）"
ms.date: 2017-03-07
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- when_CSharpKeyword
- when
dev_langs:
- CSharp
helpviewer_keywords:
- when keyword [C#]
ms.assetid: dd543335-ae37-48ac-9560-bd5f047b9aea
caps.latest.revision: 30
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
ms.openlocfilehash: ae869fa04d2dfb963694f258624c5cd594ff1184
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
 # <a name="when-c-reference"></a>when（C# 参考）

在以下两个上下文中，可以使用上下文关键字 `when` 指定筛选条件：

- 在 [try/catch](try-catch.md) 或 [try/catch/finally](try-catch-finally.md) 块的 `catch` 语句中。
- 在 [switch](switch.md) 语句的 `case` 标签中。

## <a name="when-in-a-catch-statement"></a>`catch` 语句中的 `when`

从 C# 6 开始，`When` 可用于 `catch` 语句中，以指定为执行特定异常处理程序而必须为 true 的条件。 语法为：

```csharp
catch ExceptionType [e] when (expr)
```
其中，*expr* 是一个表达式，其计算结果为布尔值。 如果该表达式返回 `true`，则执行异常处理程序；如果返回 `false`，则不执行。 

以下示例使用 `when` 关键字有条件地执行 @System.Net.HttpRequestException 的处理程序，具体取决于异常消息的文本内容。

 [!code-cs[when-with-catch](../../../../samples/snippets/csharp/language-reference/keywords/when/catch.cs)]  
  
## <a name="when-in-a-switch-statement"></a>`switch` 语句中的 `when`

从 7 开始，`case` 标签无需是互斥的，且 `case` 标签在 `switch` 语句中的显示顺序可以决定要执行的 switch 块。 `when` 关键字可指定一个筛选条件，该条件使得仅当筛选条件也为 true 时，与其相关联的 case 标签才为 true。 语法为：

```csharp
case (expr) when (when-condition):
```
其中，*expr* 是与匹配表达式进行比较的常量模式或类型模式，而 *when-condition* 是任意布尔表达式。 

以下示例使用 `when` 关键字针对具有零范围的 `Shape` 对象进行测试，同时针对各种范围大于零的 `Shape` 对象进行测试。 

 [!code-cs[when-with-case#1](../../../../samples/snippets/csharp/language-reference/keywords/when/when.cs#1)]  

## <a name="see-also"></a>请参阅 
  [switch 语句](switch.md)  
  [try/catch 语句](try-catch.md)  
  [try/catch/finally 语句](try-catch-finally.md) 


