---
title: "客户端验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f0c1f805-1a81-4d0d-a112-bf5e2e87a631
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 客户端验证
服务通常发布元数据以启用客户端代理类型的自动生成和配置。  如果服务不受信任，客户端应用程序应该验证元数据是否符合客户端应用程序有关安全性、事务、服务协定类型等方面的策略。  下面的示例演示如何编写一个客户端终结点行为，用于验证服务终结点以确保可以安全地使用该服务终结点。  
  
 服务公开四个终结点。  第一个终结点使用 WSDualHttpBinding，第二个终结点使用 NTLM 身份验证，第三个终结点启用事务流，第四个终结点使用基于证书的身份验证。  
  
 客户端使用 <xref:System.ServiceModel.Description.MetadataResolver> 类来检索服务的元数据。  客户端强制实施禁用双工绑定、NTLM 身份验证和使用验证行为的事务流的策略。  对于从服务的元数据导入的每个 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例，客户端应用程序会在尝试使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端连接到终结点之前，向 <xref:System.ServiceModel.Description.ServiceEndpoint> 添加 `InternetClientValidatorBehavior` 终结点行为的一个实例。  在调用服务上的任何操作之前，会运行该行为的 `Validate` 方法，并通过引发 `InvalidOperationExceptions` 强制实施客户端的策略。  
  
### 生成示例  
  
1.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
### 在同一计算机上运行示例  
  
1.  使用管理员特权打开 Visual Studio 命令提示并从示例安装文件夹运行 Setup.bat。  这将安装运行示例所需的所有证书。  
  
2.  从 \\service\\bin\\Debug 运行服务应用程序。  
  
3.  从 \\client\\bin\\Debug 运行客户端应用程序。  客户端活动将显示在客户端控制台应用程序上。  
  
4.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
5.  在运行完该示例后运行 Cleanup.bat 移除证书。  其他安全示例使用相同的证书。  
  
### 跨计算机运行示例  
  
1.  在服务器上，在使用管理员特权运行的 Visual Studio 命令提示中，键入 `setup.bat service`。  如果采用 `service` 参数运行 `` `setup.bat`，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
2.  在服务器上，编辑 App.config 以反映新证书名称。  也就是说，将 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) 元素中的 `findValue` 属性更改为计算机的完全限定域名。  
  
3.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
4.  在客户端上，使用管理员特权打开 Visual Studio 命令提示，并键入 `setup.bat client`。  如果使用 `client` `` 参数运行 `setup.bat`，则会创建一个名为 Client.com 的客户端证书，并将此客户端证书导出到名为 Client.cer 的文件中。  
  
5.  在 client.cs 文件中更改 MEX 终结点的地址值和用于设置默认服务器证书的 `findValue` 以与服务的新地址相匹配。  通过使用服务器的完全限定域名替换 localhost 来执行此操作。  请重新生成。  
  
6.  将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
7.  在客户端上，在使用管理员特权打开的 Visual Studio 命令提示中运行 ImportServiceCert.bat。  这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
8.  在服务器上，在使用管理员特权打开的 Visual Studio 命令提示中运行 ImportClientCert。  这会将 Client.cer 文件中的客户端证书导入 LocalMachine \- TrustedPeople 存储区。  
  
9. 在服务计算机上，在 Visual Studio 中生成服务项目并运行 service.exe。  
  
10. 在客户端计算机上，运行 client.exe。  
  
    1.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
### 运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
    > [!NOTE]
    >  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。  如果已运行跨计算机使用证书的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储中的服务证书。  为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <完全限定的服务器计算机名称>。例如：certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## 请参阅  
 [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)