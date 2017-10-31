---
title: "使用自定义绑定的安全功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a2425679-484a-4e6c-9c98-7da7304f1516
caps.latest.revision: 11
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 11
---
# 使用自定义绑定的安全功能
使用系统提供的绑定之一，可以执行最常见的安全任务。但是，如果需要更多控制，则可以创建带有 <xref:System.ServiceModel.Channels.SecurityBindingElement> 的自定义绑定，以下这些主题将对此进行介绍。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]自定义绑定的更多信息，请参见[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
## 本节内容  
 [SecurityBindingElement 身份验证模式](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)  
 介绍可能用于自定义绑定的身份验证模式。  
  
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)  
 介绍创建带有安全元素的自定义绑定的基本步骤。  
  
 [如何：为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)  
 介绍如何为指定身份验证模式创建安全元素。  
  
 [如何：在 WSFederationHttpBinding 上禁用安全会话](../../../../docs/framework/wcf/feature-details/how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 介绍如何在创建联合服务时禁用安全会话。  
  
 [如何：启用消息重播检测](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)  
 介绍如何确定重放攻击出现的时间。  
  
 [如何：创建支持凭据](../../../../docs/framework/wcf/feature-details/how-to-create-a-supporting-credential.md)  
 介绍如何向服务提供支持凭据（如果服务要求）。  
  
 [如何：设置签名确认](../../../../docs/framework/wcf/feature-details/how-to-set-up-a-signature-confirmation.md)  
 介绍在对消息进行数字签名时确认签名的步骤。  
  
 [如何：设置最大时钟偏差](../../../../docs/framework/wcf/feature-details/how-to-set-a-max-clock-skew.md)  
 介绍如何设置服务与客户端之间所允许的最大时间差。  
  
 [如何：禁用数字签名的加密](../../../../docs/framework/wcf/feature-details/how-to-disable-encryption-of-digital-signatures.md)  
 介绍禁用对数字签名的加密能提高性能的方式。  
  
## 参考  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>  
  
 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)  
  
## 相关章节  
 [了解保护级别](../../../../docs/framework/wcf/understanding-protection-level.md)  
  
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)  
  
## 请参阅  
 [绑定与安全](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)   
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)