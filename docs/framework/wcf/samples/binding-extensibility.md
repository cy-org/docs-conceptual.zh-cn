---
title: "绑定扩展性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabdd583-ddf5-493e-9dba-c6c31cde8f65
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 绑定扩展性
本节包含演示 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中自定义绑定的示例。  
  
## 本节内容  
 <xref:System.ServiceModel.NetHttpBinding>  
 演示如何实现在 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> 之上堆积 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 或 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement> 的绑定。  
  
 <xref:System.ServiceModel.WSStreamedHttpBinding>  
 演示如何创建一个绑定，该绑定用于在使用 HTTP 传输时支持件流式传送方案。