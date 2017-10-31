---
title: "WCF Web HTTP 错误处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 02891563-0fce-4c32-84dc-d794b1a5c040
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# WCF Web HTTP 错误处理
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] Web HTTP 错误处理可用于从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Web HTTP 服务返回指定 HTTP 状态代码的错误，并且返回的错误详细信息使用与操作相同的格式（如 XML 或 JSON）。  
  
## WCF Web HTTP 错误处理  
 <xref:System.ServiceModel.Web.WebFaultException> 类定义可用于指定 HTTP 状态代码的构造函数。随后会将此状态代码返回到客户端。<xref:System.ServiceModel.Web.WebFaultException> 类的泛型版本 <xref:System.ServiceModel.Web.WebFaultException%601> 可用于返回用户定义的类型，该类型中包含有关所出现错误的信息。将使用由操作指定的格式序列化此自定义对象，并将它返回到客户端。下面的示例演示如何返回 HTTP 状态代码。  
  
```  
Public string Operation1()  
{   // Operation logic  
   // ...  
   Throw new WebFaultException(HttpStatusCode.Forbidden);  
}  
```  
  
 下面的示例演示如何在用户定义的类型中返回 HTTP 状态代码和额外信息。`MyErrorDetail` 是用户定义的类型，其中包含有关所出现错误的额外信息。  
  
```  
Public string Operation2()  
   // Operation logic  
   // ...   MyErrorDetail detail = new MyErrorDetail  
   {  
      Message = “Error Message”,  
      ErrorCode = 123,  
   }  
   throw new WebFaultException<MyErrorDetail>(detail, HttpStatusCode.Forbidden);  
}  
```  
  
 上述代码返回 HTTP 响应，其中包括禁止状态代码以及包含 `MyErrorDetails` 对象实例的正文。`MyErrorDetails` 对象的格式由以下内容确定：  
  
-   服务操作指定的 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute> 特性的 `ResponseFormat` 参数值。  
  
-   <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> 的值。  
  
-   通过访问 <xref:System.ServiceModel.Web.OutgoingWebResponseContext> 得到的 <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> 属性值。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]这些值如何影响操作的格式设置的更多信息，请参见 [WCF Web HTTP 格式设置](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)。  
  
 <xref:System.ServiceModel.Web.WebFaultException> 是一个 <xref:System.ServiceModel.FaultException>，因此可用作公开 SOAP 终结点和 Web HTTP 终结点的服务的错误异常编程模型。  
  
## 请参阅  
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [WCF Web HTTP 格式设置](../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md)   
 [定义和指定错误](../../../../docs/framework/wcf/defining-and-specifying-faults.md)   
 [处理异常和错误](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md)   
 [发送和接收错误](../../../../docs/framework/wcf/sending-and-receiving-faults.md)