---
title: "链接需求 | Microsoft Docs"
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
  - "调用方安全检查"
  - "代码访问安全性, 需求"
  - "要求的权限"
  - "授予权限, 需求"
  - "链接需求"
  - "权限 [.NET Framework], 需求"
  - "安全性 [.NET Framework], 需求"
  - "用户的权限需求"
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
caps.latest.revision: 18
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# 链接需求
链接要求导致在实时编译过程中进行安全检查，并且只检查代码的直接调用程序集。  当代码绑定到类型引用（包括函数指针引用和方法调用）时发生链接。  如果调用程序集的权限不足以链接到代码，则加载并运行代码时将不允许该链接且将引发运行时异常。  可在继承自代码的类中重写链接要求。  
  
 请注意，不使用此类型的要求执行完整的堆栈审核，并且代码仍容易遭受引诱攻击。  例如，如果程序集 A 中的方法受链接要求的保护，则将基于程序集 B 的权限计算程序集 B 中的直接调用方。  但是，如果链接要求使用程序集 B 中的方法间接调用程序集 A 中的方法，则它将不会计算程序集 C 中的方法。  链接要求只指定直接调用程序集中的直接调用方为了链接到你的代码所必须拥有的权限。  而不指定所有调用方为了运行你的代码所必须拥有的权限。  
  
 <xref:System.Security.CodeAccessPermission.Assert%2A>、<xref:System.Security.CodeAccessPermission.Deny%2A> 和 <xref:System.Security.CodeAccessPermission.PermitOnly%2A> 堆栈审核修饰符不影响链接要求计算。  由于链接要求不执行堆栈审核，所以堆栈审核修饰符对链接要求并无影响。  
  
 如果通过[反射](../../../docs/framework/reflection-and-codedom/reflection.md)访问链接要求保护的方法，则链接要求将检查通过反射访问的代码的直接调用方。  对于使用反射执行的方法发现和方法调用都是如此。  例如，假设代码使用反射来返回表示受链接要求保护的方法的 <xref:System.Reflection.MethodInfo> 对象，然后将 **MethodInfo** 对象传递给使用该对象来调用原始方法的一些其他代码。  在这种情况下，链接要求会进行两次检查：一次针对返回 **MethodInfo** 对象的代码，一次针对调用该对象的代码。  
  
> [!NOTE]
>  在静态类构造函数上执行的链接要求不保护构造函数，因为静态构造函数是在应用程序的代码执行路径外部由系统调用的。  因此，当链接要求应用于整个类时，它不能保护对静态构造函数的访问，尽管它确实保护类的其余部分。  
  
 下面的代码片段以声明方式指定链接到 `ReadData` 方法的任何代码必须具有 `CustomPermission` 权限。  此权限是假设的自定义权限，在 .NET Framework 中并不存在。  通过将 **SecurityAction.LinkDemand** 标记传递到 `CustomPermissionAttribute` 来生成该要求。  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function    
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## 请参阅  
 [特性](../../../docs/standard/attributes/index.md)   
 [代码访问安全性](../../../docs/framework/misc/code-access-security.md)