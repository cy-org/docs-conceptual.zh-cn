---
title: "Windows Communication Foundation 绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "绑定 [WCF]"
  - "WCF [WCF], 绑定"
  - "Windows Communication Foundation [WCF], 绑定"
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Windows Communication Foundation 绑定
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 将应用程序软件的编写方式与该软件和其他软件的通信方式分离开来。绑定用于指定客户端与服务相互通信所需的传输、编码和协议详细信息。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用绑定来生成终结点的基础网络表示，因此，进行通信的各方必须对大多数绑定详细信息达成一致。完成此任务的最简单方法是让服务的客户端使用该服务的终结点所使用的绑定。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何进行此操作的更多信息，请参见[Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)。  
  
 绑定由绑定元素的集合组成。每个元素描述终结点与客户端的通信方式的某一方面。一个绑定必须至少包括一个传输绑定元素，至少包括一个消息编码绑定元素（默认情况下，传输绑定元素可能提供该元素）以及包括任意数目的其他协议绑定元素。使用本说明中生成运行时的进程，每个绑定元素均可为该运行时提供代码。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供包含常见绑定元素选择的绑定。这些绑定可以与其默认设置一起使用，您也可以根据用户要求修改这些默认值。这些系统提供的绑定具有一些属性，可以通过这些属性直接控制绑定元素及其设置。通过为绑定的每个版本提供其自己的名称，还可以轻松地并行使用该绑定的多个版本。有关详细信息，请参见[配置系统提供的绑定](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)。  
  
 如果需要的绑定元素集合不是由系统提供的这些绑定之一提供，则可以创建由所需绑定元素的集合组成的自定义绑定。这些自定义绑定易于创建且不需要新类，但是，它们不提供用于控制绑定元素或其设置的属性。您可以访问这些绑定元素并通过包含它们的集合修改其设置。有关详细信息，请参见 [自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
## 本节内容  
 [配置系统提供的绑定](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 描述如何使用和修改 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的绑定来支持常用方案。  
  
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 描述如何在代码中以强制方式和使用配置以声明方式来定义服务和客户端的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 绑定。  
  
 [自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)  
 描述什么是 <xref:System.ServiceModel.Channels.CustomBinding> 以及何时使用它。  
  
## 参考  
 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## 相关章节  
 [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)