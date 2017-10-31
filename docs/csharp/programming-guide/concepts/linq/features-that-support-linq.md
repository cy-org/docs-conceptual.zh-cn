---
title: "支持 LINQ 的 C# 功能"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- LINQ [C#], features supporting LINQ
ms.assetid: 524b0078-ebfd-45a7-b390-f2ceb9d84797
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
ms.openlocfilehash: 01db44482ee3230d15af5ce8e0373fb15a769609
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="c-features-that-support-linq"></a>支持 LINQ 的 C# 功能
下一节介绍 C# 3.0 中引入的新语言构造。 虽然这些新功能在一定程度上都用于 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询，但并不限于 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]，如果认为有用，在任何情况下都可以使用这些新功能。  
  
## <a name="query-expressions"></a>查询表达式  
 查询表达式使用类似于 SQL 或 XQuery 的声明性语法来查询 IEnumerable 集合。 在编译时，查询语法转换为对 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 提供程序的标准查询运算符扩展方法实现的方法调用。 应用程序通过使用 `using` 指令指定适当的命名空间来控制范围内的标准查询运算符。 下面的查询表达式获取一个字符串数组，按字符串中的第一个字符对字符串进行分组，然后对各组进行排序。  
  
```  
var query = from str in stringArray  
            group str by str[0] into stringGroup  
            orderby stringGroup.Key  
            select stringGroup;  
```  
  
 有关详细信息，请参阅 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)。  
  
## <a name="implicitly-typed-variables-var"></a>隐式类型化变量 (var)  
 可以使用 [var](../../../../csharp/language-reference/keywords/var.md) 修饰符来指示编译器推断并分配类型，而不必在声明并初始化变量时显式指定类型，如下所示：  
  
```  
var number = 5;  
var name = "Virginia";  
var query = from str in stringArray  
            where str[0] == 'm'  
            select str;  
```  
  
 声明为 `var` 的变量与显式指定其类型的变量一样都是强类型。 通过使用 `var`，可以创建匿名类型，但它可用于任何本地变量。 也可以使用隐式类型声明数组。  
  
 有关详细信息，请参阅[隐式类型本地变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
## <a name="object-and-collection-initializers"></a>对象和集合初始值设定项  
 通过对象和集合初始值设定项，初始化对象时无需为对象显式调用构造函数。 初始值设定项通常用在将源数据投影到新数据类型的查询表达式中。 假定一个类名为 `Customer`，具有公共 `Name` 和 `Phone` 属性，可以按下列代码中所示使用对象初始值设定项：  
  
```  
Customer cust = new Customer { Name = "Mike", Phone = "555-1212" };  
```  
  
 有关详细信息，请参阅[对象和集合初始值设定项](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。  
  
## <a name="anonymous-types"></a>匿名类型  
 匿名类型由编译器构造，且类型名称只可用于编译器。 匿名类型提供一种在查询结果中对一组属性临时分组的简便方法，无需定义单独的命名类型。 使用新的表达式和对象初始值设定项初始化匿名类型，如下所示：  
  
```  
select new {name = cust.Name, phone = cust.Phone};  
```  
  
 有关详细信息，请参阅[匿名类型](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。  
  
## <a name="extension-methods"></a>扩展方法  
 扩展方法是一种可与类型关联的静态方法，因此可以像实例方法那样对类型调用它。 实际上，利用此功能，可以将新方法“添加”到现有类型，而不会实际修改它们。 标准查询运算符是一组扩展方法，它们为实现 <xref:System.Collections.Generic.IEnumerable%601> 的任何类型提供 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询功能。  
  
 有关详细信息，请参阅[扩展方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)  
  
## <a name="lambda-expressions"></a>Lambda 表达式  
 Lambda 表达式是一种内联函数，该函数使用 => 运算符将输入参数与函数体分离，并且可以在编译时转换为委托或表达式树。 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 编程中，在对标准查询运算符进行直接方法调用时，会遇到 lambda 表达式。  
  
 有关详细信息，请参见:  
  
-   [匿名函数](../../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)  
  
-   [Lambda 表达式](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
  
-   [表达式树 (C#)](../../../../csharp/programming-guide/concepts/expression-trees/index.md)  
  
## <a name="auto-implemented-properties"></a>自动实现的属性  
 自动实现的属性使属性声明变得更简洁。 当你声明以下示例中所示的属性时，编译器会创建仅可以通过属性 getter 和 setter 访问的私有匿名支持字段。  
  
```  
public string Name {get; set;}  
```  
  
 有关详细信息，请参阅[自动实现的属性](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)。  
  
## <a name="see-also"></a>请参阅  
 [语言集成查询 (LINQ) (C#)](../../../../csharp/programming-guide/concepts/linq/index.md)

