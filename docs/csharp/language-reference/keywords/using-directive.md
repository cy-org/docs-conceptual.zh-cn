---
title: "using 指令（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
caps.latest.revision: 31
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
ms.openlocfilehash: 1129efd8a1c4058a9648eab61f98cdcef7e9f2f7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="using-directive-c-reference"></a>using 指令（C# 参考）
`using` 指令有三种用途：  
  
-   允许在命名空间中使用类型，这样无需在该命名空间中限定某个类型的使用：  
  
    ```csharp  
    using System.Text;  
    ```  
  
-   允许访问类型的静态成员，而无需限定使用类型名称进行访问。 
  
    ```csharp  
    using static System.Math;  
    ```  
     
    有关详细信息，请参阅 [using static 指令](using-static.md)。

-   为命名空间或类型创建别名。 这称为 *using 别名指令*。  
  
    ```csharp  
    using Project = PC.MyCompany.Project;  
    ```  
  
 `using` 关键字还用于创建 using 语句，此类语句有助于确保正确处理 <xref:System.IDisposable> 对象（如文件和字体）。 有关详细信息，请参阅 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)。  
  
## <a name="using-static-type"></a>Using Static 类型  
 你可以访问类型的静态成员，而无需限定使用类型名称进行访问：  
  
```csharp  
using static System.Console;   
using static System.Math;  
class Program   
{   
    static void Main()   
    {   
        WriteLine(Sqrt(3*3 + 4*4));   
    }   
}  
```  
  
## <a name="remarks"></a>备注  
 `using` 指令的范围限于显示它的文件。  
  
 创建 `using` 别名，以便更易于将标识符限定为命名空间或类型。 using 别名指令的右侧必须始终是一个完全限定类型，而与前面的 using 指令无关。  
  
 创建 `using` 指令，以便在命名空间中使用类型而不必指定命名空间。 `using` 指令不为你提供对嵌套在指定命名空间中的任何命名空间的访问权限。  
  
 命名空间分为两类：用户定义的命名空间和系统定义的命名空间。 用户定义的命名空间是在代码中定义的命名空间。 有关系统定义的命名空间的列表，请参阅 [.NET Framework 类库](http://go.microsoft.com/fwlink/?LinkID=227195)。  
  
 有关引用其他程序集中的方法的示例，请参阅[创建和使用 C# DLL](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)。  
  
## <a name="example-1"></a>示例 1  
  
 下面的示例显示如何为命名空间定义和使用 `using` 别名：  
  
 [!code-cs[csrefKeywordsNamespace#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_1.cs)]  
  
 using 别名指令的右侧不能有开放式泛型类型。 例如，不能为 List\<T> 创建 using 别名，但可以为 List\<int> 创建。  
  
## <a name="example-2"></a>示例 2  
  
 下面的示例显示如何为类定义 `using` 指令和 `using` 别名：  
  
 [!code-cs[csrefKeywordsNamespace#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [Using 命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [using 语句](../../../csharp/language-reference/keywords/using-statement.md)

