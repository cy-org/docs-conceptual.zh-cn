---
title: "使用字节流编码器编码二进制对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 020ee981-c889-4b12-a3ea-91823ef46444
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 使用字节流编码器编码二进制对象
使用 <xref:System.ServiceModel.Channels.ByteStreamMessageEncodingBindingElement> 配置通过 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 发送和接收原始二进制数据。  
  
## 字节流消息编码器体系结构  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用的二进制消息编码器没有功能可用于处理、验证或标识消息中的基础二进制数据。数据包会编码为 XML 进行发送、接收和解码。编码器在数据传递到传输之后但在消息发送到消息队列之前处理数据。在功能上，二进制编码器将消息数据包装在 `<binary>` 元素中进行发送，并在收到消息之后删除元素。  
  
## 使用字节流消息编码器  
 下面的示例演示实现字节流消息编码器的服务协定。  
  
```csharp  
[OperationContract]  
Void Myfunction(Stream stream);  
```  
  
 下面的示例演示调用的服务。  
  
```csharp  
proxy.MyFunction(stream);  
```  
  
 使用实现消息基础结构（如路由器）的服务时，将直接处理消息，而不进行检查、验证或通过其他方式与消息交互，如下面的示例所示。  
  
```csharp  
[OperationContract]  
void ProcessMessage(Message message) ;  
```  
  
## 方案  
 字节流编码器可在以下方案中使用。  
  
-   在使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的计算机之间传输 JPEG 图像。在此方案中，图像会通过传输从外部源到达，而发送的数据会是组成图像的原始字节。某个服务会接收二进制数据并显示图像。  
  
-   从消息队列读出信息并进行处理。消息会从消息队列管理器中读取，并在消息队列通道中向上传递以进行处理。消息队列通道会充当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道堆栈中的队列管理器。  
  
 对于通过消息队列通道发送消息，发送方无法控制从队列管理器接收的字节。如果接收进程无法读取原始字节，则消息会以错误格式接收，不会进行处理；假定接收进程能够将接收的字节转换为可用格式。