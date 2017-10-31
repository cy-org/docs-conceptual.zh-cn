---
title: "基于目标和使用的标准比较 ASP.NET Web 服务与 WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3890278-fa9b-4902-91ea-8da73b7143cc
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 基于目标和使用的标准比较 ASP.NET Web 服务与 WCF
开发 ASP.NET Web 服务的目标是生成通过使用 Simple Object Access Protocol \(SOAP\) over HTTP 来发送和接收消息的应用程序。  消息的结构可使用 XML 架构来定义，并且提供了一种工具，以便将消息序列化为 .NET Framework 对象以及将这种对象反序列化为消息。  该技术可以自动生成元数据，以便用 Web 服务描述语言 \(WSDL\) 描述 Web 服务，并且提供了另一个工具，用来从 WSDL 生成 Web 服务的客户端。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用于使 .NET Framework 应用程序能够与其他软件实体交换消息。  默认情况下使用 SOAP，但消息可采用任何格式，并可以使用任何传输协议传递。  消息的结构可使用 XML 架构来定义，并且提供多种选项以便将消息序列化为 .NET Framework 对象以及将这种对象反序列化为消息。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可以自动生成元数据来描述使用 WSDL 中的技术生成的应用程序，而且它还提供了一个工具，用来从 WSDL 生成这些应用程序的客户端。  
  
 [使用 ASP.NET 创建的 XML Web 服务](http://go.microsoft.com/fwlink/?LinkId=94872)（可能为英文网页）中介绍了 ASP.NET Web 服务支持的标准。  [系统提供的互操作性绑定支持的 Web 服务协议](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)更为详细地列出了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 所支持的标准。  
  
## 请参阅  
 [从开发的角度比较 ASP.NET Web 服务与 WCF](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)