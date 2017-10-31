---
title: "链接查询示例 (C#)"
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
ms.assetid: abbca162-d95e-43af-b92c-e46e6aa2540e
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 70179c93c48f56614bd7c8b648f73e86ebe26ff4
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="chaining-queries-example-c"></a>链接查询示例 (C#)
此示例建立在前一示例的基础上，演示两个都使用延迟执行和迟缓计算的查询链接到一起时会发生什么情况。  
  
## <a name="example"></a>示例  
 在此示例中，还会引入另一个扩展方法 `AppendString`，该方法将一个指定字符串追加到源集合的每个字符串上，然后生成新的字符串。  
  
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
AppendString: source >ABC<  
Main: str >ABC!!!<  
  
ToUpper: source >def<  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
ToUpper: source >ghi<  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
  
 在此示例中，可以看到，每个扩展方法每次只对源集合中的一个项进行一次操作。  
  
 在此示例中，可以清楚地看到，尽管已将生成集合的查询链接到了一起，但未具体化任何中间集合。 相反，每一项只是从一个迟缓方法传递到下一个迟缓方法。 这种方法的内存需求量比另一种方法小得多，在另一种方法中，首先获取一个字符串数组，然后创建第二个字符串数组（其中的字符串都已转换为大写形式），最后创建第三个字符串数组（其中的每个字符串都追加了感叹号）。  
  
 本教程下一主题演示中间具体化：  
  
-   [中间具体化 (C#)](../../../../csharp/programming-guide/concepts/linq/intermediate-materialization.md)  
  
## <a name="see-also"></a>另请参阅  
 [教程：将查询链接在一起 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)

