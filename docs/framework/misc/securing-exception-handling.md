---
title: "保护异常处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "代码安全性, 异常处理"
  - "异常处理, 安全性"
  - "安全编码, 异常处理"
  - "安全性 [.NET Framework], 异常处理"
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# 保护异常处理
在 Visual C\+\+ 和 Visual Basic 中，在堆栈上部的筛选器表达式在任何 **finally** 语句之前运行。  与该筛选器关联的 **catch** 块在 **finally** 语句之后运行。  有关更多信息，请参见[使用用户筛选的异常](../../../docs/standard/exceptions/using-user-filtered-exception-handlers.md)。  本节讨论上述顺序的安全含义。  请看下面的伪代码示例，其中演示了筛选语句和 **finally** 语句的运行顺序。  
  
```cpp  
void Main()   
{  
    try   
    {  
        Sub();  
    }   
    except (Filter())   
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()   
{  
    try   
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }   
    finally   
    {  
        Console.WriteLine("finally");  
    }  
}                        
```  
  
 该代码将输出下面的内容。  
  
```  
Throw  
Filter  
Finally  
Catch  
```  
  
 该筛选器在 **finally** 语句之前运行，这样，任何会更改状态的做法都可能引发安全问题，因为其他代码的执行可能会利用这种状态更改。  例如：  
  
```cpp  
try   
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and   
    // so on) that could be exploited if malicious   
    // code ran before state is restored.  
    Do_some_work();  
}   
finally   
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 该伪代码允许位于堆栈较上部的筛选器运行任意代码。  可能会产生类似效果的其他操作示例有：临时模拟另一个标识；设置跳过某种安全检查的内部标志；更改与线程关联的区域性。  建议采纳的解决方案是引入一个异常处理程序，用于将代码对线程状态的更改与调用方的筛选器块分开。  然而，重要的是必须正确地引入异常处理程序，否则，就无法解决这一问题。  下面的示例切换用户界面区域性，但任何一种线程状态更改都可采用类似的方式公开。  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",   
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 在这种情况下，正确的修复方法是将现有的 **try**\/**finally** 块包装到 **try**\/**catch** 块中。  仅仅将 **catch\-throw** 子句引入到现有的 **try**\/**finally** 块中不能修复该问题，如下面的示例所示。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try   
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally   
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 这样不能修复上述问题，原因在于：在 `FilterFunc` 获得控制之前，没有运行 **finally** 语句。  
  
 下面的示例通过确保在向调用方的异常筛选器块提供异常之前执行 **finally** 子句，修复了上述问题。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try    
    {  
        try   
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally   
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)