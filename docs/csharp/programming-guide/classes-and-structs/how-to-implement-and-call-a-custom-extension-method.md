---
title: "如何：实现和调用自定义扩展方法（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- extension methods [C#], implementing and calling
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
caps.latest.revision: 15
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
ms.openlocfilehash: 8c1c26640c550ce2b16ffafd59430e92189764f9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>如何：实现和调用自定义扩展方法（C# 编程指南）
本主题介绍如何实现 [.NET Framework 类库](http://go.microsoft.com/fwlink/?LinkID=217856) 中任意类型的扩展方法，或是你想要扩展的任何其他 .NET 类型。 客户端代码可以通过以下方法使用扩展方法，添加包含这些扩展方法的 DLL 的引用，以及添加 [using](../../../csharp/language-reference/keywords/using-directive.md) 指令，该指令指定在其中定义扩展方法的命名空间。  
  
## <a name="to-define-and-call-the-extension-method"></a>定义和调用扩展方法  
  
1.  定义包含扩展方法的静态[类](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
     此类必须对客户端代码可见。 有关可访问性规则的详细信息，请参阅[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
2.  将扩展方法实现为静态方法，并且使其可见性至少与所在类的可见性相同。  
  
3.  此方法的第一个参数指定方法所操作的类型；此参数前面必须加上 [this](../../../csharp/language-reference/keywords/this.md) 修饰符。  
  
4.  在调用代码中，添加 `using` 指令，用于指定包含扩展方法类的[命名空间](../../../csharp/language-reference/keywords/namespace.md)。  
  
5.  和调用类型的实例方法那样调用这些方法。  
  
     请注意，第一个参数并不是由调用代码指定，因为它表示要在其上应用运算符的类型，并且编译器已经知道对象的类型。 你只需通过 `n` 提供形参 2 的实参。  
  
## <a name="example"></a>示例  
 以下示例实现 `CustomExtensions.StringExtension` 类中名为 `WordCount` 的扩展方法。 此方法对 <xref:System.String> 类进行操作，该类指定为第一个方法参数。 将 `CustomExtensions` 命名空间导入应用程序命名空间，并在 `Main` 方法内部调用此方法。  
  
 [!code-cs[csProgGuideExtensionMethods#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-and-call-a-custom-extension-method_1.cs)]  
  
## <a name="compiling-the-code"></a>编译代码  
 若要运行此代码，请将其复制并粘贴到已在 [!INCLUDE[vs_current_short](~/includes/vs-current-short-md.md)] 中创建的 Visual C# 控制台应用程序项目。 默认情况下，此项目面向 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 3.5 版，并且具有对 System.Core.dll 的引用和一个用于 System.Linq 的 `using` 指令。 如果项目中缺少其中一个或多个要求，则可以手动添加它们。   
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 扩展方法不存在特定的安全漏洞。 始终不会将扩展方法用于模拟类型的现有方法，因为为了支持类型本身定义的实例或静态方法，已解决所有名称冲突。 扩展方法无法访问扩展类中的任何隐私数据。  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [LINQ（语言集成查询）](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)   
 [protected](../../../csharp/language-reference/keywords/protected.md)   
 [internal](../../../csharp/language-reference/keywords/internal.md)   
 [public](../../../csharp/language-reference/keywords/public.md)   
 [this](../../../csharp/language-reference/keywords/this.md)   
 [namespace](../../../csharp/language-reference/keywords/namespace.md)

