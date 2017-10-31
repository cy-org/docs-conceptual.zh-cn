---
title: "安全和争用条件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "代码安全性, 争用条件"
  - "争用条件"
  - "安全编码, 争用条件"
  - "安全性 [.NET Framework], 争用条件"
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 安全和争用条件
另一个需要关注的方面是争用条件可能会利用安全漏洞。  可能利用的方式有好几种。  下面的副主题概述了开发人员必须避免的几种主要陷阱。  
  
## Dispose 方法中的争用条件  
 如果某个类的 **Dispose** 方法（有关更多信息，请参见 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)）没有进行同步，则 **Dispose** 内的清除代码可能会运行多次，如下面的示例所示。  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
  
```  
  
```csharp  
void Dispose()   
{  
    if( myObj != null )   
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
 由于此 **Dispose** 实现未进行同步，因此在将 `_myObj` 设置为 **null** 之前，第一个线程及随后的第二个线程均可调用 `Cleanup`。  这是否会成为一个安全问题取决于运行 `Cleanup` 代码时发生了什么情况。  未同步的 **Dispose** 实现出现的重要问题需要使用资源句柄（例如文件）。  不适当的处理可能导致使用错误的句柄，这通常会造成安全弱点。  
  
## 构造函数中的争用条件  
 在某些应用程序中，其他线程可能在它们的类构造函数完全运行之前访问类成员。  您应当检查所有的类构造函数以确保发生这种情况时不会出现安全问题，或者根据需要同步线程。  
  
## 缓存对象的争用条件  
 如果类的其他部分没有被适当地同步，缓存安全信息的代码或使用代码访问安全 [Assert](../../../docs/framework/misc/using-the-assert-method.md) 操作的代码也很容易受到争用条件的影响，具体情况如下面的示例所示。  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False()  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
  
```  
  
```csharp  
void SomeSecureFunction()   
{  
    if(SomeDemandPasses())   
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false();  
    }  
}  
void DoOtherWork()   
{  
    if( fCallersOK )   
    {  
        DoSomethingTrusted();  
    }  
    else   
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
 对于可以使用同一对象从其他线程调用的 `DoOtherWork`，如果存在到达它的其他路径，则不受信任的调用方就可以绕过请求。  
  
 如果您的代码缓存了安全信息，请确保从安全信息中查找这一弱点。  
  
## Finalizer 中的争用条件  
 在引用静态资源或非托管资源的对象（该对象随后会在其终结器中释放这一资源）中，也可能出现争用条件。  如果多个对象共享同一个在类的终结器中操作的资源，则这些对象必须同步所有对该资源的访问。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)