---
title: "重构为纯函数 (C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
ms.assetid: 2944a0d4-fd33-4e2e-badd-abb0f9be2fcc
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 9bb17207ba72bb22f5d6db55e9d1bd77e3013445
ms.openlocfilehash: 2bce781df80a777203ed8e713bedf83f1c7779a8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/25/2017

---
# <a name="refactoring-into-pure-functions-c"></a>重构为纯函数 (C#)

纯函数转换的一个重要方面是学习如何使用纯函数重构代码。  
  
> [!NOTE]
>  函数编程中的常用术语是使用纯函数重构程序。 在 Visual Basic 和 C++ 中，这对应于使用相应语言的函数。 但在 C# 中，函数称为方法。 出于本文论述的需要，在 C# 中以方法的形式实现了一个纯函数。  
  
 如本节前面所述，纯函数具有两个有用的特性：  
  
-   它没有任何副作用。 函数不会更改函数以外的任何变量或任何类型的数据。  
  
-   它具有一致性。 在提供同一组输入数据的情况下，它将始终返回相同的输出值。  
  
 转换为函数编程的一种方式是重构现有代码以消除不必要的副作用和外部依赖项。 这样，您可以创建现有代码的纯函数版本。  
  
 本主题讨论什么是纯函数，什么不是纯函数。 [教程：操作 WordprocessingML 文档中的内容 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md) 教程演示如何操作 WordprocessingML 文档并包括两个有关如何使用纯函数进行重构的示例。  
  
## <a name="eliminating-side-effects-and-external-dependencies"></a>消除副作用和外部依赖项  
 下面的示例对比两个非纯函数和一个纯函数。  
  
### <a name="non-pure-function-that-changes-a-class-member"></a>可更改类成员的非纯函数  
 在下面的代码中，`HypenatedConcat` 函数不是纯函数，因为它修改了类中的 `aMember` 数据成员：  
  
```csharp  
public class Program  
{  
    private static string aMember = "StringOne";  
  
    public static void HypenatedConcat(string appendStr)  
    {  
        aMember += '-' + appendStr;  
    }  
  
    public static void Main()  
    {  
        HypenatedConcat("StringTwo");  
        Console.WriteLine(aMember);  
    }  
}  
```  
  
 此代码生成以下输出：  
  
```  
StringOne-StringTwo  
```  
  
 请注意，它与修改的数据是具有 `public` 还是 `private` 访问权限或者是 `static` 成员还是实例成员均无关。 纯函数不会更改函数以外的任何数据。  
  
### <a name="non-pure-function-that-changes-an-argument"></a>可更改参数的非纯函数  
 此外，此同一个函数的下面版本不是纯函数，因为它修改了其参数 `sb` 的内容。  
  
```csharp  
public class Program  
{  
    public static void HypenatedConcat(StringBuilder sb, String appendStr)  
    {  
        sb.Append('-' + appendStr);  
    }  
  
    public static void Main()  
    {  
        StringBuilder sb1 = new StringBuilder("StringOne");  
        HypenatedConcat(sb1, "StringTwo");  
        Console.WriteLine(sb1);  
    }  
}  
```  
  
 此版本的程序生成的输出与第一个版本相同，因为 `HypenatedConcat` 函数已通过调用 <xref:System.Text.StringBuilder.Append%2A> 成员函数而更改了其第一个参数的值（状态）。 请注意，即使 `HypenatedConcat` 实际上使用了按值调用参数传递，也会发生此更改。  
  
> [!IMPORTANT]
>  对于引用类型，按值传递参数会得到对所传递对象的引用的副本。 此副本与原始引用一样，仍与同一个实例数据关联（除非为引用变量分配新对象）。 函数修改参数不一定需要按引用调用。  
  
### <a name="pure-function"></a>纯函数  
下面版本的程序演示如何将 `HypenatedConcat` 函数作为纯函数实现。  
  
```csharp  
class Program  
{  
    public static string HyphenatedConcat(string s, string appendStr)  
    {  
        return (s + '-' + appendStr);  
    }  
  
    public static void Main(string[] args)  
    {  
        string s1 = "StringOne";  
        string s2 = HyphenatedConcat(s1, "StringTwo");  
        Console.WriteLine(s2);  
    }  
}  
```  
  
 此版本同样生成相同的输出行：`StringOne-StringTwo`。 请注意保留串联值，它存储在中间变量 `s2` 中。  
  
 一种非常实用的方法是编写本地不纯（即声明和修改本地变量）但在全局为纯的函数。 这些函数具有许多需要的可组合特性，但舍弃了一些较为繁复的函数编程语法，如在使用简单的循环即可完成同样操作时必须使用递归。  
  
## <a name="standard-query-operators"></a>标准查询运算符  
 标准查询运算符的重要特性是它们以纯函数的形式实现。  
  
 有关详细信息，请参阅[标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
## <a name="see-also"></a>请参阅  
 [纯函数转换简介 (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [函数编程与命令式编程 (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)

