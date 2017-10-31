---
title: "WebContentTypeMapper 示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# WebContentTypeMapper 示例
本示例演示如何将新内容类型映射到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 消息正文格式。  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint> 元素可插入 Web 消息编码器，它允许 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在同一个终结点接收 JSON、XML 或原始二进制消息。编码器通过查看请求的 HTTP 内容类型来确定消息的正文格式。本示例介绍 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 类，该类允许用户控制内容类型和正文格式之间的映射。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为内容类型提供一组默认的映射。例如，`application/json` 映射到 JSON，`text/xml` 映射到 XML。未映射到 JSON 或 XML 的任何内容类型都将映射到原始二进制格式。  
  
 在某些方案（例如推送式 API）中，服务开发人员不控制由客户端返回的内容类型。例如，客户端可以将 JSON 作为 `text/javascript` 而不是 `application/json` 返回。在这种情况下，服务开发人员必须提供从 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 派生的类型以正确处理给定的内容类型，如下面的示例代码所示。  
  
```  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
  
```  
  
 该类型必须重写 <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> 方法。该方法必须计算 `contentType` 参数并返回下列值之一：<xref:System.ServiceModel.Channels.WebContentFormat>、<xref:System.ServiceModel.Channels.WebContentFormat>、<xref:System.ServiceModel.Channels.WebContentFormat> 或 <xref:System.ServiceModel.Channels.WebContentFormat>。返回 <xref:System.ServiceModel.Channels.WebContentFormat> 时将遵从默认的 Web 消息编码器映射。在前面的示例代码中，`text/javascript` 内容类型映射到 JSON，所有其他映射保持不变。  
  
 若要使用 `JsonContentTypeMapper` 类，请在您的 Web.config 中使用以下设置：  
  
```  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 若要验证使用 JsonContentTypeMapper 的要求，请从上面的配置文件中移除 contentTypeMapper 特性。在尝试使用 `text/javascript` 来发送 JSON 内容时，客户端页加载将失败。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明生成解决方案 WebContentTypeMapperSample.sln。  
  
3.  定位到 http:\/\/localhost\/ServiceModelSamples\/JCTMClientPage.htm（不要在浏览器中从项目目录中打开 JCTMClientPage.htm）。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
  
## 请参阅