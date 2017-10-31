---
title: "当 Web 场中承载 WCF 服务时防止重放攻击 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c2ed695-7a31-4257-92bd-9e9731b886a5
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 当 Web 场中承载 WCF 服务时防止重放攻击
当使用 WCF 消息安全性防止重播攻击通过创建 NONCE 传入的邮件和检查内部 `InMemoryNonceCache` 以查看是否存在生成的 NONCE。如果是，则该消息被丢弃重播。WCF 服务时承载在 web 场中，自 `InMemoryNonceCache` 不共享跨 web 场中的节点，服务是脆弱重播攻击。若要减轻此方案 WCF4.5 提供了一个允许您通过从抽象类派生的类来实现您自己的共享的杜撰缓存的扩展性点<xref:System.ServiceModel.Security.NoneCache>。  
  
## NoneCache 执行  
 若要实现您自己的共享的杜撰缓存，派生类从 <xref:System.ServiceModel.Security.NoneCache> 和重写 [M:System.ServiceModel.Security.NoneCache.CheckNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.CheckNonce%2A> 和 [M:System.ServiceModel.Security.NoneCache.TryAddNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.TryAddNonce%2A> 方法。[M:System.ServiceModel.Security.NoneCache.CheckNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.CheckNonce%2A> 将检查缓存中是否存在指定的 NONCE。[M:System.ServiceModel.Security.NoneCache.TryAddNonce\(System.Byte\<xref:System.ServiceModel.Security.NoneCache.TryAddNonce%2A>尝试向缓存添加 NONCE。一旦实现类，你其挂钩的实例化一个实例，并将其分配给<xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSecuritySettings.NonceCache%2A> 客户端\-侧重播检测和  <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSecuritySettings.NonceCache%2A> 服务器端重播检测。没有支持此功能框配置。  
  
## 请参阅  
 [消息安全](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)   
 [SymmetricSecurityBindingElement](../../../../docs/framework/wcf/diagnostics/wmi/symmetricsecuritybindingelement.md)