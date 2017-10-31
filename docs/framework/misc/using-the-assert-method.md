---
title: "使用 Assert 方法 | Microsoft Docs"
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
  - "Assert 方法"
  - "断言的权限"
  - "调用方安全检查"
  - "代码访问安全性, 重写安全检查"
  - "授予权限, 重写安全检查"
  - "重写安全检查"
  - "权限 [.NET Framework], 断言"
  - "权限 [.NET Framework], 重写安全检查"
  - "安全性 [.NET Framework], 断言"
  - "安全性 [.NET Framework], 重写安全检查"
ms.assetid: 1e40f4d3-fb7d-4f19-b334-b6076d469ea9
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 18
---
# 使用 Assert 方法
<xref:System.Security.CodeAccessPermission.Assert%2A> 是一种可在代码访问权限类和 <xref:System.Security.PermissionSet> 类上调用的方法。  可以使用 **Assert**，让你的代码（和下游调用方）可以执行代码有权执行但其调用方可能无权执行的操作。  安全断言会更改在安全检查期间运行时所执行的正常过程。  断言权限时，它会通知安全系统不检查断言权限的代码的调用方。  
  
> [!CAUTION]
>  请谨慎使用断言，因为它们会打开安全漏洞并破坏运行时强制执行安全限制的机制。  
  
 当库调用非托管代码或所执行的调用需要与库的预期用途不明显关联的权限时，断言非常有用。  例如，所有调用非托管代码的托管代码都必须具有指定了 **UnmanagedCode** 标志的 **SecurityPermission**。  默认情况下，如果代码不是来自本地计算机（如从本地 intranet 下载的代码），则不会对其授予此权限。  因此，为了使从本地 intranet 下载的代码能调用使用非托管代码的库，它必须具有由该库断言的权限。  此外，某些库可能会执行对调用方不可见且需要特殊权限的调用。  
  
 在代码以对调用方完全不可见的方式访问资源时，也可使用断言。  例如，假设你的库从数据库获取信息，但在此过程中还会从计算机注册表读取信息。  因为用你的库的开发人员无权访问你的源，所以他们无法知道其代码需要 **RegistryPermission** 才能使用你的代码。  在此情况下，如果你决定要求代码调用方有权访问注册表是不合理或不必要的，你可以断言权限以读取注册表。  在这种情况下，库可以断言权限以使没有 **RegistryPermission** 的调用方可使用该库。  
  
 仅当断言权限和下游调用方所需的权限属于同一类型且要求的权限是断言权限的子集时，断言才会影响堆栈审核。  例如，如果你断言 **FileIOPermission** 以读取 C 驱动器上的所有文件，且提出 **FileIOPermission** 读取 C:\\Temp 中的文件的下游要求，则断言可能会影响堆栈审核；但是，如果是要求 **FileIOPermission** 写入到 C 驱动器，则断言不起作用。  
  
 若要执行断言，必须向你的代码授予正在断言的权限以及表示有权执行断言的 <xref:System.Security.Permissions.SecurityPermission>。  虽然你可以断言尚未授予代码的权限，但此断言毫无意义，因为安全检查在断言使其成功之前就会失败。  
  
 下图显示了使用 **Assert** 将发生的情况。  假设以下语句针对程序集 A、B、C、E 和 F 以及 P1 和 P1A 两个权限为 true：  
  
-   P1A 表示读取 C 驱动器上的 .txt 文件的权限。  
  
-   P1 表示读取 C 驱动器上所有文件的权限。  
  
-   P1A 和 P1 都是 **FileIOPermission** 类型，且 P1A 是 P1 的子集。  
  
-   已向程序集 E 和 F 授予了 P1A 权限。  
  
-   已向程序集 C 授予了 P1 权限。  
  
-   尚未向程序集 A 和 B 授予 P1 或 P1A 权限。  
  
-   方法 A 包含在程序集 A 中，方法 B 包含在程序集 B 中，依次类推。  
  
 ![](../../../docs/framework/misc/media/assert.gif "assert")  
使用断言  
  
 在此方案中，方法 A 调用 B、B 调用 C、C 调用 E、而 E 调用 F。  方法 C 断言权限来读取 C 驱动器上的文件（权限 P1），方法 E 要求权限以限读取 C 驱动器上的 .txt 文件（权限 P1A）。  在运行时遇到 F 中的要求时，将执行堆栈审核，以从 E 开始检查 F 的所有调用方的权限。  已向 E 授予 P1A 权限，所以将继续执行堆栈审核以检查 C 的权限（其中已发现 C 的断言）。  因为要求的权限 \(P1A\) 是断言的权限 \(P1\) 的子集，所以堆栈审核将停止且安全检查会自动成功。  未向程序集 A 和 B 授予权限 P1A 并不重要。  通过断言 P1，方法 C 确保其调用方可以访问受 P1 保护的资源，即使尚未授予调用方访问该资源的权限也是如此。  
  
 如果你设计一个类库且某个类访问受保护的资源，则在大多数情况下，你应该提出安全要求，要求此类的调用方拥有适当的权限。  如果该类随后会执行一个你知道其大多数调用方均无权执行的操作，并且如果你愿意为允许这些调用方调用你的代码承担责任，则你可以通过调用权限对象上的 **Assert** 方法来断言权限，其中该对象表示代码正在执行的操作。  以此方式使用 **Assert** 使得通常不可调用你的代码的调用方也能够执行此操作。  因此，如果你断言了一个权限，应确保预先执行了适当的安全检查，以防止你的组件被误用。  
  
 例如，假设你的高度受信任的库类具有删除文件的方法。  它通过调用非托管的 Win32 函数来访问文件。  调用方调用代码的 **Delete** 方法，已使用要删除的文件的名称 C:\\Test.txt 进行传递。  在 **Delete** 方法中，你的代码会创建一个 <xref:System.Security.Permissions.FileIOPermission> 对象，它表示对 C:\\Test.txt 的写权限。  （需要写权限来删除文件。） 然后你的代码会通过调用 **FileIOPermission** 对象的 **Demand** 方法来调用命令性安全检查。  如果调用堆栈中的某个调用方不具有此权限，则会引发 <xref:System.Security.SecurityException>。  如果未引发任何异常，你会知道所有调用方都有权限访问 C:\\Test.txt。  因为你确信大多数调用方都没有访问非托管代码的权限，所以随后你的代码会创建一个 <xref:System.Security.Permissions.SecurityPermission> 对象，它表示有权调用非托管代码，并调用该对象的 **Assert** 方法。  最后，它会调用非托管的 Win32 函数来删除 C:\\Text.txt，并将控件返回给调用方。  
  
