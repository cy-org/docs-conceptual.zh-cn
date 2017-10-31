---
title: "与 COM 应用程序集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "COM [WCF]"
  - "COM [WCF], Windows Communication Foundation 集成"
  - "WCF, COM 集成"
  - "WCF, 重用代码"
  - "Windows Communication Foundation, COM 集成"
  - "Windows Communication Foundation, 重用代码"
ms.assetid: c98bda3e-6779-419e-8e6d-9aa94053026d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 与 COM 应用程序集成
通过使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务标记，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务可直接集成到现有代码中。  服务标记可以在众多基于 COM 的开发环境（如 Office VBA、Visual Basic 6.0 或 Visual C\+\+ 6.0）中使用。  
  
## 本节内容  
 [COM 应用程序集成概述](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications-overview.md)  
 对集成过程的主要部分进行概述。  
  
 [如何：注册和配置服务标记](../../../../docs/framework/wcf/feature-details/how-to-register-and-configure-a-service-moniker.md)  
 若要在 COM 应用程序中使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务标记，请向 COM 注册所需属性化类型，并以所需绑定配置对 COM 应用程序和标记进行配置。  
  
 [如何：使用未注册的 Windows Communication Foundation 服务标记](../../../../docs/framework/wcf/feature-details/use-the-wcf-service-moniker-without-registration.md)  
 说明如何以 Web 服务定义语言 \(WSDL\) 文档的形式或者从 WS\-MetadataExchange 终结点获取协定的定义。  
  
 [如何：将服务标记用于 WSDL 协定](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-wsdl-contracts.md)  
 说明如何使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] WSDL 标记调用一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例。  
  
 [如何：将服务标记与元数据交换协定一起使用](../../../../docs/framework/wcf/feature-details/how-to-use-a-service-moniker-with-metadata-exchange-contracts.md)  
 说明如何使用指定 Mex 终结点的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 标记调用一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例。  
  
 [如何：指定通道安全凭据](../../../../docs/framework/wcf/feature-details/how-to-specify-channel-security-credentials.md)  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务标记支持 `IChannelCredentials` 接口，该接口允许使用一系列替换方法来指定通道凭据。  
  
## 参考  
 <xref:System.ServiceModel>  
  
## 请参阅  
 [与 COM\+ 应用程序集成](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)