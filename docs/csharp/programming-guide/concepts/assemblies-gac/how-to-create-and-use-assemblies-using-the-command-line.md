---
title: "如何：使用命令行创建和使用程序集 (C#)"
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
ms.assetid: 408ddce3-89e3-4e12-8353-34a49beeb72b
caps.latest.revision: 4
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 630a799331e03860fbee34eab6bea3bb594ef0f0
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-create-and-use-assemblies-using-the-command-line-c"></a>如何：使用命令行创建和使用程序集 (C#)
程序集或动态链接库 (DLL) 会在运行时链接到程序。 为了演示如何生成和使用 DLL，请考虑以下方案：  
  
-   `MathLibrary.DLL`：包含要在运行时调用的方法的库文件。 在此示例中，DLL 包含两个方法，即 `Add` 和 `Multiply`。  
  
-   `Add`：包含方法 `Add` 的源文件。 它返回其参数的总和。 包含方法 `Add` 的类 `AddClass` 是命名空间 `UtilityMethods` 的成员。  
  
-   `Mult`：包含方法 `Multiply` 的源代码。 它返回其参数的乘积。 包含方法 `Multiply` 的类 `MultiplyClass` 也是命名空间 `UtilityMethods` 的成员。  
  
-   `TestCode`：包含 `Main` 方法的文件。 它使用 DLL 文件中的方法计算运行时参数的总和与乘积。  
  
## <a name="example"></a>示例  
  
```csharp  
// File: Add.cs   
namespace UtilityMethods  
{  
    public class AddClass   
    {  
        public static long Add(long i, long j)   
        {   
            return (i + j);  
        }  
    }  
}  
```  
  
```csharp  
// File: Mult.cs  
namespace UtilityMethods   
{  
    public class MultiplyClass  
    {  
        public static long Multiply(long x, long y)   
        {  
            return (x * y);   
        }  
    }  
}  
```  
  
```csharp  
// File: TestCode.cs  
  
using UtilityMethods;  
  
class TestCode  
{  
    static void Main(string[] args)   
    {  
        System.Console.WriteLine("Calling methods from MathLibrary.DLL:");  
  
        if (args.Length != 2)  
        {  
            System.Console.WriteLine("Usage: TestCode <num1> <num2>");  
            return;  
        }  
  
        long num1 = long.Parse(args[0]);  
        long num2 = long.Parse(args[1]);  
  
        long sum = AddClass.Add(num1, num2);  
        long product = MultiplyClass.Multiply(num1, num2);  
  
        System.Console.WriteLine("{0} + {1} = {2}", num1, num2, sum);  
        System.Console.WriteLine("{0} * {1} = {2}", num1, num2, product);  
    }  
}  
/* Output (assuming 1234 and 5678 are entered as command-line arguments):  
    Calling methods from MathLibrary.DLL:  
    1234 + 5678 = 6912  
    1234 * 5678 = 7006652          
*/  
```  
  
 此文件包含使用 DLL 方法 `Add` 和 `Multiply` 的算法。 它首先分析从命令行输入的参数 `num1` 和 `num2`。 然后通过对 `AddClass` 类使用 `Add` 方法来计算总和，并通过对 `MultiplyClass` 类使用 `Multiply` 方法来计算乘积。  
  
 请注意，文件开头的 `using` 指令使你可以使用非限定类名在编译时引用 DLL 方法，如下所示：  
  
```csharp  
MultiplyClass.Multiply(num1, num2);  
```  
  
 否则，你必须使用完全限定的名称，如下所示：  
  
```csharp  
UtilityMethods.MultiplyClass.Multiply(num1, num2);  
```  
  
## <a name="execution"></a>执行  
 若要运行程序，请输入 EXE 文件的名称，后跟两个数字，如下所示：  
  
 `TestCode 1234 5678`  
  
## <a name="compiling-the-code"></a>编译代码  
 若要生成文件 `MathLibrary.DLL`，请使用以下命令行编译两个文件 `Add` 和 `Mult`。  
  
```csharp  
csc /target:library /out:MathLibrary.DLL Add.cs Mult.cs  
```  
  
 [/target:library](../../../../csharp/language-reference/compiler-options/target-library-compiler-option.md) 编译器选项告知编译器输出 DLL 而不是 EXE 文件。 后跟文件名的 [/out](../../../../csharp/language-reference/compiler-options/out-compiler-option.md) 编译器选项用于指定 DLL 文件名。 否则，编译器使用第一个文件 (`Add.cs`) 作为 DLL 的名称。  
  
 若要生成可执行文件 `TestCode.exe`，请使用以下命令行：  
  
```csharp  
csc /out:TestCode.exe /reference:MathLibrary.DLL TestCode.cs  
```  
  
 **/out** 编译器选项告知编译器输出 EXE 文件并指定输出文件的名称 (`TestCode.exe`)。 此编译器选项是可选的。 [/reference](../../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 编译器选项指定此程序使用的 DLL 文件。 有关详细信息，请参阅 [/reference](../../../../csharp/language-reference/compiler-options/reference-compiler-option.md)。  
  
 有关从命令行进行生成的详细信息，请参阅[在命令行上使用 csc.exe 生成](../../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../../csharp/programming-guide/index.md)   
 [程序集和全局程序集缓存 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [创建用于容纳 DLL 函数的类](../../../../framework/interop/creating-a-class-to-hold-dll-functions.md)

