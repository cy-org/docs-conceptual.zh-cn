---
title: "如何：暂停 Windows 服务 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ServiceController.Pause"
helpviewer_keywords: 
  - "暂停 Windows 服务应用程序"
  - "Windows 服务应用程序, 暂停"
ms.assetid: eddb9409-942b-46b6-a2ce-fbd4c65f2790
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 15
---
# 如何：暂停 Windows 服务 (Visual Basic)
此示例使用 <xref:System.ServiceProcess.ServiceController> 组件暂停本地计算机上的 IIS 管理服务。  
  
## 示例  
 [!code-vb[VbRadconService#11](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#11)]  
[!code-vb[VbRadconService#12](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#12)]  
  
 此代码示例也可用作 IntelliSense 代码段。  在代码段选择器中，它位于**“Windows 操作系统”\>“Windows 服务”**中。  有关更多信息，请参见 [代码段](../Topic/Code%20Snippets.md)。  
  
## 编译代码  
 此示例需要：  
  
-   对 System.serviceprocess.dll 的项目引用。  
  
-   对 <xref:System.ServiceProcess> 命名空间中的成员的访问权限。  如果代码中的成员名称没有完全限定，则需要添加一条 `Imports` 语句。  有关更多信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../ocs/visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
## 可靠编程  
 默认情况下，<xref:System.ServiceProcess.ServiceController> 类的 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 属性是本地计算机。  若要引用另一台计算机上的 Windows 服务，请将 <xref:System.ServiceProcess.ServiceController.MachineName%2A> 属性更改为该计算机的名称。  
  
 以下情况可能会导致异常：  
  
-   服务不能被暂停。  （[InvalidOperationException 类](frlrfSystemInvalidOperationExceptionClassTopic)）  
  
-   在访问系统 API 时发生错误。  （[Win32Exception 类](frlrfSystemComponentModelWin32ExceptionClassTopic)）  
  
## .NET Framework 安全性  
 可以对计算机上的服务控制加以限制，方法是使用 [ServiceControllerPermissionAccess 枚举](frlrfSystemServiceProcessServiceControllerPermissionAccessClassTopic)在 [ServiceControllerPermission 类](frlrfSystemServiceProcessServiceControllerPermissionClassTopic)中设置权限。  
  
 可以对服务信息访问加以限制，方法是使用 [PermissionState 枚举](frlrfSystemSecurityPermissionsPermissionStateClassTopic)在 [SecurityPermission 类](frlrfSystemSecurityPermissionsSecurityPermissionClassTopic)中设置权限。  
  
## 请参阅  
 <xref:System.ServiceProcess.ServiceController>   
 <xref:System.ServiceProcess.ServiceControllerStatus>   
 <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A>   
 [如何：继续 Windows 服务 \(Visual Basic\)](../../../docs/framework/windows-services/how-to-continue-a-windows-service-visual-basic.md)