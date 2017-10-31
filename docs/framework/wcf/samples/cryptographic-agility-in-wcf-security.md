---
title: "WCF 安全中的加密灵活性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# WCF 安全中的加密灵活性
本示例演示如何在标准\/自定义算法中进行指定，以便在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端和服务中提供加密的敏捷实现。  该示例由下列项目组成：  
  
 服务  
 这是一个自承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，该服务实现 `ICalculator` 接口并使用禁用了安全会话和可靠会话的 <xref:System.ServiceModel.WsHttpBinding> 来保证终结点安全。  该服务定义一个自定义 `SecurityAlgorithmSuite` 类，以指定要用于消息安全的加密算法。  
  
 客户端  
 这是在身份验证成功后访问服务的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端。  该客户端调用由 `ICalculator` 接口公开并由服务实现的操作。  该客户端也定义相同的自定义 `SecurityAlgorithmSuite` 类，以指定要用于消息安全的加密算法。  
  
### 使用此示例  
  
1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开 CryptoAgility.sln 解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  打开[!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)]并导航到 \\WCF\\Basic\\Security\\CryptoAgility\\Service\\bin 目录，右击 service.exe 并选择**“以管理员身份运行”**，从而使用管理员特权运行 service.exe 文件。  
  
4.  导航到 \\WCF\\Basic\\Security\\CryptoAgility\\Client\\bin 目录并正常运行 client.exe 文件。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`  
  
## 请参阅  
 [安全性](../../../../docs/framework/wcf/feature-details/security.md)