> [!CAUTION]
>  你必须确保你的代码在以下情况下不使用断言：其他代码可使用你的代码来访问由你正在断言的权限所保护的资源。  例如，在写入其名称由调用方指定为参数的文件的代码中，不可断言 **FileIOPermission** 来写入文件，因为你的代码将可能被第三方误用。  
  
 当使用命令性安全语法时，在多个权限上以相同方式调用 **Assert** 方法会引发安全性异常。  应改为创建 **PermissionSet** 对象，向它传递你想要调用的单个权限，然后调用 **PermissionSet** 对象上的 **Assert** 方法。  在使用声明性安全语法时，可以多次调用 **Assert** 方法。  
  
 下列示例演示了使用 **Assert** 方法来重写安全检查的声明性语法。  请注意，**FileIOPermissionAttribute** 语法采用两个值：<xref:System.Security.Permissions.SecurityAction> 枚举以及要向其授予权限的文件或目录的位置。  对 **Assert** 的调用会使得访问 `C:\Log.txt` 的要求成功，即使未检查调用方是否有访问文件的权限也是如此。  
  
```vb  
Option Explicit  
Option Strict  
  
Imports System  
Imports System.IO  
Imports System.Security.Permissions  
  
Namespace LogUtil  
   Public Class Log  
      Public Sub New()  
  
      End Sub  
  
     <FileIOPermission(SecurityAction.Assert, All := "C:\Log.txt")> Public Sub   
      MakeLog()  
         Dim TextStream As New StreamWriter("C:\Log.txt")  
         TextStream.WriteLine("This  Log was created on {0}", DateTime.Now) '  
         TextStream.Close()  
      End Sub  
   End Class  
End Namespace  
  
```  
  
```csharp  
namespace LogUtil  
{  
   using System;  
   using System.IO;  
   using System.Security.Permissions;  
  
   public class Log  
   {  
      public Log()  
      {      
      }     
      [FileIOPermission(SecurityAction.Assert, All = @"C:\Log.txt")]  
      public void MakeLog()  
      {     
         StreamWriter TextStream = new StreamWriter(@"C:\Log.txt");  
         TextStream.WriteLine("This  Log was created on {0}", DateTime.Now);  
         TextStream.Close();  
      }  
   }  
}   
```  
  
 下列代码片段演示了使用 **Assert** 方法来重写安全检查的命令性语法。  在此示例中，声明了 **FileIOPermission** 对象的实例。  将向其构造函数传递 **FileIOPermissionAccess.AllAccess** 以定义允许的访问类型，并且此函数后接一个描述文件位置的字符串。  定义 **FileIOPermission** 对象后，只需调用其 **Assert** 方法即可重写安全检查。  
  
```vb  
Option Explicit  
Option Strict  
Imports System  
Imports System.IO  
Imports System.Security.Permissions  
Namespace LogUtil  
   Public Class Log  
      Public Sub New()  
      End Sub 'New  
  
      Public Sub MakeLog()  
         Dim FilePermission As New FileIOPermission(FileIOPermissionAccess.AllAccess, "C:\Log.txt")  
         FilePermission.Assert()  
         Dim TextStream As New StreamWriter("C:\Log.txt")  
         TextStream.WriteLine("This  Log was created on {0}", DateTime.Now)  
         TextStream.Close()  
      End Sub  
   End Class  
End Namespace  
  
```  
  
```csharp  
namespace LogUtil  
{  
   using System;  
   using System.IO;  
   using System.Security.Permissions;  
  
   public class Log  
   {  
      public Log()  
      {      
      }     
      public void MakeLog()  
      {  
         FileIOPermission FilePermission = new FileIOPermission(FileIOPermissionAccess.AllAccess,@"C:\Log.txt");   
         FilePermission.Assert();  
         StreamWriter TextStream = new StreamWriter(@"C:\Log.txt");  
         TextStream.WriteLine("This  Log was created on {0}", DateTime.Now);  
         TextStream.Close();  
      }  
   }  
}  
```  
  
## 请参阅  
 <xref:System.Security.PermissionSet>   
 <xref:System.Security.Permissions.SecurityPermission>   
 <xref:System.Security.Permissions.FileIOPermission>   
 <xref:System.Security.Permissions.SecurityAction>   
 [特性](../../../docs/standard/attributes/index.md)   
 [代码访问安全性](../../../docs/framework/misc/code-access-security.md)