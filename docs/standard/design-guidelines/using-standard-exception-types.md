---
title: "使用标准异常类型 | Microsoft Docs"
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
  - "引发异常，标准类型"
  - "捕捉异常"
  - "捕获的异常"
  - "引发的异常"
ms.assetid: ab22ce03-78f9-4dca-8824-c7ed3bdccc27
caps.latest.revision: 17
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 17
---
# 使用标准异常类型
本部分介绍的框架和及其用法的详细信息中提供的标准异常。 列表并不详尽。 请参阅其他 Framework 异常类型的.NET Framework 参考文档的使用情况。  
  
## 异常和 SystemException  
 **X 不** 引发 <xref:System.Exception?displayProperty=fullName> 或 <xref:System.SystemException?displayProperty=fullName>。  
  
 **X 不** 捕获 `System.Exception` 或 `System.SystemException` 在 framework 代码中，除非您想要再次引发异常。  
  
 **X 避免** 捕捉 `System.Exception` 或 `System.SystemException`, ，除非在顶级异常处理程序。  
  
## ApplicationException  
 **X 不** 不引发异常或派生自 <xref:System.ApplicationException>。  
  
## InvalidOperationException  
 **✓ 执行** 引发 <xref:System.InvalidOperationException> 如果对象处于不合适的状态。  
  
## ArgumentException、 ArgumentNullException 和 ArgumentOutOfRangeException  
 **✓ 执行** 引发 <xref:System.ArgumentException> 或如果将错误的参数传递给成员及其子类型之一。 如果适用，更喜欢的派生程度最高的异常类型。  
  
 **✓ 执行** 设置 `ParamName` 属性时引发一个的子类 `ArgumentException`。  
  
 此属性表示导致引发异常的参数的名称。 请注意，可以使用构造函数重载之一设置该属性。  
  
 **✓ 执行** 使用 `value` 属性 setter 的隐式值参数的名称。  
  
## NullReferenceException、 IndexOutOfRangeException 和 AccessViolationException  
 **X 不** 允许公共调用 Api 来显式或隐式引发 <xref:System.NullReferenceException>, ，<xref:System.AccessViolationException>, ，或 <xref:System.IndexOutOfRangeException>。 这些异常是保留和而引发由执行引擎，并且在大多数情况下指示错误。  
  
 应进行检查以避免引发这些异常的参数。 引发这些异常会公开您可能随时间变化的方法的实现详细信息。  
  
## StackOverflowException  
 **X 不** 显式引发 <xref:System.StackOverflowException>。 应仅由 CLR 显式引发异常。  
  
 **X 不** 捕获 `StackOverflowException`。  
  
 它几乎是不可能编写托管的代码来保持一致存在任意堆栈溢出。 通过使用探测移动到明确定义的位置而导致堆栈溢出而不是从任意堆栈溢出倒出，CLR 的非托管的部分保持一致。  
  
## OutOfMemoryException  
 **X 不** 显式引发 <xref:System.OutOfMemoryException>。 此异常是仅由引发 CLR 基础结构。  
  
## ComException、 SEHException 和 ExecutionEngineException  
 **X 不** 显式引发 <xref:System.Runtime.InteropServices.COMException>,  ，<xref:System.ExecutionEngineException>, ，和 <xref:System.Runtime.InteropServices.SEHException>。 这些例外是仅由 CLR 基础结构引发。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)