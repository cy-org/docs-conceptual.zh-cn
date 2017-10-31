---
title: "后期绑定重载决策不能应用于“&lt;过程名&gt;”，因为访问实例是一个接口类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30933"
  - "bc30933"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30933"
  - "重载决策, 使用后期绑定参数"
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 后期绑定重载决策不能应用于“&lt;过程名&gt;”，因为访问实例是一个接口类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

编译器尝试解析对重载属性或过程的引用，但引用失败，原因是某个参数的类型为 `Object`，而且引用对象具有接口数据类型。  `Object` 参数强制编译器将引用解析为后期绑定。  
  
 在这些情况下，编译器通过实现类而不是通过基础接口来解析重载。  如果类重命名了其中一个重载版本，则编译器不会将该版本视为重载，原因是它具有不同的名称。  而这反过来会使编译器在重命名的版本可能是解析引用的正确选择时忽略此版本。  
  
 **错误 ID：**BC30933  
  
### 更正此错误  
  
-   使用 `CType` 将参数从 `Object` 强制转换为由您要调用的重载的签名指定的类型。  
  
     请注意，将引用对象强制转换为基础接口并无帮助。  必须强制转换参数才能避免此错误。  
  
## 示例  
 下面的示例演示对重载的 `Sub` 过程（将导致此错误在编译时出现）的调用。  
  
```  
Module m1  
    Interface i1  
        Sub s1(ByVal p1 As Integer)  
        Sub s1(ByVal p1 As Double)  
    End Interface  
    Class c1  
        Implements i1  
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1  
        End Sub  
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1  
        End Sub  
    End Class  
    Sub Main()  
        Dim refer As i1 = New c1  
        Dim o1 As Object = 3.1415  
        ' The following reference is INVALID and causes a compiler error.  
        refer.s1(o1)   
    End Sub  
End Module  
```  
  
 在前面的示例中，如果编译器允许所编写的对 `s1` 的调用，则解析将通过类 `c1` 而不是接口 `i1` 进行。  这将意味着编译器不会考虑 `s2`，原因是它在 `c1` 中具有不同的名称，即使它是由 `i1` 定义的正确选择也是如此。  
  
 可以通过将调用改为以下任一行代码来更正此错误：  
  
```  
refer.s1(CType(o1, Integer))  
refer.s1(CType(o1, Double))  
```  
  
 上面每一行代码都显式地将 `Object` 变量 `o1` 强制转换为已为重载定义的一种参数类型。  
  
## 请参阅  
 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [重载决策](../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)