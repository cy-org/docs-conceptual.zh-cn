---
title: "如何：声明、实例化和使用委托（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- delegates [C#], declaring and instantiating
ms.assetid: 61c4895f-f785-48f8-8bfe-db73b411c4ae
caps.latest.revision: 21
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
ms.openlocfilehash: 5a16fe4c627989f701ba523769cd87839d074849
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-declare-instantiate-and-use-a-delegate-c-programming-guide"></a>如何：声明、实例化和使用委托（C# 编程指南）
在 C# 1.0 和更高版本中，可以如下面的示例所示声明委托。  
  
 [!code-cs[csProgGuideDelegates#13](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_1.cs)]  
  
 [!code-cs[csProgGuideDelegates#14](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_2.cs)]  
  
 C# 2.0 提供了更简单的方法来编写前面的声明，如下面的示例所示。  
  
 [!code-cs[csProgGuideDelegates#32](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_3.cs)]  
  
 在 C# 2.0 和更高版本中，还可以使用匿名方法来声明和初始化[委托](../../../csharp/language-reference/keywords/delegate.md)，如下面的示例所示。  
  
 [!code-cs[csProgGuideDelegates#15](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_4.cs)]  
  
 在 C# 3.0 和更高版本中，还可以通过使用 lambda 表达式声明和实例化委托，如下面的示例所示。  
  
 [!code-cs[csProgGuideDelegates#31](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_5.cs)]  
  
 有关详细信息，请参阅 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 下面的示例演示如何声明、实例化和使用委托。 `BookDB` 类封装用来维护书籍数据库的书店数据库。 它公开一个方法 `ProcessPaperbackBooks`，用于在数据库中查找所有平装书并为每本书调用委托。 使用的 `delegate` 类型名为 `ProcessBookDelegate`。 `Test` 类使用此类打印平装书的书名和平均价格。  
  
 使用委托提升书店数据库和客户端代码之间的良好分隔功能。 客户端代码程序不知道如何存储书籍或书店代码如何查找平装书。 书店代码不知道它在找到平装书之后对其执行什么处理。  
  
## <a name="example"></a>示例  
 [!code-cs[csProgGuideDelegates#12](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_6.cs)]  
  
## <a name="robust-programming"></a>可靠编程  
  
-   声明委托。  
  
     以下语句声明新的委托类型。  
  
     [!code-cs[csProgGuideDelegates#16](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_7.cs)]  
  
     每个委托类型描述自变量的数量和类型，以及它可以封装的方法的返回值类型。 每当需要一组新的自变量类型或返回值类型，则必须声明一个新的委托类型。  
  
-   实例化委托。  
  
     声明委托类型后，则必须创建委托对象并将其与特定的方法相关联。 在上例中，你通过将 `PrintTitle` 方法传递给 `ProcessPaperbackBooks` 方法执行此操作，如下面的示例所示：  
  
     [!code-cs[csProgGuideDelegates#17](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_8.cs)]  
  
     这将创建一个新的与[静态](../../../csharp/language-reference/keywords/static.md)方法 `Test.PrintTitle` 关联的委托对象。 同样，如下面的示例所示，传递对象 `totaller` 中的非静态方法 `AddBookToTotal`：  
  
     [!code-cs[csProgGuideDelegates#18](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_9.cs)]  
  
     在这两种情况下，都将新的委托对象传递给 `ProcessPaperbackBooks` 方法。  
  
     创建委托后，它与之关联的方法就永远不会更改；委托对象是不可变的。  
  
-   调用委托。  
  
     创建委托对象后，通常会将委托对象传递给将调用该委托的其他代码。 委托对象是通过使用委托对象的名称调用的，后跟用圆括号括起来的将传递给委托的自变量。 下面是一个委托调用示例：  
  
     [!code-cs[csProgGuideDelegates#19](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_10.cs)]  
  
     委托可以同步调用（如在本例中）或通过使用 `BeginInvoke` 和 `EndInvoke` 方法异步调用。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)

