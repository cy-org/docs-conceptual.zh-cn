---
title: "nameof（C# 参考）"
ms.date: 2017-06-16
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- nameof_CSharpKeyword
- nameof
dev_langs:
- CSharp
ms.assetid: 33601bf3-cc2c-4496-846d-f9679bccf2a7
caps.latest.revision: 3
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
ms.openlocfilehash: db79af5f38439b881863cf3e03aa0e684ec5cd39
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="nameof-c-reference"></a>nameof（C# 参考）

用于获取变量、类型或成员的简单（非限定）字符串名称。  

在报告代码中的错误、挂接“模型-视图-控制器”(MVC) 链接、触发属性更改事件时，你通常会希望捕获方法的字符串名称。  使用 `nameof` 有助于在重命名定义时使代码始终有效。  以前必须使用字符串来引用定义，在重命名代码元素时，此方法很脆弱，因为工具不知道要检查这些字符串。  
  
 `nameof` 表达式具有此形式：  
  
```csharp  
if (x == null) throw new ArgumentNullException(nameof(x));  
WriteLine(nameof(person.Address.ZipCode)); // prints "ZipCode"  
```  
  
## <a name="key-use-cases"></a>关键用例  
 这些示例显示 `nameof` 的关键用例。  
  
 验证参数：  
 ```csharp  
void f(string s) {  
    if (s == null) throw new ArgumentNullException(nameof(s));  
}  
```  
  
 MVC 操作链接：  
 ```html  
<%= Html.ActionLink("Sign up",  
             @typeof(UserController),  
             @nameof(UserController.SignUp))  
%>  
```  
  
 INotifyPropertyChanged：  
 ```csharp  
int p {  
    get { return this.p; }  
    set { this.p = value; PropertyChanged(this, new PropertyChangedEventArgs(nameof(this.p)); } // nameof(p) works too  
}  
```  
  
 XAML 依赖项属性：  
 ```csharp  
public static DependencyProperty AgeProperty = DependencyProperty.Register(nameof(Age), typeof(int), typeof(C));  
```  
  
 日志记录：  
 ```csharp  
void f(int i) {  
    Log(nameof(f), "method entry");  
}  
```  
  
 特性:  
 ```csharp  
[DebuggerDisplay("={" + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```  
  
## <a name="examples"></a>示例  
 一些 C# 示例：  
  
```csharp  
using Stuff = Some.Cool.Functionality  
class C {  
    static int Method1 (string x, int y) {}  
    static int Method1 (string x, string y) {}  
    int Method2 (int z) {}  
    string f<T>() => nameof(T);  
}  
  
var c = new C()  
  
nameof(C) -> "C"  
nameof(C.Method1) -> "Method1"   
nameof(C.Method2) -> "Method2"  
nameof(c.Method1) -> "Method1"   
nameof(c.Method2) -> "Method2"  
nameof(z) -> "z" // inside of Method2 ok, inside Method1 is a compiler error  
nameof(Stuff) = "Stuff"  
nameof(T) -> "T" // works inside of method but not in attributes on the method  
nameof(f) -> "f"  
nameof(f<T>) -> syntax error  
nameof(f<>) -> syntax error  
nameof(Method2()) -> error "This expression does not have a name"  
```  
  
## <a name="remarks"></a>备注  
 `nameof` 的参数必须是简单名称、限定名称、成员访问、指定成员的基访问或指定成员的此类访问。  参数表达式标识代码定义，但从不进行计算。  
  
 因为在语法上参数必须为表达式，因此有很多禁用内容无需列出。  以下内容会产生错误，值得一提：预定义的类型（如 `int` 或 `void`）、可以为 null 的类型（`Point?`）、数组类型（`Customer[,]`）、指针类型 (`Buffer*`)、限定别名 (`A::B`)、未绑定的泛型类型 (`Dictionary<,>`)、预处理符号 (`DEBUG`) 和标签 (`loop:`)。  
  
 如果需要获取完全限定名，可以将 `typeof` 表达式和 `nameof`结合使用。  例如：
```csharp  
class C {
    void f(int i) {  
        Log($"{typeof(C)}.{nameof(f)}", "method entry");  
    }
}
``` 

 遗憾的是，`typeof` 不是类似于 `nameof` 的常数表达式，因此，不能在 `nameof` 的所有相同位置将 `typeof` 和 `nameof` 结合使用。  例如，以下操作会导致 CS0182 编译错误：
 ```csharp  
[DebuggerDisplay("={" + typeof(C) + nameof(GetString) + "()}")]  
class C {  
    string GetString() { }  
}  
```    
 在这些示例中，显示了可使用类型名称并访问实例方法名称。  按照计算表达式的要求，无需具有类型的实例。  在某些情况下使用类型名称非常方便，因为只引用名称而不使用实例数据，因此不必构建实例变量或表达式。  
  
 你可以引用类中特性表达式的类成员。  
  
 无法获取类似于“`Method1 (str, str)`”的签名信息。  实现该操作的一种方法是使用表达式 `Expression e = () => A.B.Method1("s1", "s2")`，并从生成的表达式树中拉取 MemberInfo。  
  
## <a name="language-specifications"></a>语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 

