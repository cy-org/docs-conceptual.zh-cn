---
title: "异常类和属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Exception 类"
  - "异常, Exception 类"
ms.assetid: e2e1f8c4-e7b4-467d-9a66-13c90861221d
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 异常类和属性
<xref:System.Exception> 类是异常从其进行继承的基类。  大多数异常对象都是 **Exception** 的某个派生类的实例，不过，任何从 <xref:System.Object> 类派生的对象都可以作为异常引发。  请注意，并非所有语言都支持引发和捕捉不从 **Exception** 派生的对象。  在几乎任何情况下，都建议仅引发和捕捉 **Exception** 对象。  
  
 **Exception** 类的若干属性使了解异常更容易。  这些属性包括：  
  
-   <xref:System.Exception.StackTrace%2A> 属性。  
  
     此属性包含可用来确定错误发生位置的堆栈跟踪。  如果有可用的调试信息，则堆栈跟踪包含源文件名和程序行号。  
  
-   <xref:System.Exception.InnerException%2A> 属性。  
  
     此属性可用来在异常处理过程中创建和保留一系列异常。  可使用此属性创建一个新异常来包含以前捕捉的异常。  原始异常可由 **InnerException** 属性中的第二个异常捕获，这使处理第二个异常的代码可以检查附加信息。  
  
     例如，假设有一个读取文件并格式化相应数据的方法。  代码尝试从文件读取，但引发 FileException。  该方法捕捉 FileException 并引发 BadFormatException。  在此情况下，FileException 可保存在 BadFormatException 的 **InnerException** 属性中。  
  
     为提高调用方确定异常引发原因的能力，有时可能需要方法捕捉帮助器例程引发的异常，然后引发一个进一步指示已发生的错误的异常。  可以创建一个更有意义的新异常，其中内部异常引用可以设置为原始异常。  然后可以针对调用方引发这种更有意义的异常。  请注意，使用此功能，可以创建以最先引发的异常作为结束点的一系列相链接的异常。  
  
-   <xref:System.Exception.Message%2A> 属性。  
  
     此属性提供有关异常起因的详细信息。  **Message** 以引发异常的线程的 <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=fullName> 属性所指定的语言显示。  
  
-   <xref:System.Exception.HelpLink%2A> 属性。  
  
     此属性可保存某个帮助文件的 URL（或 URN），该文件提供有关异常起因的大量信息。  
  
-   <xref:System.Exception.Data%2A> 属性  
  
     此属性是可以保存任意数据（以键值对的形式）的 IDictionary。  
  
 大多数从 **Exception** 继承的类都不实现其他成员或提供附加功能；它们只是从 **Exception** 继承。  因此，在异常层次结构、异常名称以及异常包含的信息中可以找到有关异常的最重要信息。  
  
## 请参阅  
 [异常层次结构](../../../docs/standard/exceptions/exception-hierarchy.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [异常的最佳做法](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [异常](../../../docs/standard/exceptions/index.md)