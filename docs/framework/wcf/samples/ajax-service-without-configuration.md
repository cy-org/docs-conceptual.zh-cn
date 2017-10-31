---
title: "无配置的 AJAX 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6db7acd-5679-45d4-b98a-8449c6873838
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 无配置的 AJAX 服务
本示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 创建一个基本的 ASP.NET 异步 JavaScript 和 XML \(AJAX\) 服务（可通过从 Web 浏览器客户端使用 JavaScript 代码访问的服务）而不使用任何配置设置。  该服务在 .svc 文件中使用特殊语法来自动启用 AJAX 终结点。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对 AJAX 的支持经过了优化，以便通过 `ScriptManager` 控件与 ASP.NET AJAX 一起使用。  有关将 ASP.NET AJAX 与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 一起使用的示例，请参见 [Ajax Samples](http://msdn.microsoft.com/zh-cn/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e)。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 此示例是基于使用 HTTP POST 的 AJAX 服务生成的。  如[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)示例中所述，<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 用于承载服务。  
  
```  
<%ServiceHost  
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CalculatorService  
    Factory="System.ServiceModel.Activation.WebScriptServiceHostFactory"  
%>  
  
```  
  
 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 自动将 <xref:System.ServiceModel.Description.WebScriptEndpoint> 添加到服务。  如果不需要对终结点进行任何配置更改，则可从服务的 Web.config 文件中完全移除 \<system.ServiceModel\> 部分。  Web.config 文件包含一些由 ConfigFreeClientPage.aspx 使用的 ASP.NET 设置。  如果不是这样，则可以移除整个 Web.config 文件。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Ajax\ConfigFreeAjaxService`  
  
#### 设置、生成和运行示例  
  
1.  确保按照 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)中的安装说明进行操作。  
  
2.  按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明生成解决方案 ConfigFreeAjaxService.sln。  
  
3.  导航到 http:\/\/localhost\/ServiceModelSamples\/ConfigFreeClientPage.aspx（不要在浏览器中从项目目录内打开 ConfigFreeClientPage.aspx）。  
  
> [!NOTE]
>  运行此示例时，请确保不要对 IIS 中的 ServiceModelSamples 文件夹同时启用匿名身份验证和 Windows 身份验证。  如果同时启用了这两种身份验证，请禁用 Windows 身份验证。  运行了该示例后，请启用 Windows 身份验证并运行“iisreset”。  
  
## 请参阅  
 [基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)