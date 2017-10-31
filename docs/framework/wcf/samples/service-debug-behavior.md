---
title: "服务调试行为 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9d8fd3fb-dc39-427a-8235-336a7e7162ba
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 服务调试行为
本示例演示如何配置服务调试行为设置。此示例基于实现 `ICalculator` 服务协定的[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。本示例在配置文件中显式定义服务调试行为。也可以在代码中强制完成此操作。  
  
 在此示例中，客户端是一个控制台应用程序 \(.exe\)，服务是由 Internet 信息服务 \(IIS\) 承载的。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 服务器的 Web.config 文件定义服务调试行为以启用帮助页和异常处理，如下面的示例所示。  
  
```  
  
<behaviors>  
     <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
         <!-- WARNING: Setting includeExceptionDetailInFaults = "True" could result in leaking secured server information to the client.-->  
         <!-- Please set this to false when deploying -->  
             <serviceDebug includeExceptionDetailInFaults="True" httpHelpPageEnabled="True"/>  
         </behavior>  
     </serviceBehaviors>  
</behaviors>  
  
```  
  
 [\<serviceDebug\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md) 是配置元素，使用它可以更改服务调试行为属性。用户可以修改此行为以实现以下目标：  
  
-   这使服务可以返回应用程序代码引发的任何异常，即使未使用 <xref:System.ServiceModel.FaultContractAttribute> 声明该异常。为此，需要将 `includeExceptionDetailInFaults` 设置为 `true`。此设置在调试服务器引发意外异常的事例时很有用。  
  
    > [!IMPORTANT]
    >  在生产环境中打开此设置会不安全。由于意外服务器异常可能具有某些不适用于客户端的信息，因此将 `includeExceptionDetailsInFaults` 设置为 `true` 可能导致信息泄露。  
  
-   用户还可以使用 [\<serviceDebug\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md) 来启用或禁用帮助页。每个服务可以选择公开一个帮助页，该帮助页包含有关服务的信息，其中包括要获取服务的 WSDL 的终结点。通过将 `httpHelpPageEnabled` 设置为 `true` 可以启用该帮助页。这将使帮助页返回到对服务基址的 GET 请求。通过设置另一个属性 `httpHelpPageUrl`，可以更改此地址。通过使用 HTTPS（而不是 HTTP）可以使其安全。这可以通过设置 `httpsHelpPageEnabled` 和 `httpsHelpPageUrl` 来完成。  
  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。前三个操作（加、减和乘）都会成功。最后一个操作（“除”）由于除数为零异常而失败。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\ServiceDebug`  
  
## 请参阅