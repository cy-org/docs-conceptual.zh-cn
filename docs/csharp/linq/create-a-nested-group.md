---
title: "创建嵌套组"
description: "如何创建嵌套组。"
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: e9f00708-362e-4d13-98c5-d77549347ba0
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 361ac1f224c6eef292fcf8434c7e465c9448b19c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="create-a-nested-group"></a>创建嵌套组

以下示例演示如何在 LINQ 查询表达式中创建嵌套组。 首先根据学生年级创建每个组，然后根据每个人的姓名进一步细分为小组。  
  
## <a name="example"></a>示例

 > [!NOTE]
 > 此示例包含对[查询对象集合](query-a-collection-of-objects.md)内示例代码中所定义对象的引用。 

 [!code-cs[csProgGuideLINQ#24](../../../samples/snippets/csharp/concepts/linq/how-to-create-a-nested-group_1.cs)]  
  
 请注意，需要使用 3 个嵌套的 `foreach` 循环来循环访问嵌套组的内部元素。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ 查询表达式](index.md)

