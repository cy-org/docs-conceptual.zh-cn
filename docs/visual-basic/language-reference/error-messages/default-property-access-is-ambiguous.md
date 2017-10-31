---
title: "默认属性访问在接口“&lt;接口名 1&gt;”的继承接口成员“&lt;默认属性名&gt;”和接口“&lt;接口名 2&gt;”的“&lt;默认属性名&gt;”之间不明确 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30686"
  - "bc30686"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30686"
ms.assetid: 784fefec-ef57-48cf-b960-957df419b439
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 默认属性访问在接口“&lt;接口名 1&gt;”的继承接口成员“&lt;默认属性名&gt;”和接口“&lt;接口名 2&gt;”的“&lt;默认属性名&gt;”之间不明确
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

某个接口从两个接口继承，这两个接口的每个接口都声明一个同名的默认属性。  编译器无法不加限定地将某个访问解析到此默认属性。  下面的示例阐释了这一点。  
  
```  
Public Interface Iface1  
    Default Property prop(ByVal arg As Integer) As Integer  
End Interface  
Public Interface Iface2  
    Default Property prop(ByVal arg As Integer) As Integer  
End Interface  
Public Interface Iface3  
    Inherits Iface1, Iface2  
End Interface  
Public Class testClass  
    Public Sub accessDefaultProperty()  
        Dim testObj As Iface3  
        Dim testInt As Integer = testObj(1)  
    End Sub  
End Class  
```  
  
 当您指定 `testObj(1)` 时，编译器尝试将其解析到默认属性。  但是，由于是继承的接口，有两个可能的默认属性，所以，编译器会发出信号告知此错误。  
  
 **错误 ID：**BC30686  
  
### 更正此错误  
  
-   避免继承任何同名成员。  在前面的示例中，如果 `testObj` 不需要任何成员（例如 `Iface2` 的成员），则按如下所示声明它：  
  
    ```  
    Dim testObj As Iface1  
    ```  
  
     \- 或 \-  
  
-   在类中实现继承接口。  然后，您可以实现每个不同名称的继承属性。  但是，它们中只有一个可以是实现类的默认属性。  下面的示例阐释了这一点。  
  
    ```  
    Public Class useIface3  
        Implements Iface3  
        Default Public Property prop1(ByVal arg As Integer) As Integer Implements Iface1.prop  
            ' Insert code to define Get and Set procedures for prop1.  
        End Property  
        Public Property prop2(ByVal arg As Integer) As Integer Implements Iface2.prop  
            ' Insert code to define Get and Set procedures for prop2.  
        End Property  
    End Class  
    ```  
  
## 请参阅  
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)