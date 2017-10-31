---
title: "-moduleassemblyname（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /moduleassemblyname
dev_langs:
- CSharp
helpviewer_keywords:
- moduleassemblyname compiler option [C#]
- /moduleassemblyname compiler option [C#]
- .moduleassemblyname compiler option [C#]
ms.assetid: d464d9b9-f18d-423b-95e9-66c7878fd53a
caps.latest.revision: 10
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
ms.openlocfilehash: 2522609aa41ad944b37a8882c1cc56cd5967b330
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="moduleassemblyname-c-compiler-option"></a>/moduleassemblyname（C# 编译器选项）
指定一个程序集，.netmodule 可以访问其非公共类型。  
  
## <a name="syntax"></a>语法  
  
```console  
/moduleassemblyname:assembly_name  
```  
  
## <a name="arguments"></a>参数  
 `assembly_name`  
 .netmodule 可以访问其非公共类型的程序集的名称。  
  
## <a name="remarks"></a>备注  
 生成 .netmodule 时，应使用 /moduleassemblyname 并满足以下条件：  
  
-   .netmodule 需要具有访问现有程序集中非公共类型的权限。  
  
-   知道生成后的 .netmodule 所在程序集的名称。  
  
-   现有程序集已经获得有元程序集访问权限，可访问生成后的 .netmodule 所在的程序集。  
  
 有关生成 .netmodule 的详细信息，请参阅 [/target: module（C# 编译器选项）](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)。  
  
 有关友元程序集的详细信息，请参阅[友元程序集](http://msdn.microsoft.com/library/df0c70ea-2c2a-4bdc-9526-df951ad2d055)。  
  
 此选项不适用于开发环境内，仅当从命令行编译时可用。  
  
 此编译器选项在 Visual Studio 中不可用，并且无法以编程方式更改。  
  
## <a name="example"></a>示例  
 此示例将生成包含私有类型的程序集，并且授予名为 csman_an_assembly 的程序集友元程序集访问权限。  
  
```csharp  
// moduleassemblyname_1.cs  
// compile with: /target:library  
using System;  
using System.Runtime.CompilerServices;  
  
[assembly:InternalsVisibleTo ("csman_an_assembly")]  
  
class An_Internal_Class   
{  
    public void Test()   
    {   
        Console.WriteLine("An_Internal_Class.Test called");   
    }  
}  
```  
  
## <a name="example"></a>示例  
 该例生成一个可访问程序集 moduleassemblyname_1.dll 中非公共类型的 .netmodule。 通过了解此 .netmodule 在生成后所在的程序集（名为 csman_an_assembly），可以指定 /moduleassemblyname，以便 .netmodule 在已经获得 csman_an_assembly 的友元程序集访问权限的程序集中访问非公共类型。  
  
```csharp  
// moduleassemblyname_2.cs  
// compile with: /moduleassemblyname:csman_an_assembly /target:module /reference:moduleassemblyname_1.dll  
class B {  
    public void Test() {  
        An_Internal_Class x = new An_Internal_Class();  
        x.Test();  
    }  
}  
```  
  
## <a name="example"></a>示例  
 此代码示例通过引用之前生成的程序集和 .netmodule 来生成程序集 csman_an_assembly。  
  
```csharp  
// csman_an_assembly.cs  
// compile with: /addmodule:moduleassemblyname_2.netmodule /reference:moduleassemblyname_1.dll  
class A {  
    public static void Main() {  
        B bb = new B();  
        bb.Test();  
    }  
}  
```  
  
 已调用 An_Internal_Class.Test   
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

