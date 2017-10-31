---
title: "将标准查询运算符链接在一起 (C#)"
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
ms.assetid: 66f2b0a9-2c23-4735-988e-bbc9dfb55c7b
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 40c65c80c08caa310cb72a194534ad63fcea890a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="chaining-standard-query-operators-together-c"></a>将标准查询运算符链接在一起 (C#)
这是[教程：将查询链接在一起 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md) 教程中的最后一个主题。  
  
 标准查询运算符也可以链接在一起。 例如，您可以插入 <xref:System.Linq.Enumerable.Where%2A?displayProperty=fullName> 运算符，并且该运算符也可以以迟缓方式操作。 它不会具体化任何中间结果。  
  
## <a name="example"></a>示例  
 在此示例中，调用 <xref:System.Linq.Enumerable.Where%2A> 之前将调用 `ConvertCollectionToUpperCase` 方法。 <xref:System.Linq.Enumerable.Where%2A> 方法的操作方式与本教程前面示例中使用的迟缓方法 `ConvertCollectionToUpperCase` 和 `AppendString` 几乎完全相同。  
  
 区别之一是在本例中，<xref:System.Linq.Enumerable.Where%2A> 方法循环访问其源集合，确定第一项不传递谓词，然后获取传递谓词的下一项。 示例然后生成第二项。  
  
 但基本要旨是相同的：除非必要，否则不具体化中间集合。  
  
 在使用查询表达式时，会将查询表达式转换为对标准查询运算符的调用，这一原理同样适用。  
  
 本节中查询 Office Open XML 文档的所有示例都使用相同的原理。 延迟执行和迟缓计算是有效使用 LINQ（和 LINQ to XML）所必须理解的一些基础概念。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            where s.CompareTo("D") >= 0  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 该示例产生下面的输出：  
  
```  
ToUpper: source >abc<  
ToUpper: source >def<  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
ToUpper: source >ghi<  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
## <a name="see-also"></a>另请参阅  
 [教程：将查询链接在一起 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)

