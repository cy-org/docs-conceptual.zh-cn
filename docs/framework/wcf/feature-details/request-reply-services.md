---
title: "请求-答复服务 | Microsoft Docs"
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
  - "协定 [WCF], 请求-答复服务"
  - "请求-答复协定 [WCF]"
  - "WCF [WCF], 请求-答复服务"
  - "Windows Communication Foundation [WCF], 请求-答复服务"
ms.assetid: 2fa710f1-47f4-4598-b063-3ab3bd22ebba
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 请求-答复服务
请求\-答复服务是 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中操作协定的默认类型。客户端调用服务操作并等待服务的响应。您可以同步执行对服务操作的调用（客户端接收到服务的响应或调用超时前客户端将保持阻止状态），也可以异步执行对服务操作的调用（客户端调用服务操作，继续工作，并在其他线程上接收服务的响应）。  
  
 若要创建请求\-答复服务协定，请定义服务协定，然后对每个操作应用 <xref:System.ServiceModel.OperationContractAttribute> 类，如下面的示例代码所示。  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IRequestReplyCalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
}  
  
```  
  
 您不必将 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 属性设置为 `false`，因为这是默认行为。  
  
## 请参阅  
 [单向服务](../../../../docs/framework/wcf/feature-details/one-way-services.md)   
 [双工服务](../../../../docs/framework/wcf/feature-details/duplex-services.md)