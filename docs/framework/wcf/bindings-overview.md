---
title: "Windows Communication Foundation 绑定概述 | Microsoft Docs"
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
  - "绑定 [WCF], 概述"
ms.assetid: cfb5842f-e0f9-4c56-a015-f2b33f258232
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Windows Communication Foundation 绑定概述
绑定是用于指定连接到 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务终结点所必需的通信详细信息的对象。  [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务中的每个终结点都要求正确指定绑定。  本主题概述了绑定所定义的通信详细信息类型、绑定的元素、[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 中包含哪些绑定以及如何为终结点指定绑定。  
  
## 绑定所定义的内容  
 绑定中的信息可能非常基本，也可能非常复杂。  最基本的绑定仅指定连接终结点所必需的传输协议（如 HTTP）。  一般来说，绑定包含的有关如何连接到终结点的信息属于以下类别中的一种。  
  
 协议  
 确定要使用的安全机制：可靠消息传递功能或事务上下文流设置。  
  
 编码  
 确定消息编码（例如，文本或二进制）。  
  
 传输  
 确定要使用的基础传输协议（例如，TCP 或 HTTP）。  
  
## 绑定的元素  
 绑定基本上由绑定元素的有序堆栈组成，其中每个元素都指定了连接到服务终结点所必需的通信信息的一部分。  该堆栈中最底下的两层都是必需的。  该堆栈的最底层为传输绑定元素，而紧挨着它的上面一层为包含消息编码规范的元素。  用于指定其他通信协议的可选绑定元素位于这两个必需元素的上面。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]这些绑定元素及其正确排序的更多信息，请参见[自定义绑定](../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
## 系统提供的绑定  
 绑定中的信息可能十分复杂，而且某些设置可能与其他设置不兼容。  因此，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包含一组系统提供的绑定。  这些绑定旨在满足大多数应用程序要求。  下面的类表示系统提供的绑定的一些示例：  
  
-   <xref:System.ServiceModel.BasicHttpBinding>：一个 HTTP 协议绑定，适用于连接到符合 WS\-I 基本配置文件规范的 Web 服务（例如，基于 ASP.NET Web 服务的服务）。  
  
-   <xref:System.ServiceModel.WSHttpBinding>：一个可互操作的绑定，适用于连接到符合 WS\-\* 协议的终结点。  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>：使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 连接到同一计算机上的其他 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 终结点。  
  
-   <xref:System.ServiceModel.NetMsmqBinding>：使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 创建与其他 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 终结点的排队消息连接。  
  
 有关 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 提供的所有绑定的完整列表及说明，请参见[系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)。  
  
## 使用自己的绑定  
 如果系统提供的绑定都不具有服务应用程序所需的正确功能组合，则可以创建自己的绑定。  有两种方法可以实现此目的。  您可以使用 <xref:System.ServiceModel.Channels.CustomBinding> 对象从预先存在的绑定元素创建新的绑定，也可以通过从 <xref:System.ServiceModel.Channels.Binding> 绑定派生来创建完全由用户定义的绑定。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]使用这两种方法创建自己的绑定的更多信息，请参见 [自定义绑定](../../../docs/framework/wcf/extending/custom-bindings.md) 和[创建用户定义的绑定](../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
## 使用绑定  
 使用绑定需要执行两个基本步骤：  
  
1.  选择或定义绑定。  最简单的方法就是选择 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 包含的系统提供绑定中的一个，并且通过该绑定的默认设置来使用它。  您还可以选择一个系统提供的绑定，然后根据您的要求重新设置它的属性值。  或者，您可以创建一个自定义绑定或用户定义的绑定，以实现更高程度的控制和自定义。  
  
2.  创建一个使用所选择或定义的绑定的终结点。  
  
## 代码和配置  
 可以通过两种方式来定义绑定：通过代码或通过配置。  这两种方法与您使用的是系统提供的绑定还是自定义绑定无关。  通常，使用代码可以使您在设计时对绑定的定义拥有完全的控制。  另一方面，使用配置则使系统管理员或 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务或客户端的用户可以更改绑定的参数，而不必重新编译服务应用程序。  由于无法预测用于部署 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 应用程序的特定计算机要求，因而通常需要这种灵活性。  通过将绑定（和寻址）信息保持在代码外部，人们可以更改这些信息，而不必重新编译或重新部署应用程序。  请注意，代码中定义的绑定是在配置中指定的绑定之后创建的，这使得代码定义的绑定可以覆盖配置中定义的任何绑定。  
  
## 请参阅  
 [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)