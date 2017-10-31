---
title: "使用消息级编程在 Json 中序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5f940ba2-57ee-4c49-a779-957c5e7e71fa
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 使用消息级编程在 Json 中序列化
WCF 支持 JSON 格式的序列化数据。本主题描述如何使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 判断 WCF 要序列化您的类型。  
  
## 类型化的消息编程  
 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute> 应用于服务操作时使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>。这两个属性允许您指定 `RequestFormat` 和 `ResponseFormat`。对请求和响应集这两个就这些使用 JSON `WebMessageFormat.Json`。为了使用 JSON ，必须使用 <xref:System.ServiceModel.WebHttpBinding> 自动配置 <xref:System.ServiceModel.Description.WebHttpBehavior>。有关 WCF 序列化的更多信息，请参见：[序列化和反序列化](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)、[Windows Communication Foundation](http://msdn.microsoft.com/magazine/cc163569.aspx) 的序列化。有关 JSON 和 WCF 的详细信息，请参见 [RESTfull 与 WCF 服务简介](http://msdn.microsoft.com/magazine/dd315413.aspx)，[创建 JSON 启用 WCF服务。.NET 3.5](http://www.pluralsight-training.net/community/blogs/fritz/archive/2008/01/31/50121.aspx)，和 [的其余部分在 WCF 概述](http://msdn.microsoft.com/netframework/dd547388)。  
  
> [!IMPORTANT]
>  使用 JSON 需要使用 <xref:System.ServiceModel.WebHttpBinding> 和 <xref:System.ServiceModel.Description.WebHttpBehavior>，不支持 SOAP 通信。与进行通信的服务 <xref:System.ServiceModel.WebHttpBinding> 因此将不能使用 svcutil 命令线工具或 Visual Studio 添加服务引用功能生成的客户端不支持显露服务元数据\-侧代理。如何以编程方式可以调用服务，使用的详细信息 <xref:System.ServiceModel.WebHttpBinding>，请参见 [如何消耗 REST 服务 WCF](http://blogs.msdn.com/b/pedram/archive/2008/04/21/how-to-consume-rest-services-with-wcf.aspx)。  
  
## 非类型化的消息编程  
 直接使用非类型化的消息对象时您必须显式集要将它作为 JSON 序列的非类型化的消息上的属性。下面的代码段演示如何执行此操作。  
  
```  
 Message response = Message.CreateMessage(  
                  MessageVersion.None,    // No SOAP message version  
                             "*",                     // SOAP action, ignored since this is JSON  
                             "Response string: JSON format specified", // Message body  
                             new DataContractJsonSerializer(typeof(string))); // Specify DataContractJsonSerializer  
      response.Properties.Add( WebBodyFormatMessageProperty.Name,   
                    new WebBodyFormatMessageProperty(WebContentFormat.Json)); // Use JSON format  
  
```  
  
## 请参阅  
 [AJAX 集成和 JSON 支持](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)   
 [独立 JSON 序列化](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)   
 [JSON 序列化](../../../../docs/framework/wcf/samples/json-serialization.md)