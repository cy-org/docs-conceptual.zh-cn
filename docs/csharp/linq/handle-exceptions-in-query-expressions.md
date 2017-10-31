---
title: "在查询表达式中处理异常"
description: "如何在查询表达式中处理异常。"
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2bf0c397-13fb-4f68-bc2b-531c6c88a167
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9ce4a4ca62bb476b2414ec8b93d5633faca53b59
ms.contentlocale: zh-cn
ms.lasthandoff: 08/11/2017

---
# <a name="handle-exceptions-in-query-expressions"></a>在查询表达式中处理异常

在查询表达式的上下文中可以调用任何方法。 但是，我们建议避免在查询表达式中调用任何会产生副作用（如修改数据源内容或引发异常）的方法。 此示例演示在查询表达式中调用方法时如何避免引发异常，而不违反有关异常处理的常规 .NET Framework 指南。 这些指南阐明，当你理解在给定上下文中为何会引发异常时，捕获到该特定异常是可以接受的。 有关详细信息，请参阅[异常的最佳做法](../../standard/exceptions/best-practices-for-exceptions.md)。  
  
 最后的示例演示了在执行查询期间必须引发异常时，该如何处理这种情况。  
  
## <a name="example"></a>示例  

 以下示例演示如何将异常处理代码移到查询表达式外。 只有当方法不取决于查询的任何本地变量时，才可以执行此操作。  
  
 [!code-cs[csProgGuideLINQ#10](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_1.cs)]  
  
## <a name="example"></a>示例 

 在某些情况下，针对由查询内部引发的异常的最佳措施可能是立即停止执行查询。 下面的示例演示如何处理可能在查询正文内部引发的异常。 假定 `SomeMethodThatMightThrow` 可能导致要求停止执行查询的异常。  
  
 请注意，`try` 块封装 `foreach` 循环，且不对自身进行查询。 这是由于 `foreach` 循环正是实际执行查询时的点。 有关详细信息，请参阅 [LINQ 查询简介](../programming-guide/concepts/linq/introduction-to-linq-queries.md)。  
  
 [!code-cs[csProgGuideLINQ#12](../../../samples/snippets/csharp/concepts/linq/how-to-handle-exceptions-in-query-expressions_2.cs)]  
  

## <a name="see-also"></a>另请参阅  
 [LINQ 查询表达式](index.md)

