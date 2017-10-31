---
title: "使用 WCF 开发工具 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 使用 WCF 开发工具
本节描述有助于开发 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 服务的 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 开发工具。  
  
 可以以 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 模板为基础快速生成自己的服务，然后使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务自动主机和 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端对您的服务进行调试和测试。  通过一起使用这些工具，可以快速完美地完成调试和测试过程，无需在早期阶段提交给承载模型。  
  
## WCF 开发人员工具  
 [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)  
  
 可以在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中使用预定义的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 项目和项模板快速生成 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务和周边应用程序。  
  
 [WCF 服务主机 \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务自动主机 \(WcfSvcHost.exe\) 允许您启动 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 调试器 \(F5\) 以自动承载和测试已实现的服务。  然后可以使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端 \(wcfTestClient.exe\) 或您自己的客户端来测试服务，以查找并解决任何潜在错误。  
  
 [WCF 测试客户端 \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\) 是一个 GUI 工具，通过使用该工具，可以输入任意类型的参数、将该输入提交给服务并查看服务发回的响应。  当与 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务自动主机结合时，它可以提供完美的服务测试体验。  
  
 [从 XML 生成数据类型类](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md)  
  
 可将存储在剪贴板中的 XML 数据粘贴到代码页中。  数据中定义的类将被转换为代码类型。  
  
## 在无管理员权限的情况下使用工具  
 为了使没有管理员权限的用户能够开发 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务，在安装 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的过程中为命名空间“http:\/\/\+:8731\/Design\_Time\_Addresses”创建了一个 ACL（访问控制列表）。  该 ACL 被设置为“\(UI\)”，这将包括登录到此计算机的所有交互用户。  管理员可以在此 ACL 中添加或移除用户，或者打开其他端口。此 ACL 支持 WCF 或 WF 模板以其各自的默认配置发送和接收数据。  它还使用户能够使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务自动主机 \(wcfSvcHost.exe\)，而无需向他们授予管理员权限。  
  
 可以使用提升的管理员帐户在 [!INCLUDE[wv](../../../includes/wv-md.md)] 中通过 Netsh.exe 工具来修改访问权限。  下面是使用 Netsh.exe 的示例。  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] Netsh.exe 的更多信息，请参见[如何使用 Netsh.exe 工具和命令行开关](http://go.microsoft.com/fwlink/?LinkId=97877)。  
  
## 请参阅  
 [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)   
 [WCF 服务主机 \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)   
 [WCF 测试客户端 \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)