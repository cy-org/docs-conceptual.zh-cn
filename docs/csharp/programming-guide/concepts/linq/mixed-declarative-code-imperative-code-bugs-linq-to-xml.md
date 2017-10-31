---
title: "混合声明性代码-命令性代码的问题 (LINQ to XML) (C#)"
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
ms.assetid: fada62d0-0680-4e73-945a-2b00d7a507af
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2fb679ee2593520e633daba969ccaa4db4d30509
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mixed-declarative-codeimperative-code-bugs-linq-to-xml-c"></a>混合声明性代码/命令性代码的问题 (LINQ to XML) (C#)
[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 包含各种不同的方法，使您能够直接修改 XML 树。 您可以添加元素、删除元素、更改元素的内容、添加属性等等。 在[修改 XML 树 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md) 中详细介绍了此编程接口。 如果循环访问一个轴，例如 <xref:System.Xml.Linq.XContainer.Elements%2A>，而在循环访问该轴时正在修改 XML 树，那么可能会发生一些异常问题。  
  
 此问题有时称为“万圣节问题”。  
  
## <a name="definition-of-the-problem"></a>问题的定义  
 如果你使用 LINQ 编写循环访问集合的代码，那么你是以声明性风格在编写代码。 这种风格更像是描述要实现的内容，而不是描述所需要的实现方式。 如果你编写的代码要执行以下操作：1) 获取第一个元素；2) 测试该元素是否符合某种条件；3) 修改该元素；4) 将该元素放回列表中。那么，此代码就是命令性代码。 你是在告诉计算机希望以何种方式完成任务。  
  
 在同一操作中混合这些代码风格正是导致问题的原因。 考虑以下情况：  
  
 假设您有一个链接列表，其中有三个项（a、b 和 c）：  
  
 `a -> b -> c`  
  
 现在，假设您想在链接列表中移动，并添加三个新项（a'、b' 和 c'）。 您希望生成如下所示的链接列表：  
  
 `a -> a' -> b -> b' -> c -> c'`  
  
 因此您编写代码来循环访问该列表，在每一项后面紧接着添加一个新项。 而实际发生的情况是，您的代码首先将看到 `a` 元素，然后在它后面插入 `a'`。 现在，您的代码将移动到列表中的下一节点，此时下一节点是 `a'`！ 它会不假思索地向列表中添加一个新项 `a''`。  
  
 在实际中该如何解决这一问题？ 您可以创建原始链接列表的副本，然后创建一个全新的列表。 或者，如果您正在编写纯粹的命令性代码，您可以找到第一项，添加新项，然后在链接列表中前进两步，跳过刚添加的元素。  
  
## <a name="adding-while-iterating"></a>循环访问时添加  
 例如，假设您希望编写一段代码，让它为树中的每个元素创建一个重复的元素：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
foreach (XElement e in root.Elements())  
    root.Add(new XElement(e.Name, (string)e));  
```  
  
 此代码将进入一个无限循环。 `foreach` 语句循环访问 `Elements()` 轴，将新元素添加到 `doc` 元素。 结果它也循环访问刚添加的元素。 由于它在每次循环访问中都分配新对象，最终将会耗尽所有可用内存。  
  
 可以通过使用 <xref:System.Linq.Enumerable.ToList%2A> 标准查询运算符将集合放入内存来修复此问题，如下所示：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
foreach (XElement e in root.Elements().ToList())  
    root.Add(new XElement(e.Name, (string)e));  
Console.WriteLine(root);  
```  
  
 现在代码可以正常工作了。 生成的 XML 树如下所示：  
  
```xml  
<Root>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
  <A>1</A>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
## <a name="deleting-while-iterating"></a>循环访问时删除  
 如果想要删除某一级别上的所有节点，您可能立即想到编写类似如下所示的代码：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
foreach (XElement e in root.Elements())  
    e.Remove();  
Console.WriteLine(root);  
```  
  
 然而，此代码执行起来不会如您所愿。 在这种情况下，在移除第一个元素 A 之后，将从包含在根中的 XML 树中移除该元素，Elements 方法中执行循环访问的代码将找不到下一个元素。  
  
 前面的代码产生以下输出：  
  
```xml  
<Root>  
  <B>2</B>  
  <C>3</C>  
</Root>  
```  
  
 解决方法仍是调用 <xref:System.Linq.Enumerable.ToList%2A> 来具体化集合，如下所示：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
foreach (XElement e in root.Elements().ToList())  
    e.Remove();  
Console.WriteLine(root);  
```  
  
 此代码产生以下输出：  
  
```xml  
<Root />  
```  
  
 或者，可以通过对父元素调用 <xref:System.Xml.Linq.XElement.RemoveAll%2A> 来完全消除循环：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
root.RemoveAll();  
Console.WriteLine(root);  
```  
  
## <a name="why-cant-linq-automatically-handle-this"></a>为何 LINQ 不能自动处理此问题？  
 一种方法是总是将所有内容放入内存，而不是执行迟缓计算。 但是，在性能和内存使用方面，这种方法开销非常大。 事实上，如果 LINQ 和 (LINQ to XML) 采用此方法，在实际情况中将会失败。  
  
 另一种可能的方法是将某种事务语法放入 LINQ，让编译器尝试分析代码并确定是否需要具体化任何特定的集合。 但是，尝试确定具有副作用的所有代码将会非常复杂。 考虑下列代码：  
  
```csharp  
var z =  
    from e in root.Elements()  
    where TestSomeCondition(e)  
    select DoMyProjection(e);  
```  
  
 这种分析代码需要分析 TestSomeCondition 和 DoMyProjection 方法，以及这些方法调用的所有方法，以此来确定是否有任何代码会产生副作用。 但是，分析代码不能简单地查找所有具有副作用的代码。 在此情况下，它需要选择只对 `root` 的子元素具有副作用的代码。  
  
 LINQ to XML 不会尝试进行任何这样的分析。  
  
 因此，避免这些问题就靠您了。  
  
## <a name="guidance"></a>指导  
 首先，不要将声明性代码和命令性代码混合。  
  
 即便您确切知道您的集合的语义以及修改 XML 树的方法的语义，可以更巧妙地编写代码来避免这类问题，但您的代码将来需要由其他开发人员来维护，而他们可能并不像您那样清楚这些问题。 如果混合使用声明性和命令性编码风格，您的代码将更加脆弱。  
  
 如果您编写代码将集合具体化从而避免这些问题，应在代码中适当加以注释，使负责维护的程序员能够了解问题所在。  
  
 其次，在性能和其他因素允许的情况下，仅使用声明性代码。 不要修改现有的 XML 树， 而是生成一个新树。  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("A", "1"),  
    new XElement("B", "2"),  
    new XElement("C", "3")  
);  
XElement newRoot = new XElement("Root",  
    root.Elements(),  
    root.Elements()  
);  
Console.WriteLine(newRoot);  
```  
  
## <a name="see-also"></a>请参阅  
 [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

